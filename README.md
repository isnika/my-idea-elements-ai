# BillScan - AI-Powered Automatic Receipt Scanning Assistant

Final project for the Building AI course

## Summary

BillScan is an application that uses a phone camera and computer vision AI (combined with OCR) to scan receipts and purchase bills, automatically identify key information (date, store name, items, total amount), and enter it directly into an Excel spreadsheet — helping individuals and small business owners manage expenses and revenue quickly without manual data entry.

## Background

For small business owners, restaurants, grocery stores, or individuals managing their own spending, recording purchase and sales receipts into notebooks or Excel files is often time-consuming and error-prone. Many people keep their paper receipts but never find time to consolidate them, leading to a loss of control over cash flow.

* Manually entering data from paper receipts into Excel takes time and is prone to numerical errors
* Receipts can easily get lost or fade over time if not digitized promptly
* Small business owners often don't have dedicated accounting staff to handle this task

My personal motivation comes from observing many acquaintances, especially small shop owners, spending hours at the end of the day tallying up a stack of paper receipts. I believe a tool that only requires taking a photo to automatically record data into Excel could save them a great deal of time and reduce errors.

## How is it used?

The user opens the app and takes a photo of a receipt (a purchase receipt, sales invoice, utility bill, etc.). The application will:

1. Recognize and extract the text on the receipt (OCR)
2. Classify the information: date, store/partner name, list of items, unit prices, total amount
3. Automatically categorize the entry as an "expense" or "revenue" based on the type of receipt
4. Write the data directly into a new row in the user's expense-revenue management Excel file

The main target users are small business owners, restaurants, retail shops, freelancers, or anyone who wants to track personal or household spending neatly without needing complex and expensive accounting software.

## Data sources and AI methods

Training data can be sourced from:

* Public receipt recognition datasets such as [SROIE (ICDAR 2019 Receipt OCR)](https://rrc.cvc.uab.es/?ch=13) and [CORD (Consolidated Receipt Dataset)](https://github.com/clovaai/cord)
* Self-collected receipt images following common formats used in Vietnam (supermarket receipts, handwritten retail receipts, e-invoices) to help the model perform better with domestic formats and fonts

Planned AI approach:

* OCR (Optical Character Recognition) techniques to convert printed/handwritten text on receipts into digital text
* A structured information extraction model (Named Entity Recognition / Key Information Extraction), potentially leveraging transfer learning from existing models such as LayoutLM to understand receipt layout, not just read text
* A simple nearest-neighbor classification method, as learned in this course, could be applied to quickly classify receipt types (expense/revenue, by category) as a baseline for comparison with the main model

| Component | Description |
| --------- | ----------- |
| Input | Photo of a receipt/bill |
| Model | OCR + Key Information Extraction (transfer learning from LayoutLM) |
| Output | Structured data (date, partner, items, amount) written into an Excel file |

## Challenges

* Receipts may be blurry, wrinkled, poorly lit, or follow many different formats, causing OCR misreadings
* Automatically classifying an entry as "expense" or "revenue" sometimes requires context that is hard for a machine to infer with 100% accuracy, so users need to be able to review and edit before saving
* Data security and privacy of financial information are important considerations when storing and syncing with Excel/the cloud
* Effectiveness depends on users photographing receipts as soon as they are generated, rather than letting them pile up

## What next?

* Support automatic generation of summary reports (weekly/monthly income-expense charts) directly in Excel
* Direct integration with Google Sheets or popular accounting software for multi-device syncing
* Add a reminder/alert feature when expenses exceed a set budget
* Additional skills needed: mobile app development, image preprocessing, and Excel/Google Sheets API integration

## Acknowledgments

* Idea inspired by lessons on nearest neighbor and classification from the Building AI course
* Reference dataset: [SROIE Dataset - ICDAR 2019](https://rrc.cvc.uab.es/?ch=13)
* Reference dataset: [CORD Dataset by Clova AI](https://github.com/clovaai/cord) / publicly available for research purposes
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