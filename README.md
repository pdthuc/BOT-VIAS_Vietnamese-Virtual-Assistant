# Virtual Assistant: VIAS
## Trợ lý ảo tiếng Việt **VIAS** 

### DỰ ÁN TRỢ LÝ ẢO TIẾNG VIỆT

**Các chức năng cơ bản:**

    1. Chào hỏi
    2. Hiển thị giờ
    3. Mở website, application
    4. Tìm kiếm trên Google
    5. Gửi email
    6. Dự báo thời tiết
    7. Mở video trên Youtube
    8. Thay đổi hình nền máy tính
    9.  Đọc báo hôm nay
    10. Tìm và đọc định nghĩa trên Wikipedia
    
# 1. Chức năng chuyển văn bản thành âm thanh

  -  Dùng `gTSS (google Text To Speech)` chuyển văn bản thành âm thanh theo tiếng Việt và lưu lại dưới dạng file **sound.mp3**
  -  Sau đó dùng hàm `playsound.playsound()` để đọc file **sound.mp3** trên máy tính
  -  Xóa file **sound.mp3** sau khi đọc xong để tránh lỗi trùng lắp file khi đọc nhiều văn bản

