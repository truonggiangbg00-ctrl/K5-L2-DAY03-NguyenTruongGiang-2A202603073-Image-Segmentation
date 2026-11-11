# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: …
- Ngày / CVAT local: …
- Công cụ đã dùng: …

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic | 3 / 3 | 20 |
| medium_instance | medium_instance | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic | 3 / 2 | 30 |
| cp1_holes | cp1_holes | 1 / 1 | 3 |
| cp2_slice | cp2_slice | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion | 1 / 1 | 3 |
| cp3_thin | cp3_thin | 1 / 1 | 3 |
| cp4_curb | cp4_curb | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh "000000181542.jpg", vị trí xe máy bên phải ảnh, object Medium đầu tiên tự vẽ là xe máy
- Class và quy tắc tôi dùng để chọn biên: Class MOTORCYCLE. Khi vẽ mask, tôi dựa vào đường viền thực tế của xe, bao gồm thân xe, bánh xe và các bộ phận có thể nhìn thấy. Những phần thuộc về người điều khiển không được tính vào mask xe máy. Với các phần bị người che khuất, tôi chỉ vẽ theo vùng còn nhìn thấy, không tự suy đoán phần bị che.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai, hành động sửa và lý do: Ở khu vực xe máy và người điều khiển, cần kiểm tra các đường biên vì hai đối tượng nằm sát nhau và có phần chồng lấp. Tôi ưu tiên giữ những vùng gợi ý trùng với đường viền thực tế và điều chỉnh những vùng có nguy cơ lấn sang đối tượng khác.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.
Tôi chọn tách người và xe máy thành các đối tượng riêng biệt vì đây là hai class khác nhau. Dù người đang ngồi trên xe, không nên gộp toàn bộ thành một mask.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: hard_panoptic/ảnh "000000350023.jpg"/ vùng đường đi.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Biên / phủ vùng (vùng cần kiểm tra)
- Bằng chứng tôi nhìn thấy: Khu vực phía dưới ô tô, đặc biệt quanh các bánh xe, có ranh giới phức tạp với mặt đường và những vùng bị che khuất. Nếu đặt các điểm polygon chưa chính xác, mask có thể thiếu một phần xe hoặc lấn sang nền đường.
- Quy tắc và hành động sửa: Cần phóng to khu vực ô tô để kiểm tra đường biên, bổ sung hoặc di chuyển các điểm polygon chưa khớp với hình dạng xe. Chỉ lấy những phần thực sự thuộc về ô tô và có thể nhìn thấy, không mở rộng mask sang mặt đường hay phương tiện phía sau. Chuyển layout phần đường về sau
- Sau sửa đã Save và export lại chưa? Rồi

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Ảnh "000000181542.jpg"/ Vị trí xe máy | Gộp người với xe máy thành một vùng hoặc tách thành hai đối tượng riêng.|Người được tô đỏ, xe máy được tô xanh. Hai đối tượng tiếp xúc nhưng thuộc hai class khác nhau.|Chọn tách người và xe máy. Mask của xe chỉ bao gồm các bộ phận thuộc xe, không bao gồm cơ thể người điều khiển.|
| Ảnh "000000350023.jpg"/ Vị trí mặt đường |Chỉ lấy phần thân xe rõ ràng hoặc lấy cả những phần bánh xe có thể nhìn thấy.|Bánh xe thuộc ô tô nhưng một số vùng tối phía dưới có thể khó phân biệt với bóng đổ và mặt đường.|Chọn lấy cả phần bánh xe nhìn thấy được, loại bỏ vùng bóng đổ và mặt đường. Không tự vẽ thêm phần bị che khuất.|
| Ảnh "000000458325.jpg"/ Vị trí cuối đường |Gộp các đối tượng cùng class đang chồng lấp hoặc tách từng đối tượng riêng biệt.|Có nhiều người và xe máy nằm sát nhau, một số phần bị che bởi đối tượng phía trước.|Chọn tách từng đối tượng có thể phân biệt được. Chỉ vẽ những vùng nhìn thấy và kiểm tra kỹ ranh giới giữa các mask.|
