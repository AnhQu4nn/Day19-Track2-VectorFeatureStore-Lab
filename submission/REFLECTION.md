# Reflection — Lab 19

**Tên:** Anh Quan
**Cohort:** _<A20-K1 / A20-K2 / ...>_
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set, hybrid RRF là lựa chọn cân bằng nhất vì kết hợp tín hiệu lexical của BM25 và semantic của vector search. Với query `exact`, BM25 rất mạnh vì user dùng đúng keyword kỹ thuật như Kubernetes, OAuth, PostgreSQL; hybrid thường ngang hoặc nhỉnh hơn vì vẫn giữ được kết quả keyword tốt. Với `paraphrase`, vector search hữu ích hơn vì query diễn đạt lại ý nghĩa thay vì trùng từ, nhưng `BAAI/bge-small-en-v1.5` không tối ưu cho tiếng Việt nên semantic-only chưa luôn ổn định. Với `mixed`, hybrid thắng rõ nhất: phần exact giúp BM25 neo đúng topic, phần paraphrase giúp vector kéo thêm kết quả liên quan.

Tôi sẽ không dùng hybrid khi cần matching chính xác, audit được, hoặc query là mã định danh/log/error code; lúc đó BM25/filter tốt hơn. Nếu corpus/query rất đa ngôn ngữ và ít keyword ổn định, pure vector với model multilingual tốt có thể đơn giản hơn.

---

## Điều ngạc nhiên nhất khi làm lab này

Điều bất ngờ nhất là embedding model choice ảnh hưởng rất lớn: cùng pipeline vector search nhưng model English-trained làm paraphrase tiếng Việt yếu hơn kỳ vọng. Hybrid không phải “magic”, nó thắng vì bù trừ lỗi của hai retriever.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
