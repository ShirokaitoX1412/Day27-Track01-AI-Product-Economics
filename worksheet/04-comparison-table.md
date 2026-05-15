# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp tất cả số đã tính ở `03-cost-calculation.md` thành 1 bảng so sánh duy nhất — đây là artifact chính nhóm sẽ present.
>
> **Thời gian**: 10 phút (đầu phần Final)

---

## Vì sao có bảng so sánh?

Khi sếp hỏi "Nên deploy config nào?", bạn cần đặt lên bàn **1 bảng** thay vì đọc 3 báo cáo riêng. Bảng so sánh đầy đủ cho phép so sánh thẳng từng dòng, dễ nhìn ra tradeoff.

---

## Bảng chính

|                                        | Config 1                            | Config 2                                | Config 3                                        |
| -------------------------------------- | ----------------------------------- | --------------------------------------- | ----------------------------------------------- |
| **Tên**                                | Budget Bot                          | Premium Concierge                       | Smart Mix                                       |
| **① Model**                            | GPT-4o-mini                         | Claude Opus 4.7                         | Mixed: GPT-4o-mini general + Claude Sonnet visa |
| **② Web search**                       | OFF                                 | ON broad                                | ON selective (Visa, Weather)                    |
| **③ History**                          | Last 3                              | Full                                    | Last 5                                          |
| **Intent classifier**                  | Keyword                             | LLM                                     | Keyword                                         |
| **Cost / conv (Scenario A — 4 turns)** | $0.0018                             | $0.1104                                 | $0.0187                                         |
| **Cost / conv (Scenario B — 7 turns)** | $0.0033                             | $0.2059                                 | $0.0410                                         |
| **Monthly A** (300 conv/day × 30)      | $16.20                              | $993.60                                 | $168.30                                         |
| **Monthly B** (1,200 conv/day × 30)    | $118.80                             | $7,410.60                               | $1,476.00                                       |
| **vs human $4,500/mo (A)**             | rẻ 278×                             | rẻ 4.5×                                 | rẻ 27×                                          |
| **vs human $18,000/mo (B)**            | rẻ 151×                             | rẻ 2.4×                                 | rẻ 12×                                          |
| **Savings % (A)**                      | 99.6%                               | 78.0%                                   | 96.3%                                           |
| **Savings % (B)**                      | 99.3%                               | 58.8%                                   | 91.8%                                           |
| **Quality estimate**                   | Low/Med                             | High                                    | Med/High                                        |
| **Speed estimate**                     | High                                | Low                                     | Medium                                          |
| **Điểm yếu chính**                     | Rõ ràng nhất, dễ lỗi visa outdated  | Chi phí cao nếu traffic tăng            | Phức tạp routing, vẫn có chi phí visa cao       |
| **Best for** (khi nào nên dùng)        | Mùa thấp điểm hoặc traffic siêu cao | Khách VIP / launch giai đoạn thử nghiệm | Khi cần chất lượng tốt mà vẫn tiết kiệm         |

---

## Quan sát nhanh từ bảng

### Câu 1 — Config rẻ nhất là gì? Đắt nhất là gì?

```text
Rẻ nhất: Budget Bot — monthly B = $118.80
Đắt nhất: Premium Concierge — monthly B = $7,410.60
Chênh: ~62× lần
```

### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

```text
Đổi từ cheap model (GPT-4o-mini) sang premium model (Claude Opus) tăng cost trên mỗi conv khoảng 30–60×. Web search broad tăng thêm ~$0.056 / conv ở Scenario B, còn selective tăng nhẹ khoảng $0.016 / conv. History Full vs Last 3 chỉ làm chi phí cao hơn ở các turn dài, nhưng không bằng lệnh model tier và web search broad.
```

### Câu 3 — Tại sao Scenario B không đắt ×4 lần Scenario A?

```text
Scenario B dài hơn nhưng chi phí không nhân 4 vì phần system prompt, RAG và một số turn vẫn cố định. Ngoài ra, booking/khiếu nại vẫn là $0 LLM cost nên nếu traffic B có tỉ lệ chuyển người cao hơn thì cost/conv thấp hơn kỳ vọng ×4.
```

### Câu 4 — Có config nào AI đắt hơn human không?

```text
Không có. Cả 3 config đều rẻ hơn human baseline ở cả Scenario A và B. Ngay cả Premium Concierge vẫn rẻ hơn 2.4× ở B, và Budget Bot tiết kiệm cực mạnh nhờ model cheap + không web search.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Bảng đầy đủ — không còn ô trống
- [x] Đã có 4 câu trả lời cho 4 quan sát ở trên
- [x] Nhóm đồng thuận về số trong bảng (đã sanity check)

Xong → mở `05-recommendation.md` để viết recommendation cuối + chuẩn bị present.
