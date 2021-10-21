# VIETNAMESE VIRTUAL ASSISTANT: VIAS
## Trợ lý ảo tiếng Việt **VIAS** 

### DỰ ÁN TRỢ LÝ ẢO TIẾNG VIỆT

**Các chức năng chính:**

    1. Chatbot tiếng Anh
    2. Thông báo ngày, giờ
    3. Mở Website, ứng dụng
    4. Tìm kiếm từ khóa trên Google
    5. Gửi email (Chưa hoàn thiện)
    6. Dự báo thời tiết
    7. Xem youtube
    8. Thay đổi hình nền máy tính
    9. Đọc báo hôm nay (Chưa hoàn thiện)
    10. Tìm kiếm trên Wikipedia 
    
#  Chức năng chuyển văn bản thành âm thanh
  -  Dùng `gTSS (google Text To Speech)` chuyển văn bản thành âm thanh theo tiếng Việt và lưu lại dưới dạng file **'voice + datatime'.mp3**
  -  Sau đó dùng hàm `playsound.playsound()` để đọc file **.mp3** trên máy tính
  -  Xóa file **.mp3** sau khi đọc xong để tránh lỗi trùng lắp file khi đọc nhiều văn bản
  -  Ngoài ra ta còn có hàm `speak_other_language` để đọc văn bản bằng 1 ngôn ngữ khác với biến `otherLanguage` truyền vào


#  Chức năng chuyển âm thanh thành văn bản
   Trong chức năng này, dùng 2 hàm là `get_audio()`, `stop()` và `get_text()`.
   
   ### Trong hàm `get_audio()`
 -  Dùng thư viện speech_recognition có chức năng nhân diện giọng nói để chuyển âm thanh thành văn bản.
 -  Âm thanh được đọc vào sau đó được xử lý qua hàm `listen()` và lưu vào biến **audio**.
 -  Âm thanh sẽ được nhận dạng ở tiếng Việt bằng hàm `recognize_google()` và lưu kết quả vào biến **text**
 - Nếu **audio** không lỗi tức `recognize_google()` có thể nhận dạng được thì hàm sẽ trả về **text**. Ngược lại, nếu lỗi thì sẽ trả về **0**.
 
  ### Trong hàm `stop()`
   Đọc đoạn text "Tạm biệt" bằng cách dùng hàm `speak()` ở trên.
   
  ### Trong hàm `get_text()`
 - Máy tính sẽ nhận dạng âm thanh của người đọc tối đa 3 lần (bằng cách dùng for 3 lần), nếu text khác **0** thì `get_text()` trả vè `text.lower()`. 
 - Ngược lại text = 0 thì trả về hàm `stop()` và `get_text()` trả về 0
 - `time.sleep(3)`: tạm dừng 3s tránh máy đọc các đoạn văn bản bị khớp nhau. 


#  Chức năng hiển thị thời gian
- Dùng thư viện **`datetime`**, lưu vào biến **now**
- Nếu trong biến **text** đầu vào có từ `"giờ"` thì sẽ đọc thời gian hiện tại trong ngày
- Nếu trong biến **text** đầu vào có từ `"ngày"` thì sẽ đọc thời điểm hiện tại trong năm


# Chức năng mở ứng dụng hệ thống, website và chức năng tìm kiếm từ khóa trên Google

### Hàm `open_application()`
- Dùng hàm `os.startfile()` để mở các file ứng dụng từ hệ thống

### Hàm `open_website()`
- Dùng hàm `re.search()` để tách "domain" sau từ "truy cập" trong biến **text** và ghép nó với phần tiền tố "https://www." để tạo thành **url** của web.
- Tiếp theo, dùng `webbroser.open(url)` để mở trang web theo url
- Nếu domain được tìm thấy thì thực hiện mở website bằng `open_website()` và trả về **True**, ngược lại thì không thực hiện gì cả và trả về **False**.

### Hàm `open_google_and_search()`
- Tách từ khóa sau từ "kiếm" trong **text** bằng `split()` rồi lưu vào **search_for**
- Gọi hàm `webdriver.Chrome(path)` để mở Google Chrome 
- Dùng hàm `driver.find_element_by_path()` để lấy thẻ **query** (viết tắt là q) rồi lưu vào biến que
- Biến **que** thực hiện tiềm kiếm từ khóa **search_for** và trả trên Google Search. 


#  Chức năng gửi Email (chưa hoàn thiện)
- Sử dụng thư viện **`smtplib`** để thực hiện gửi mail bằng stmp.
- SMTP - Simple Mail Transfer Protocol: Giao thức truyền tải thư tín đơn giản
- Lấy tên người nhận bằng hàm `get_text()`, lưu vào biến **recipient**
    vd: tìm thấy tên "thục" trong tên người cần gửi thì thực hiện gửi Email.
