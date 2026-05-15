# 01 · Base Flow + Chốt 3 Knobs

> **Mục tiêu**: Hiểu chatbot hoạt động ra sao ở mức base (không chọn config gì) — và xác định 3 knobs nhóm sẽ tweak ở các bước sau.
>
> **Thời gian**: 7 phút (trong 15 phút phần Setup)

---

## Bước 1 — Đọc base flow trong cost reference card

Mở file `cost-reference-card.md` ở phần **2. Base Flow** — xem flow chatbot mặc định. Đây là cấu trúc mọi config sẽ build dựa trên.

Đọc xong, tự kiểm tra hiểu:

- Khi tourist gửi tin nhắn, AI làm gì đầu tiên?
  - Nhận user message, chạy intent classification.
- 5 intent dẫn đến 5 hành động khác nhau — hành động nào tốn LLM, hành động nào không?
  - Visa/Guide/Weather dùng LLM; Booking và Khiếu nại chuyển người nên không tốn LLM.
- Sau khi route, AI ráp gì lại để generate response?
  - System prompt + history + RAG + web results (nếu bật) + user message → gửi model.

Nếu chưa hiểu → quay lại đọc lại 1 lần nữa. Đừng đi tiếp khi còn mơ hồ.

---

## Bước 2 — Vẽ lại flow theo cách hiểu của nhóm

```text
User message
    ↓
Intent classifier
    ↓
+--------------------------+----------------------+-----------------------+-------------------+-------------------+
| Visa/Policy              | Guide/Destination    | Weather/Event         | Tour/Booking      | Complaint         |
+--------------------------+----------------------+-----------------------+-------------------+-------------------+
| RAG (+optional web)      | RAG                  | Web search + RAG      | Handoff to Sales  | Escalate to Mgr   |
|                         |                      |                       | ($0 LLM cost)     | ($0 LLM cost)     |
+--------------------------+----------------------+-----------------------+-------------------+-------------------+
    ↓                        ↓                      ↓
Context assembly: system + history + RAG + user + web results
    ↓
Response generation (chosen model)
```

Flow cần đủ 4 điểm: intent → route → context → response. Chúng tôi đã vẽ để đảm bảo:

- Intent classification phân loại thành 5 nhánh.
- Booking và Complaint không tính LLM cost.
- Weather cần web search nếu bật.
- Context assembly gộp prompt + history + RAG + user + web.

---

## Bước 3 — Xác định 3 Knobs

### Knob 1 — Model tier

**Nhóm suy nghĩ**:

- Tourist hỏi cả câu hỏi đơn giản (itinerary, food) và câu hỏi quan trọng (visa, weather).
- Nếu chọn cheap toàn bộ, cost rất thấp nhưng visa/weather có thể thiếu độ chính xác.
- Nếu chọn premium toàn bộ, chất lượng cao nhưng chi phí tăng mạnh và có thể không cần cho mọi intent.
- Tốt nhất là dùng cheap cho FAQ/guide, premium/strong cho visa policy.

### Knob 2 — Web search

**Nhóm suy nghĩ**:

- Visa policy và weather thực sự cần thông tin real-time.
- Guide/Destination có thể dùng RAG từ KB đã có sẵn.
- Web search tốn thêm ~$0.008 + 800 tokens mỗi query, nên không bật broad vô tội vạ.
- ON selective cho Visa + Weather là điểm cân bằng hợp lý.

### Knob 3 — History management

**Nhóm suy nghĩ**:

- Scenario A chỉ 4 lượt, nên Last 3 đã đủ nhẹ và tiết kiệm.
- Scenario B 7 lượt, nên Last 5 giúp nhớ budget / điểm đến / yêu cầu vẫn còn cân bằng.
- Full history sẽ ít lỗi quên, nhưng mỗi turn dài hơn và chi phí tăng rõ rệt.
- Nếu bot quên budget hoặc lịch trình ở turn 6 thì trải nghiệm sẽ mất điểm.

---

## Bước 4 — Sơ bộ nhóm muốn thử những combo nào?

**Combo 1 (định hướng cheap)**:

```text
Model: Cheap (GPT-4o-mini)    Web: OFF    History: Last 3    (đặt tên dự kiến: Budget Bot)
```

**Combo 2 (định hướng premium)**:

```text
Model: Premium (Claude Opus 4.7)    Web: ON broad    History: Full    (đặt tên dự kiến: Premium Concierge)
```

**Combo 3 (định hướng balanced / smart mix)**:

```text
Model: Mixed (GPT-4o-mini general + Claude Sonnet visa)    Web: ON selective (Visa + Weather)    History: Last 5    (đặt tên dự kiến: Smart Mix)
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Đã vẽ flow base có đủ 4 bước (Intent → Route → Context → Response)
- [x] Hiểu Booking + Khiếu nại = $0 LLM cost (chuyển con người)
- [x] Đã phác thảo ≥3 combo khác nhau (chưa cần chi tiết)
- [x] Nhóm đồng thuận về hướng đi mỗi combo

Xong → 10:25 chuyển sang **Main phase**. Mở `02-config-design.md`.
