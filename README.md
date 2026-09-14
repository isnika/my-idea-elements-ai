# BillScan - Trợ lý quét hóa đơn tự động bằng AI

Final project for the Building AI course

## Summary

BillScan là ứng dụng dùng camera điện thoại và AI thị giác máy tính (kết hợp OCR) để quét hóa đơn, bill mua hàng, tự động nhận diện thông tin quan trọng (ngày, tên cửa hàng, các mặt hàng, số tiền) và nhập trực tiếp vào bảng tính Excel, giúp cá nhân và chủ hộ kinh doanh nhỏ quản lý chi phí, doanh thu nhanh chóng mà không cần nhập liệu thủ công.

## Background

Đối với các hộ kinh doanh nhỏ, quán ăn, cửa hàng tạp hóa hay cá nhân tự quản lý chi tiêu, việc ghi chép lại hóa đơn mua hàng và bán hàng vào sổ sách hoặc file Excel thường tốn rất nhiều thời gian và dễ sai sót. Nhiều người có thói quen giữ lại hóa đơn giấy nhưng không bao giờ có thời gian tổng hợp lại, dẫn đến việc mất kiểm soát dòng tiền.

* Nhập liệu thủ công từ hóa đơn giấy vào Excel tốn thời gian và dễ nhầm số liệu
* Hóa đơn dễ bị thất lạc, mờ chữ theo thời gian nếu không được số hóa kịp thời
* Chủ hộ kinh doanh nhỏ thường không có nhân sự kế toán riêng để xử lý việc này

Động lực cá nhân của tôi đến từ việc quan sát thấy nhiều người quen, đặc biệt là chủ các cửa hàng nhỏ, phải ngồi hàng giờ cuối ngày để cộng sổ từ một chồng hóa đơn giấy. Tôi tin một công cụ chỉ cần chụp ảnh là tự động ghi vào Excel có thể giúp họ tiết kiệm rất nhiều thời gian và giảm sai sót.

## How is it used?

Người dùng mở ứng dụng, chụp ảnh hóa đơn (bill mua hàng, hóa đơn bán hàng, hóa đơn điện nước...). Ứng dụng sẽ:

1. Nhận diện và trích xuất văn bản trên hóa đơn (OCR)
2. Phân loại thông tin: ngày tháng, tên cửa hàng/đối tác, danh sách mặt hàng, đơn giá, tổng tiền
3. Tự động phân loại khoản mục vào "chi phí" hoặc "doanh thu" dựa trên loại hóa đơn
4. Ghi dữ liệu trực tiếp vào một dòng mới trong file Excel quản lý chi phí - doanh thu của người dùng

Đối tượng sử dụng chính là chủ hộ kinh doanh nhỏ, quán ăn, cửa hàng bán lẻ, freelancer, hoặc bất kỳ cá nhân nào muốn theo dõi chi tiêu cá nhân/gia đình một cách gọn gàng mà không cần phần mềm kế toán phức tạp và đắt tiền.

## Data sources and AI methods

Dữ liệu huấn luyện có thể lấy từ:

* Các bộ dữ liệu công khai về nhận diện hóa đơn như [SROIE (ICDAR 2019 Receipt OCR)](https://rrc.cvc.uab.es/?ch=13) và [CORD (Consolidated Receipt Dataset)](https://github.com/clovaai/cord)
* Ảnh hóa đơn tự thu thập theo mẫu phổ biến tại Việt Nam (hóa đơn siêu thị, hóa đơn bán lẻ viết tay, hóa đơn điện tử) để mô hình nhận diện tốt hơn với định dạng và font chữ trong nước

Phương pháp AI dự kiến:

* Kỹ thuật OCR (Optical Character Recognition) để chuyển hình ảnh chữ viết/in trên hóa đơn thành văn bản số
* Mô hình trích xuất thông tin có cấu trúc (Named Entity Recognition / Key Information Extraction), có thể tận dụng học chuyển giao (transfer learning) từ các mô hình sẵn có như LayoutLM để hiểu bố cục hóa đơn, không chỉ đọc chữ đơn thuần
* Có thể áp dụng phương pháp phân loại đơn giản dạng nearest neighbor đã học trong khóa này để phân loại nhanh loại hóa đơn (chi phí/doanh thu, theo danh mục) như một baseline so sánh với mô hình chính

| Thành phần   | Mô tả                                                  |
| ------------ | -------------------------------------------------------- |
| Đầu vào      | Ảnh chụp hóa đơn/bill                                   |
| Mô hình      | OCR + Key Information Extraction (transfer learning từ LayoutLM) |
| Đầu ra       | Dữ liệu có cấu trúc (ngày, đối tác, mặt hàng, số tiền) được ghi vào file Excel |

## Challenges

* Hóa đơn có thể bị mờ, nhăn, thiếu sáng, hoặc theo nhiều mẫu định dạng khác nhau khiến OCR đọc sai
* Việc phân loại tự động "chi phí" hay "doanh thu" đôi khi cần ngữ cảnh mà máy khó suy luận chính xác 100%, cần cho phép người dùng chỉnh sửa trước khi lưu
* Bảo mật và quyền riêng tư dữ liệu tài chính là vấn đề quan trọng cần cân nhắc kỹ khi lưu trữ và đồng bộ với Excel/đám mây
* Hiệu quả phụ thuộc vào việc người dùng chụp hóa đơn ngay khi phát sinh, thay vì để dồn lại

## What next?

* Hỗ trợ tự động tạo báo cáo tổng hợp (biểu đồ thu chi theo tuần/tháng) ngay trong Excel
* Tích hợp trực tiếp với Google Sheets hoặc phần mềm kế toán phổ biến để đồng bộ đa thiết bị
* Thêm tính năng nhắc nhở/cảnh báo khi chi phí vượt ngân sách đã đặt ra
* Cần thêm kỹ năng về phát triển ứng dụng di động (mobile development), xử lý ảnh (image preprocessing) và tích hợp API Excel/Google Sheets

## Acknowledgments

* Ý tưởng lấy cảm hứng từ các bài học về nearest neighbor và phân loại trong khóa học Building AI
* Bộ dữ liệu tham khảo: [SROIE Dataset - ICDAR 2019](https://rrc.cvc.uab.es/?ch=13)
* Bộ dữ liệu tham khảo: [CORD Dataset by Clova AI](https://github.com/clovaai/cord) / công khai cho mục đích nghiên cứu