# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm phải hình dung được khách hàng thật sự hỏi gì, hỏi như thế nào, và 1 conversation thực tế trông ra sao.
>
> **Thời gian**: 8 phút (trong 15 phút phần Setup)

---

## Bước 1 — Mỗi người đóng vai 1 tourist (4 phút)

### Tourist #1 (Hannah)

```text
1. Hi, can you recommend a good 5-day itinerary for first-time visitors to Vietnam?
2. What is the current visa requirement for US tourists visiting Vietnam?
3. Will it rain in Ho Chi Minh City next weekend?
4. Is it safe to travel alone in Da Nang right now?
5. What local dishes should I try in Hoi An?
```

### Tourist #2 (Alex)

```text
1. Do you have any budget tours for Hanoi and Ha Long Bay?
2. Can I pay for the tour with a foreign credit card?
3. Are there any special festival events in September?
4. Can I extend my visa while traveling in Vietnam?
5. Can you help me book an airport pickup?
```

### Tourist #3 (Mina)

```text
1. What is the easiest way to get from Hanoi to Sapa?
2. I heard visa rules changed recently, is that true?
3. My hotel transfer is delayed, can someone help?
4. Which beaches are best in July for families?
5. Do you offer tours that include local cooking classes?
```

---

## Bước 2 — Gom lại và phân loại (4 phút)

| #   | Câu hỏi (1 dòng)                                    | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
| --- | --------------------------------------------------- | --------------------- | -------------------------------- | ----------------------------- |
| 1   | Recommend a 5-day itinerary for first-time visitors | Guide/Destination     | 3–4                              | ☑ Bot · □ Người               |
| 2   | Current visa requirement for US tourists            | Visa/Policy           | 3–4                              | ☑ Bot · □ Người               |
| 3   | Will it rain in Ho Chi Minh City next weekend?      | Weather/Event         | 2–3                              | ☑ Bot · □ Người               |
| 4   | Budget tours for Hanoi and Ha Long Bay              | Tour/Booking          | 2–3                              | □ Bot · ☑ Người               |
| 5   | Is it safe to travel alone in Da Nang right now?    | Guide/Destination     | 2–3                              | ☑ Bot · □ Người               |
| 6   | Pay with foreign credit card                        | Tour/Booking          | 1–2                              | □ Bot · ☑ Người               |
| 7   | Local dishes to try in Hoi An                       | Guide/Destination     | 2                                | ☑ Bot · □ Người               |
| 8   | Hotel transfer is delayed, can someone help?        | Khiếu nại             | 1                                | □ Bot · ☑ Người               |
| 9   | Special festival events in September                | Weather/Event         | 2–3                              | ☑ Bot · □ Người               |
| 10  | Can I extend my visa while traveling?               | Visa/Policy           | 3–4                              | ☑ Bot · □ Người               |

---

## Bước 3 — Rút insight cho nhóm (cuối phần Setup)

**Tổng số câu hỏi nhóm gom được**:

```text
10
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 30%
Visa: 20%
Weather: 20%
Booking: 20%
Khiếu nại: 10%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
4 lượt cho info (guide/visa/weather), 1 lượt cho booking, 1 lượt cho complaint
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Hợp lý vì scenario A là conversation info ngắn, Scenario B thêm visa/weather và follow-up nên lên gần 7 lượt.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Tourist thường pha nhiều intent trong 1 conversation, nên bot cần route và preserve context. Visa + weather cần data cập nhật, còn booking/khiếu nại nhất định phải chuyển người để giữ chi phí hợp lý.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [x] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [x] Đã có phân bố intent % của nhóm (so với đề bài)
- [x] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.