- Gọi `get_text()` để lấy nội dung cần gửi rồi lưu vào biến **content**
- Tiếp tục mở đường truyền gửi Email băng `stmp` rồi đăng nhập tài khoản Gmail của mình
- Kết nối thành công, sẽ gửi email từ địa chỉ đã đăng nhập đến địa chỉ người nhận (dinhthucf12@gmail.com) với nội dung **content** rồi đóng đường truyền


#  Chức năng xem dự báo thời tiết
- Dùng **Open WeatherMap** tại trang web `openweathermap.org`
- Dùng biến ow_url để lưu đường dẫn đến api của trang web
- Gọi get_text() để lấy thông tin thành phố cần xem thông tin thời tiết lưu vào biến **city**. Nếu không nghe được tên thì sẽ bỏ qua
- Kết nối với api của trang web (cần đăng ký tài khoản để lấy api_key)
- Biến **call_url** sẽ lưu đường dẫn đầy đủ để truy vấn bao gồm thông tin tên thành phố **city**
- Gọi `requests.get(call_url)` lấy thông tin truy vấn, lưu vào **response**
- `response.json()` sẽ chuyển dữ liệu về json rồi lưu vào **data**
- Nếu data["cod"] không trả về 404 tức requests không lỗi, thực hiện chức năng
- Từ **data** lấy các thông tin: **temperature**, **pressure**, **humidity**
- Lưu các kết quả vào biến **content** và đọc kết quả
- time.sleep(20): tạm dừng 20s để đọc **content**


# Chức năng tìm và phát video trên Youtube
- Gọi `get_text()` lấy thông tin tên bài hát, lưu vào **myTitlle**
- Gọi While để tìm kết quả (bỏ qua kết nối yếu, ... )
- Biến **url** lưu đường dẫn kế quả đầu tiên tìm thấy trên Youtube
- Dùng hàm `webbrowser.open(url)` để mở đường dẫn đến video tìm được trên Google Chrome để phát nhạc.


#  Chức năng thay đổi hình nền máy tính
- Dùng **Unsplash** tại trang web `unsplash.com`
- Đăng ký tài khoản để lấy api_key
- Biến **url** lưu đường dẫn đến api của trang web
- Mở url và lấy requests lưu vào biến **json_string**, ảnh sẽ được load, đọc và lưu vào biến **photo**
- **photo** sẽ được lưu lại thành file ảnh trong máy
- Dùng lệnh thay đổi hình nền của máy tính thông qua hàm `ctypes.windll.user32.SystemParametersInfoW()`


#  Chức năng đọc báo ngày hôm nay (Chưa hoàn thiện)
- Chọn **Newsapi** tại `newsapi.org`, đăng ký tài khoản lấy apiKey
- Lấy thông tin về chủ đề muốn đọc, dùng requests
- Kết quả thu được kiểu json lưu vào biến **api_response**
- Hiển thị 20 tin tức thu thập và mở đường dẫn đến 3 bài báo đầu tiên.


#  Chức năng tìm định nghĩa trên từ điển Wikipedia
- Dùng `get_text()` lấy thông tin về thứ muốn định nghĩa, lưu vào **text**
- Gọi hàm `wikipedia.summary(text).split('\n')` để lưu lại thành 1 list các đoạn nội dung mà wikipedia tìm được
- Đọc đoạn định nghĩa đầu tiên
- Máy sẽ hỏi bạn muốn nghe thêm hay không, nếu có máy sẽ đọc tiếp phần tiếp theo, nếu không thì sẽ dừng đọc


#  Chức năng giao tiếp, chào hỏi với máy (AI Chatbot)
- Chức năng giao tiếp thông thường giữa người và máy.
- Sử dụng Pytorch để xây dựng mô hình AI Chatbot để giao tiếp giữa người với máy
- Vẫn đang là tiếng Anh (chưa thể nâng cấp tiếng Việt)


#  Kết hợp tất cả chức năng 
- Dùng các cặp lệnh `if...elif...else` và `while True` để lặp vô hạn cho đến khi bạn muốn dừng
- `get_text()` để lấy thông tin yêu cầu người dùng, lưu vào **text**, nếu **text** nhận 0 tức máy không nghe được, máy sẽ break
- Nếu **text** nhận được giá trị, sẽ thực hiện các câu lệnh, khi nghe thấy "dừng lại" hoặc "tạm biệt" thì cũng sẽ dừng.

# Link Video Demo
- Youtube: https://www.youtube.com/watch?v=kozVHUuiy2M&ab_channel=PhamDinhThuc

# Tài liệu tham khảo
- Codelearn.io >> https://codelearn.io/sharing/lap-trinh-tro-ly-ao-tieng-viet-python
- Chat Bot With PyTorch - NLP Beginner Tutorial >> https://www.youtube.com/playlist?list=PLqnslRFeH2UrFW4AUgn-eY37qOAWQpJyg
