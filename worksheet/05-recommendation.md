# 05 · Recommendation + Justification — Kết luận & Chuẩn bị Present

> **Mục tiêu**: Chọn 1 config (hoặc combo) nhóm recommend deploy, viết justification ngắn gọn, và chuẩn bị 5 phút present.
>
> **Thời gian**: 10 phút (cuối phần Final) — Pens down lúc 12:00

---

## Bảng số ai cũng tính được. PM giỏi phải **recommend** và **justify**.

Đây là phần quan trọng nhất — phần phân biệt nhóm chỉ làm xong với nhóm thực sự hiểu sản phẩm.

---

## 4 câu hỏi nhóm phải trả lời

Mỗi câu trả lời 2–4 câu. Không lan man, không clichés. Mỗi câu phải justify được bằng số trong bảng so sánh.

### Câu 1 — Recommend config nào?

Trước khi viết, thảo luận 1 phút:

- Recommend 1 config duy nhất chạy quanh năm? Hay 2 configs khác nhau cho mùa thấp / mùa cao?
- Có nên recommend "Smart Mix model theo intent" thay vì pick 1 config cố định không?
- Nếu sếp nói "chỉ deploy 1 config thôi" — chọn cái nào?

```text
Nhóm recommend Smart Mix làm config chính chạy quanh năm. Lý do: cân bằng hoàn hảo giữa chi phí ($162-$1,260/tháng) và chất lượng cao. Tiết kiệm >93% so với human ở cả 2 mùa, trong khi vẫn đảm bảo visa/weather info luôn fresh nhờ web selective và model Claude Sonnet cho các intent phức tạp. Nếu ngân sách cực kỳ hạn chế vào mùa thấp điểm, có thể tạm chuyển sang Budget Bot.
```

### Câu 2 — So với human baseline $0.50/conv → tiết kiệm bao nhiêu? Có đắt hơn human ở chỗ nào không?

```text
Tiết kiệm 96.4% ở mùa thấp điểm, 93.0% ở mùa cao điểm. Tổng tiết kiệm $4,338/tháng (so với $4,500 của human) vào thấp điểm và $16,740/tháng (so với $18,000) vào cao điểm. AI không thể thay thế hoàn toàn nhân viên cho việc booking, nhưng AI thắng ở 24/7 hoạt động, hỗ trợ đa ngôn ngữ, và xử lý được volume đột biến vào mùa cao điểm mà không cần tuyển thêm nhân sự tạm thời.
```

### Câu 3 — Khi nào nên upgrade / downgrade config?

Trước khi viết, tự hỏi:

- Volume bao nhiêu thì cost AI scale lớn hơn benefit?
- Quality complaint rate bao nhiêu thì biết Budget Bot không đủ?
- Có signal nào báo nên chuyển sang Premium? (mùa cao điểm bắt đầu? customer feedback?)

```text
Nên upgrade lên Premium Concierge khi: monthly conversations > 40,000 + quality complaint rate > 5% + bắt đầu vào mùa cao điểm (Tết Nguyên Đán, mùa hè). Nên downgrade về Budget Bot khi: monthly conv < 5,000 + mùa thấp điểm kéo dài + tỷ lệ conversion booking không tăng đủ để justify chi phí Smart Mix.
```

### Câu 4 — Rủi ro lớn nhất của config được chọn?

Trước khi viết, tự hỏi:

- Rủi ro về quality? (visa info outdated? language mismatch?)
- Rủi ro về cost? (provider tăng giá? volume spike?)
- Rủi ro về business? (khách bị bot trả lời sai → bad review → mất khách?)
- Có mitigation plan không?

```text
Rủi ro chính: Provider tăng giá API >30% → margin bị co lại. Mitigation: Monitor cost hàng tháng, có sẵn fallback sang DeepSeek V4 Pro ($1.74/$3.48) thay vì Claude Sonnet nếu giá Anthropic tăng. Rủi ro phụ: Web search thất bại → visa info outdated. Mitigation: Update RAG visa policy hàng tuần, fallback sang human ngay nếu bot không có đủ thông tin chắc chắn.
```

---

## Final answer — Recommendation in 1 paragraph

Tổng hợp 4 câu trên thành 1 paragraph 5–7 câu — đây là phần nhóm sẽ đọc / chiếu khi present.

```text
Nhóm chúng tôi đề xuất triển khai Smart Mix làm giải pháp chính cho chatbot AI. Với chi phí chỉ $162/tháng mùa thấp điểm và $1,260/tháng mùa cao điểm, config này tiết kiệm được 93-96% so với chi phí nhân viên ($4,500-$18,000/tháng). Sự kết hợp giữa GPT-4o-mini cho câu hỏi thông thường và Claude Sonnet 4.6 cho visa/policy, cùng web search chỉ bật cho 2 intent quan trọng, giúp cân bằng hoàn hảo giữa chi phí và chất lượng. Dù có chi phí cao hơn Budget Bot ~8.5 lần, Smart Mix tránh được rủi ro thông tin outdated và mất context, đảm bảo trải nghiệm khách hàng tốt mà vẫn tiết kiệm cực lớn so với dùng nhân viên hoàn toàn.
```

---

## Chuẩn bị Present (5 phút)

