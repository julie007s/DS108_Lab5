# GUIDELINE HƯỚNG DẪN GÁN NHÃN CẢM XÚC BÌNH LUẬN (SENTIMENT LABELING GUIDELINE)

**Mục tiêu:** Phân loại chính xác và nhất quán sắc thái cảm xúc của các bình luận (comments) dưới bài đăng thành 3 nhóm duy nhất: **Positive**, **Negative**, và **Neutral**. Từ đó tìm hiểu xu hướng người dùng tương tác với một bài viết như thế nào và cách cộng đồng mạng hưởng ứng với nội dung bài viết.

---

## I. QUY ƯỚC CÁC NHÃN CẢM XÚC (LABEL DEFINITIONS)

### 1. Nhãn: Positive (Tích cực)

- **Định nghĩa:** Bình luận thể hiện sự đồng tình, khen ngợi, hài lòng, ủng hộ, vui vẻ, biết ơn hoặc trầm trồ đối với nội dung bài viết, tác giả hoặc sản phẩm/dịch vụ được nhắc đến.
- **Dấu hiệu nhận biết:**
  - Chứa từ ngữ tích cực: _hay, đẹp, xuất sắc, đỉnh, uy tín, chuẩn, thích, yêu, cảm ơn, hữu ích, chất lượng..._
  - Chứa emoji tích cực: ❤️, 😍, 👍, 👏, 🥰, 😂 (nếu đi kèm câu đùa vui vẻ).

- **Ví dụ:**
  - "Bài viết phân tích sâu sắc quá, cảm ơn tác giả!"
  - "Sản phẩm dùng siêu thích luôn, mọi người nên mua nha 👍"

### 2. Nhãn: Negative (Tiêu cực)

- **Định nghĩa:** Bình luận thể hiện sự bất bình, chê bai, chỉ trích, thất vọng, tức giận, bài trừ hoặc sử dụng giọng điệu mỉa mai, nói kháy nhằm hạ thấp đối tượng trong bài viết.
- **Dấu hiệu nhận biết:**
  - Chứa từ ngữ tiêu cực: _dở, tệ, rác, lừa đảo, chán, tồi, làm ăn vớ vẩn, câu view..._
  - Chứa emoji tiêu cực: 😡, 🤬, 🤮, 👎, 🙄.

- **Ví dụ:**
  - "Viết bài câu view rẻ tiền, thông tin sai sự thật."
  - "Đẹp mặt chưa, tự hào ghê cơ! (Giọng điệu mỉa mai ngữ cảnh xấu)."

### 3. Nhãn: Neutral (Trung tính)

- **Định nghĩa:** Bình luận mang tính chất trao đổi, hỏi đáp thông tin khách quan (không kèm thái độ), các bình luận tag bạn bè, hoặc bình luận rác/quảng cáo không mang sắc thái cảm xúc.
- **Dấu hiệu nhận biết:**
  - Câu hỏi thuần túy: _bao nhiêu, ở đâu, khi nào, xin giá, có size không shop..._
  - Bình luận chỉ chứa dấu chấm ("."), tag tên tài khoản khác, hoặc nội dung rao vặt.

- **Ví dụ:**
  - "Sản phẩm này có sẵn tại cửa hàng không ạ?"
  - "@NguyenVanA vào đây xem cái này nè."

---

## II. CÁC QUY TẮC XỬ LÝ TRƯỜNG HỢP ĐẶC BIỆT (CORNER CASES)

| Trường hợp đặc biệt                      | Quy tắc xử lý                                                                                                                     | Ví dụ minh họa                                                                      | Nhãn đúng                                  |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------ |
| **Bình luận chứa cả khen và chê**        | Ưu tiên sắc thái chiếm trọng số mạnh hơn hoặc cảm xúc chốt ở cuối câu. Nếu cân bằng bằng nhau $\rightarrow$ Chọn **Neutral**.     | "Hàng giao hơi chậm (Neg) nhưng chất lượng sản phẩm tuyệt vời, rất đáng tiền (Pos)" | **Positive**                               |
| **Từ chửi thề nhưng mang nghĩa vui đùa** | Tránh bẫy từ khóa (keyword trap). Nếu chửi thề nhưng để thể hiện sự trầm trồ, ngạc nhiên tích cực $\rightarrow$ Gán **Positive**. | "Vãi ô viết bài này đỉnh thực" <br>"Đm hay quá bro ơi!" sự!"                        | **Positive**                               |
| **Góp ý nhẹ nhàng, lịch sự**             | Nếu là góp ý mang tính đóng góp xây dựng, không dùng từ ngữ xúc phạm hay hằn học $\rightarrow$ Gán **Neutral**.                   | "Bài viết rất tốt nhưng nên kiểm tra lại lỗi chính tả ở đoạn 2 nhé tác giả."        | **Neutral**                                |
| **Bình luận chỉ có Emoji**               | Dựa hoàn toàn vào ý nghĩa của Emoji. Nếu Emoji vô thưởng vô phạt, không rõ nghĩa $\rightarrow$ Gán **Neutral**.                   | "🔥🔥🔥" hoặc "👏👏👏" <br>"🤡" (Chế giễu) hoặc "🤮" <br> "👉📱" (Chỉ tay)          | **Positive** <br> **Negative** **Neutral** |

---

## III. QUY TRÌNH THỰC HIỆN GÁN NHÃN (3-STEP WORKFLOW)

### Bước 1: Đọc hiểu ngữ cảnh chung

- Người gán nhãn cần đọc qua bài viết gốc (Post) trước để hiểu chủ đề đang được thảo luận là gì (Tránh việc đọc comment rời rạc dẫn đến hiểu sai ý nghĩa của các từ lóng).

### Bước 2: Thực hiện gán nhãn độc lập (Single Annotation)

- Đọc kỹ từng comment và áp dụng các quy tắc ở mục I và II để điền nhãn: **Positive**, **Negative**, hoặc **Neutral**.
- _Lưu ý:_ Không được tự ý bỏ qua các comment viết sai chính tả, teencode mà phải cố gắng đọc hiểu. Chỉ bỏ qua (gán Neutral) nếu comment hoàn toàn mất cấu trúc, không dịch được nghĩa.

### Bước 3: Tính toán độ đồng thuận

- Sau khi cả ba thành viên đều thực hiên gán nhãn, nhóm sẽ tiến hành tính toán độ đồng thuận bằng cách sử dụng Cohen's Kappa với công thức
  $$Am = \frac{P_0 - P_e}{1 - P_e}$$
- Sau đó, dựa trên thang đo của Landis và Koch để đánh giá mức độ đồng thuận giữa các thành viên. Kết quả là đạt khi độ đồng thuận của nhóm đạt >60%.
