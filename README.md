# Quick Translator - Ứng dụng Dịch Anh - Việt cho điện thoại Android

Ứng dụng Android chuẩn Native (Kotlin) cho phép bạn **bôi đen bất kỳ đoạn văn bản tiếng Anh nào trên điện thoại** (trong trình duyệt Chrome, ứng dụng đọc sách/PDF, Facebook, Zalo, Tin nhắn, Báo chí...) và dịch ngay lập tức sang tiếng Việt.

---

## 🌟 Cơ chế hoạt động trên Android (Chuẩn `PROCESS_TEXT`)

Trên Android, khi bạn dùng ngón tay chạm giữ và **bôi đen văn bản**:
1. Thanh công cụ ngữ cảnh của Android sẽ xuất hiện các nút: *Sao chép*, *Chia sẻ*, và nút **"Dịch sang tiếng Việt"** (do ứng dụng Quick Translator tự động tích hợp vào hệ thống).
2. Khi bạn bấm chọn **"Dịch sang tiếng Việt"**:
   - Một **thẻ dịch nổi bán trong suốt (Floating Dialog)** sẽ lập tức xuất hiện ngay trên màn hình mà **không làm bạn bị thoát khỏi ứng dụng đang đọc**.
   - Hiển thị bản dịch tiếng Việt chuẩn xác.
   - Nút loa 🔊 phát âm chuẩn tiếng Anh.
   - Nút sao chép 📋 bản dịch 1 chạm.
   - Tra từ điển / từ loại (danh từ, động từ, từ đồng nghĩa) nếu bạn chọn từ đơn.
   - Bấm **✕** hoặc chạm ra vùng ngoài để đóng thẻ dịch nhanh chóng.

---

## 📱 Cách lấy file cài đặt `.apk` vào điện thoại

Bạn có 2 cách cực kỳ tiện lợi để xuất file `.apk` cài vào điện thoại:

### Cách 1: Biên dịch tự động trên đám mây qua GitHub (Không cần cài Java/Android Studio)

Trong thư mục dự án đã cấu hình sẵn quy trình **GitHub Actions CI/CD** tự động (`.github/workflows/build-apk.yml`).
1. Tạo một Repository mới trên tài khoản GitHub của bạn (ví dụ đặt tên: `quick-translator-android`).
2. Tải toàn bộ thư mục `android-quick-translator` này lên GitHub.
3. Bấm vào tab **Actions** trên GitHub:
   - Hệ thống đám mây của GitHub sẽ tự động biên dịch ứng dụng Android trong khoảng 2 phút.
   - Sau khi hoàn thành, bạn bấm vào bản build và tải file **`QuickTranslator-Debug-APK`** về.
4. Mở file `.apk` trên điện thoại để cài đặt và sử dụng ngay!

---

### Cách 2: Biên dịch qua Android Studio trên máy tính (1 cú nhấp chuột)

Nếu máy tính của bạn đã có sẵn **Android Studio**:
1. Mở Android Studio.
2. Chọn **Open Project** và chọn thư mục:
   ```text
   C:\Users\Admin\.gemini\antigravity\scratch\android-quick-translator
   ```
3. Chờ Android Studio đồng bộ xong (Sync Project).
4. Vào thanh menu trên cùng: **Build** ➔ **Build Bundle(s) / APK(s)** ➔ **Build APK(s)**.
5. Sau 1 phút, thông báo hoàn tất sẽ hiện ra: Bấm vào chữ **locate** để mở thư mục chứa file:
   ```text
   app/build/outputs/apk/debug/app-debug.apk
   ```
6. Gửi file `app-debug.apk` này sang điện thoại (qua Zalo, Telegram, hoặc cáp sạc) để cài đặt.

---

## ⚙️ Hướng dẫn cài đặt và sử dụng trên điện thoại

1. **Cài đặt file APK**:
   - Bấm vào file `.apk` vừa tải về trên điện thoại.
   - Nếu điện thoại hiện thông báo bảo mật: Bấm **Cài đặt** (hoặc gạt cho phép *"Cài đặt từ nguồn không xác định"*).
2. **Khởi động lần đầu**:
   - Mở ứng dụng **Quick Translator** lên một lần để Android ghi nhận tính năng dịch vào menu hệ thống.
3. **Thử nghiệm tính năng bôi đen dịch**:
   - Mở trình duyệt Chrome trên điện thoại, vào một trang web tiếng Anh bất kỳ (ví dụ `bbc.com` hoặc `wikipedia.org`).
   - Dùng ngón tay chạm giữ để **bôi đen một câu hoặc một từ tiếng Anh**.
   - Trên thanh menu hiện ra cạnh ngón tay, bạn bấm vào **"Dịch sang tiếng Việt"** (nếu nhiều mục quá, bấm dấu 3 chấm `⋮` để chọn).
   - Thẻ dịch nổi sẽ xuất hiện ngay lập tức!

---

## 📁 Cấu trúc mã nguồn ứng dụng

```text
android-quick-translator/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml                  # Đăng ký quyền Internet & bộ lọc PROCESS_TEXT
│   │   ├── java/com/quicktranslator/app/
│   │   │   ├── MainActivity.kt                  # Màn hình chính & khung dịch trực tiếp
│   │   │   ├── ProcessTextActivity.kt           # Xử lý thẻ dịch nổi khi bôi đen chữ
│   │   │   ├── TranslationService.kt            # Xử lý kết nối API Google Translate
│   │   │   └── TTSHelper.kt                     # Phát âm Text-to-Speech chuẩn tiếng Anh
│   │   └── res/
│   │       ├── layout/
│   │       │   ├── activity_main.xml            # Giao diện màn hình chính
│   │       │   └── dialog_process_text.xml      # Giao diện thẻ dịch nổi
│   │       ├── values/ (colors, strings, themes)
│   │       └── drawable/ (icons, shapes)
├── .github/workflows/build-apk.yml               # Quy trình tự động xuất APK trên GitHub
└── README.md
```
