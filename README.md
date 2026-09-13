# EcoSort - Trợ lý phân loại rác tái chế bằng AI

Final project for the Building AI course

## Summary

EcoSort là ứng dụng dùng camera điện thoại và AI thị giác máy tính để nhận diện và hướng dẫn người dùng phân loại rác thải sinh hoạt tại các khu chung cư đô thị, giúp tăng tỷ lệ tái chế và giảm rác thải ra bãi chôn lấp. Building AI course project.

## Background

Ở các đô thị lớn như TP.HCM, phần lớn rác thải sinh hoạt không được phân loại đúng cách trước khi đem đi xử lý, dù nhiều chung cư và khu dân cư đã có quy định phân loại rác. Nguyên nhân chính là người dân không chắc chắn một món đồ nên bỏ vào thùng nào (tái chế, hữu cơ, hay rác thải chung), dẫn đến tâm lý "bỏ đại cho xong".

* Rác tái chế bị lẫn vào rác thường, khiến chúng không thể tái chế được nữa
* Thiếu công cụ hướng dẫn tức thời, dễ hiểu cho người dân
* Nhân lực phân loại thủ công tại các trạm trung chuyển tốn kém và không hiệu quả

Động lực cá nhân của tôi đến từ việc quan sát thấy các thùng rác phân loại tại khu tôi sống thường xuyên bị lẫn lộn, dù mọi người đều có ý định tốt. Tôi tin một công cụ đơn giản, dùng ngay trên điện thoại, có thể thay đổi hành vi này.

## How is it used?

Người dùng mở ứng dụng, chụp ảnh món đồ họ định vứt bỏ (ví dụ: chai nhựa, vỏ hộp sữa, thức ăn thừa). Ứng dụng sẽ:

1. Nhận diện vật thể trong ảnh
2. Cho biết nên bỏ vào loại thùng nào (tái chế / hữu cơ / rác thải chung)
3. Đưa ra mẹo nhỏ nếu cần xử lý trước khi vứt (ví dụ: rửa sạch hộp sữa trước khi bỏ vào thùng tái chế)

Đối tượng sử dụng chính là cư dân các khu chung cư, đặc biệt là các gia đình mới chuyển đến khu vực có quy định phân loại rác mà họ chưa quen. Ban quản lý chung cư và các đơn vị thu gom rác cũng có thể hưởng lợi gián tiếp nhờ rác đầu vào sạch hơn, ít lẫn tạp chất hơn.

## Data sources and AI methods

Dữ liệu huấn luyện có thể lấy từ:

* Các bộ dữ liệu ảnh rác thải công khai như [TrashNet](https://github.com/garythung/trashnet) và [TACO Dataset](http://tacodataset.org/)
* Ảnh tự chụp bổ sung các loại rác phổ biến tại Việt Nam (ví dụ: hộp xôi, ly trà sữa, lá chuối gói đồ ăn) để mô hình phù hợp với bối cảnh địa phương hơn

Phương pháp AI dự kiến:

* Mạng nơ-ron tích chập (Convolutional Neural Network - CNN) để phân loại ảnh, có thể tận dụng học chuyển giao (transfer learning) từ các mô hình có sẵn như MobileNet để chạy nhẹ trên điện thoại
* Sau khi có mô hình phân loại cơ bản, có thể áp dụng kỹ thuật tương tự bài toán nearest neighbor đã học trong khóa này như một baseline đơn giản để so sánh hiệu năng với mô hình CNN

| Thành phần   | Mô tả                                      |
| ------------ | ------------------------------------------- |
| Đầu vào      | Ảnh chụp một món đồ cần vứt bỏ              |
| Mô hình      | CNN (transfer learning từ MobileNet)        |
| Đầu ra       | Nhãn loại rác + hướng dẫn xử lý             |

## Challenges

* Mô hình có thể nhầm lẫn với các vật thể mới lạ, bao bì không phổ biến, hoặc vật thể bị che khuất, dơ bẩn, biến dạng
* Không giải quyết được vấn đề gốc rễ là hạ tầng thu gom và xử lý rác sau khi đã phân loại đúng
* Cần cân nhắc quyền riêng tư nếu ảnh chụp vô tình chứa thông tin cá nhân trong khung hình
* Hiệu quả phụ thuộc vào việc người dùng có thói quen sử dụng ứng dụng thường xuyên hay không

## What next?

* Mở rộng bộ dữ liệu với nhiều loại rác đặc thù của từng khu vực, từng quốc gia
* Tích hợp tính năng "điểm thưởng" hoặc gamification để khuyến khích người dùng duy trì thói quen phân loại rác
* Hợp tác với ban quản lý chung cư hoặc công ty môi trường đô thị để triển khai thí điểm thực tế
* Cần thêm kỹ năng về phát triển ứng dụng di động (mobile development) và tối ưu hóa mô hình AI để chạy được trên thiết bị có cấu hình thấp

## Acknowledgments

* Ý tưởng lấy cảm hứng từ các bài học về nearest neighbor và phân loại trong khóa học Building AI
* Bộ dữ liệu tham khảo: [TrashNet by Gary Thung and Mindy Yang](https://github.com/garythung/trashnet)
* Bộ dữ liệu tham khảo: [TACO Dataset](http://tacodataset.org/) / công khai cho mục đích nghiên cứu