# Quy định quản lý code bằng git - github
## Quản lý git repository 
Việc phát triển và quản lý một git repository được thực hiện theo workflow như sau:
![Workflow tiêu chuẩn](workflow.png)

Các branch chính:
- master: branch chứa các phiên bản chính thức, quan trọng của project. Code trong branch này phải hoạt động ổn định. Ứng với mỗi phiên bản được lưu vào branch master, người phụ trách project sẽ tải code về và lưu vào drive của dự án.
- develop: branch chính dùng để phát triển ứng dụng. Hầu hết các hoạt động phát triển project sẽ được thực hiện trên branch này.
- Các branch feature: các branch tạo ra để phát triển tính năng riêng mà không sợ ảnh hưởng đến code chính hoặc để code song song nhiều tính năng khi code nhóm. Cú pháp đặt tên: feature-tên-tính-năng. Sau khi tính năng hoàn tất, chuyển code về branch chính thông qua lệnh merge.
- hotfixes: nếu branch master xảy ra bug khi chạy chính thức, dùng branch hotfixes để sửa lỗi đó. Sau khi sửa lỗi, merge code trong hotfixes về master. Nếu hotfixes đạt tiêu chuẩn code của project, có thể merge code trong hotfixes vào develop.
- release: branch này dùng để test project trong môi trường production trước khi merge vào master. Khi xảy ra bug, tiếp tục fix trong branch này rồi merge vào master và develop.

Quy trình phát triển repository:
- Tạo repository ở branch master.
- Tạo branch develop để bắt đầu code. Nếu chia project thành nhiều tính năng, tạo thêm các branch feature. Với các project đơn giản thì không bắt buộc.
- Nếu sử dụng các branch feature, dùng các branch này để code các tính năng. Khi một tính năng hoàn tất, merge branch feature vào develop.
- Khi code trong branch develop đủ tiêu chuẩn để tạo một phiên bản chính thức, merge branch develop vào release để thử nghiệm với môi trường production. Nếu khi thử nghiệm phát hiện bug, tạo các commit để debug ngay trên branch này. Lưu ý, việc debug trong branch này vẫn phải đảm bào chất lượng code.
- Sau khi code trong release đã hoạt động ổn định, merge release vào branch master. Nếu đã xảy ra hoạt động sửa lỗi, merge vào branch develop để cập nhật các đoạn code sửa lỗi.
- Sau khi đã chạy production trên branch master mà xảy ra lỗi, merge brnach master vào branch hotfixes để debug. Việc debug này phải đảm bảo nhanh để đưa code hoạt động trở lại nên đôi khi có thể không cần đảm bảo chất lượng code đúng chuẩn, sạch đẹp. Sau khi sửa xong bug, merge branch này vào branch master để code hoạt động trở lại. Nếu code fix bug vẫn đảm bảo chất lượng, có thể merge branch này vào branch develop để cập nhật code sửa lỗi.

## Đặt tên github repository
Cú pháp đặt tên: tên-loại-dự-án_tên-project-lớn_tên-project-con\
Ví dụ: web-api_cha_warehouse

Giải thích:
- tên-loại-dự-án: loại project của repository. Các loại repository thường dùng:
  - web-api: web API
  - desktop: desktop app
  - mobile: mobile app
  - console: console app
  - service: windows service
  - ...
- tên project lớn: tên của nhóm project tổng thể repository đang tham gia. Ví dụ: cha cho các dự án làm với công ty nhựa cha.
- tên project con: tên của project con thuộc nhóm project lớn. Ví dụ: injection-molding-machine là dự án dùng cho máy ép.