Chia 5 phút thành 5 nhịp. 1 người trong nhóm chính phụ trách 1 nhịp. Người còn lại trả lời Q&A.

### Nhịp 0:00 – 0:30 — Base flow + 3 knobs đã chọn

Ai trình bày: **Lê Quang Minh**

Nói gì:

```text
Chúng tôi có base flow gồm intent classification → routing → RAG/web search → response generation. 3 knobs chính là model tier, web search strategy, và history management mà chúng tôi tweak để tạo 3 config khác biệt.
```

### Nhịp 0:30 – 1:00 — Config overview

Ai trình bày: **Nguyễn Việt Hoàng**

Nói gì (đọc nhanh tên + knobs 3 configs):

```text
1. Budget Bot: GPT-4o-mini, web OFF, Last 3 history — cực rẻ
2. Premium Concierge: Claude Opus, web ON broad, Full history — chất lượng cao nhất
3. Smart Mix: Mix model, web selective, Last 5 history — cân bằng chi phí/chất lượng
```

### Nhịp 1:00 – 2:00 — Cost comparison

Ai trình bày: **Nguyễn Việt Hoàng**

Nói gì (chiếu bảng so sánh, highlight rẻ nhất / đắt nhất):

```text
Budget Bot rẻ nhất chỉ $19-$137/tháng. Premium Concierge đắt nhất $765-$5,472/tháng. Smart Mix ở giữa với $162-$1,260/tháng. Tất cả configs đều tiết kiệm >69% so với human baseline $0.50/conv.
```

### Nhịp 2:00 – 3:00 — Key insight

Ai trình bày: **Lê Quang Minh**

Nói gì (knob nào ảnh hưởng cost nhiều nhất + tại sao):

```text
Model tier là knob ảnh hưởng cost nhiều nhất — chọn Claude Opus thay vì GPT-4o-mini làm tăng chi phí ~40×. Web search và history management chỉ ảnh hưởng ~10-15% tổng chi phí.
```

### Nhịp 3:00 – 4:30 — Recommendation + justification

Ai trình bày: **Lê Quang Minh**

Nói gì (đọc paragraph "Final answer" ở trên):

```text
Nhóm chúng tôi đề xuất triển khai Smart Mix làm giải pháp chính. Với chi phí $162-$1,260/tháng, tiết kiệm 93-96% so với nhân viên. Mix model + web selective cân bằng chi phí và chất lượng, đảm bảo visa/weather info luôn fresh mà không phí phạm.
```

### Nhịp 4:30 – 5:00 — Hardest question prep

Ai trình bày: **Nguyễn Việt Hoàng**

Nhóm dự đoán câu hỏi khó nhất sẽ bị hỏi là gì?

```text
Tại sao không dùng Budget Bot cho cả năm mà phải chi thêm tiền cho Smart Mix? Rủi ro của Budget Bot có thực sự lớn không?
```

Câu trả lời sẵn:

```text
Budget Bot không có web search → visa info có thể outdated gây misunderstanding khách hàng. Smart Mix chỉ tốn thêm ~$140/tháng mùa thấp điểm nhưng tránh được rủi ro khách hàng phàn nàn. ROI cực kỳ dương khi chỉ thêm ít chi phí mà cải thiện đáng kể trải nghiệm.
```

---

## Q&A — 2 phút sau khi present xong

Sẵn sàng cho 1 câu từ class + 1 câu từ instructor. Không cần lo lắng — nếu chưa biết câu trả lời, nói "đây là điểm nhóm chưa nghĩ đến — sẽ tính lại sau buổi".

**3 câu instructor thường hỏi**:

1. *"Knob nào ảnh hưởng cost nhiều nhất trong config của nhóm? Tại sao?"*
2. *"Nếu provider tăng giá API ×2 → config của nhóm còn sống được không?"*
3. *"So với nhóm X (vừa present trước) — tại sao nhóm bạn chọn khác?"*

Suy nghĩ trước câu trả lời ngắn:

```text
1. Model tier — vì giá model strong đắt hơn cheap ~40×, ảnh hưởng lớn nhất đến total cost.
2. Vẫn sống được — Smart Mix vẫn tiết kiệm >85% so với human ngay cả khi giá ×2. Chỉ Premium có thể bị ảnh hưởng nhiều hơn.
3. (phụ thuộc nhóm khác)
```

---

## Bảng kiểm cuối cùng — trước 12:00 Pens Down

- [ ] Đã trả lời 4 câu PM (Recommend / Savings / Threshold / Risk)
- [ ] Final answer paragraph viết gọn (5–7 câu)
- [ ] Phân công 5 nhịp present cho mỗi thành viên
- [ ] Có sẵn câu trả lời cho 3 câu Q&A dự đoán
- [ ] Comparison table có sẵn để chiếu / chuyền tay khi present
- [ ] Repo đã commit + push (sẽ nộp link sau buổi học)

---

## Sau buổi học

1. **Commit + push repo** với tất cả file đã điền.
2. **Dán link repo** vào Discord `#day27-evidence-boards` trước 23:59.
3. **Chuẩn bị cho D28**: peer review giữa các nhóm — sẽ bị hỏi câu chất vấn khó hơn instructor. Polish thêm bảng + recommendation tối nay.

*Hôm nay bạn chứng minh bằng số. Ngày mai bạn bảo vệ bằng logic.*