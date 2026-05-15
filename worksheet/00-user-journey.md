# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm phải hình dung được khách hàng thật sự hỏi gì, hỏi như thế nào, và 1 conversation thực tế trông ra sao.
>
> **Thời gian**: 8 phút (trong 15 phút phần Setup)

---

## Bước 1 — Mỗi người đóng vai 1 tourist (4 phút)

### Tourist #1 — Lê Quang Minh

```text
1. Hi, can you recommend a good 7-day itinerary for exploring central Vietnam including Hue, Hoi An and Da Nang?
2. What is the current visa requirement for Australian tourists visiting Vietnam for 2 weeks?
3. Will it be suitable to visit Ha Long Bay in October, what's the typical weather?
4. Is it safe to rent a motorbike and self-drive from Hoi An to Da Nang?
5. What are the must-try local street foods in Ho Chi Minh City that are safe for foreigners?
6. Can you suggest some budget-friendly accommodations in the old quarter of Hanoi?
```

### Tourist #2 — Nguyễn Việt Hoàng

```text
1. Do you offer any group tours that cover Ha Giang loop for 4 days?
2. Can I modify my existing booking for the Mekong Delta tour?
3. Are there any unique cultural festivals happening in November that I shouldn't miss?
4. I need to extend my visa while I'm in Vietnam, what's the process?
5. My flight is delayed, can you help me reschedule my airport transfer?
6. What travel insurance do you recommend for international tourists visiting Vietnam?
```

---

## Bước 2 — Gom lại và phân loại (4 phút)

| #   | Câu hỏi (1 dòng)                                    | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
| --- | --------------------------------------------------- | --------------------- | -------------------------------- | ----------------------------- |
| 1   | 7-day itinerary for central Vietnam (Hue-HoiAn-DaNang) | Guide/Destination     | 4–5                              | ☑ Bot · □ Người               |
| 2   | Visa requirement for Australian tourists (2 weeks)  | Visa/Policy           | 3–4                              | ☑ Bot · □ Người               |
| 3   | Ha Long Bay weather in October                      | Weather/Event         | 2–3                              | ☑ Bot · □ Người               |
| 4   | Safety of motorbike rental Hoi An to Da Nang        | Guide/Destination     | 2–3                              | ☑ Bot · □ Người               |
| 5   | Must-try street foods in Ho Chi Minh City           | Guide/Destination     | 2                                | ☑ Bot · □ Người               |
| 6   | Budget accommodations in Hanoi old quarter         | Guide/Destination     | 3–4                              | ☑ Bot · □ Người               |
| 7   | Ha Giang loop group tours for 4 days                | Tour/Booking          | 3–4                              | □ Bot · ☑ Người               |
| 8   | Modify existing Mekong Delta tour booking           | Tour/Booking          | 2–3                              | □ Bot · ☑ Người               |
| 9   | Cultural festivals in November                      | Weather/Event         | 2–3                              | ☑ Bot · □ Người               |
| 10  | Visa extension process while in Vietnam             | Visa/Policy           | 4–5                              | ☑ Bot · □ Người               |
| 11  | Reschedule airport transfer due to delayed flight   | Khiếu nại             | 1                                | □ Bot · ☑ Người               |
| 12  | Recommended travel insurance for tourists           | Guide/Destination     | 2–3                              | ☑ Bot · □ Người               |

---

## Bước 3 — Rút insight cho nhóm (cuối phần Setup)

**Tổng số câu hỏi nhóm gom được**:

```text
12
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 50% (6/12)
Visa: 17% (2/12)
Weather: 17% (2/12)
Booking: 13% (2/12)
Khiếu nại: 8% (1/12)
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
3.5 lượt cho info (guide/visa/weather), 2.5 lượt cho booking, 1 lượt cho complaint
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Hợp lý vì nhóm có nhiều câu hỏi Guide/Itinerary phức tạp cần nhiều follow-up, scenario B (cao điểm) sẽ có nhiều câu hỏi visa/visa_extension phức tạp nên tổng lượt chat lên gần 7 lượt như đề bài.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Khách du lịch thường hỏi nhiều câu hỏi liên quan đến itinerary và local guide chiếm đa số (50%), cho thấy bot cần tập trung tối đa hóa khả năng trả lời các câu hỏi về điểm đến. Visa extensions và modification booking là các intent phức tạp nhất, cần bot có thể chuyển người ngay lập tức để tránh trải nghiệm không tốt cho khách hàng.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [x] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [x] Đã có phân bố intent % của nhóm (so với đề bài)
- [x] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.