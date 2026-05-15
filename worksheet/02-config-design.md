# 02 · Configuration Design — Đặt tên + Chốt knobs cho ≥3 Configs

> **Mục tiêu**: Biến phác thảo ở `01-base-flow.md` thành ≥3 configurations chi tiết, mỗi config có tên + 3 knobs đã chốt + lý do chọn.
>
> **Thời gian**: 15 phút (đầu phần Main, trước khi tính cost)

---

## Config 1

**Tên config**:

```text
Budget Bot
```

### 3 Knobs

**① Model tier**:

```text
Response model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens (input/output)
Classifier model: Keyword rules → giá $0 / $0 per 1M tokens
```

**② Web search**:

```text
☑ OFF
□ ON selective — bật cho intent: __________________
□ ON broad
```

**③ History management**:

```text
☑ Last 3
□ Last 5
□ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

Budget Bot phục vụ tình huống mùa thấp điểm và traffic cao, khi công ty cần giữ chi phí triển khai thấp nhất. Config này dùng cheap model và không gọi web search, nên cost/turn gần như tối thiểu. Đây là lựa chọn hợp lý khi mục tiêu là trả lời nhanh cho các câu hỏi guide và trả lời cơ bản.

### Rủi ro lớn nhất của config này

Visa info có thể outdated nếu web OFF, và Last 3 dễ quên thông tin budget hoặc yêu cầu người dùng cũ.

---

## Config 2

**Tên config**:

```text
Premium Concierge
```

### 3 Knobs

**① Model tier**:

```text
Response model: Claude Opus 4.7 → giá $5.00 / $25.00 per 1M tokens
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
□ OFF
□ ON selective — bật cho intent: __________________
☑ ON broad
```

**③ History management**:

```text
□ Last 3
□ Last 5
☑ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

Premium Concierge nhằm tới khách hàng khó tính, cần thông tin real-time và lịch sử chat đầy đủ. Web search broad đảm bảo visa, weather và sự kiện đều tươi mới, trong khi Full history giữ nguyên bối cảnh yêu cầu phức tạp. Thích hợp cho giai đoạn ra mắt dịch vụ cao cấp hoặc khi muốn bảo đảm độ chính xác tối đa.

### Rủi ro lớn nhất của config này

Chi phí mỗi conversation cao, đặc biệt khi traffic lớn và web search chạy mỗi turn.

---

## Config 3

**Tên config**:

```text
Smart Mix
```

### 3 Knobs

**① Model tier**:

```text
Response model: Mixed — GPT-4o-mini cho general, Claude Sonnet 4.6 cho visa/policy → giá blended khoảng $0.15/$0.60 và $3.00/$15.00 per 1M tokens
Classifier model: Keyword rules → giá $0 / $0 per 1M tokens
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa/Policy, Weather/Event
□ ON broad
```

**③ History management**:

```text
□ Last 3
☑ Last 5
□ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

Smart Mix cân bằng chi phí và độ chính xác: vẫn dùng cheap model cho hướng dẫn, nhưng nâng cấp visa/policy bằng strong model. Web search chỉ bật với visa và weather để giữ data fresh mà không phí phạm. Last 5 history đủ nhớ thông tin du lịch mà không phình token quá nhanh.

### Rủi ro lớn nhất của config này

Khó quản lý routing giữa cheap/strong model và vẫn có chi phí cao hơn Budget Bot nếu visa queries xuất hiện nhiều.

---

## Bảng kiểm trước khi tính cost

- [x] ≥3 configs đã đặt tên (không chỉ "Config 1/2/3")
- [x] Mỗi config đã chốt rõ 3 knobs (không còn ô trống)
- [x] Mỗi config có ≥2 câu lý do
- [x] 3 configs đủ khác biệt — không phải chỉ đổi mỗi 1 knob nhỏ
- [x] Nhóm đồng thuận đây là 3 configs đáng so sánh

Xong → mở `03-cost-calculation.md` để bắt đầu tính cost.
