# 🎬 t1djuly AI Video Studio (Browser Automation & Video Creation)

[![Node.js](https://img.shields.io/badge/Node.js-v20%2B-green.svg)](https://nodejs.org/)
[![Electron](https://img.shields.io/badge/Electron-v33-blue.svg)](https://www.electronjs.org/)
[![License](https://img.shields.io/badge/License-MIT%20%2F%20Custom-orange.svg)](#)

**t1djuly AI Video Studio** là ứng dụng desktop toàn diện xây dựng trên nền tảng **Electron** kết hợp **Chrome DevTools Protocol (CDP)**, cung cấp giải pháp trọn gói từ khâu soạn kịch bản, tự động hóa render video trên các nền tảng AI hàng đầu, biên tập timeline, lồng tiếng AI đa giọng đọc và xuất bản video ngắn tự động.

---

## 🌟 Tính Năng Nổi Bật

1. **🤖 Studio AI Automation (Đa nền tảng)**:
   - Tự động hóa điều khiển trình duyệt Google Chrome thật qua giao thức CDP pipe độc lập.
   - Hỗ trợ render video hàng loạt qua các engine: **Dola AI**, **Google Flow**, **BytePlus Seedance 2.5**, **Muse AI**.
   - Quản lý đa tài khoản với profile trình duyệt và proxy độc lập cho từng tài khoản.

2. **📜 Biên Kịch & Phân Cảnh Thông Minh (Drama Compiler)**:
   - Trình phân tích kịch bản đa phân cảnh (*multi-shot breakdown*).
   - Tự động đồng bộ mô tả ngoại hình nhân vật, góc máy, ánh sáng và bối cảnh (Prompt Synchronization).
   - Tích hợp công cụ tạo Master Prompt tối ưu cho ChatGPT / Claude tiết kiệm credit.

3. **✂️ Biên Tập & Ghép Video Nâng Cao (Timeline Editor)**:
   - Timeline đa lớp (Video, Audio, Subtitle, Watermark).
   - Bộ lọc màu điện ảnh, làm mờ phụ đề cũ (*delogo / blur sub*), chèn logo thương hiệu.
   - Cắt ghép video siêu tốc bằng FFmpeg Stream Copy không cần render lại.

4. **🎙️ Lồng Tiếng AI (Text to Speech - TTS)**:
   - Đọc phụ đề tự động từ file `.srt` hoặc văn bản kịch bản.
   - Hỗ trợ nguồn **Microsoft Edge TTS** và model **VieNeu-TTS v3 Turbo** chất lượng cao (Quỳnh Anh, Thiện Minh, Đức Trí, Mỹ Duyên,...).

5. **🚀 Tự Động Xuất Bản Reels**:
   - Tích hợp Meta Graph API xuất bản video 9:16 trực tiếp lên hệ thống Fanpage Facebook Reels.

---

## 🏗️ Cấu Trúc Thư Mục Dự Án

```text
t1djuly-studio/
├── main.js                  # Electron Main Process (quản lý window, IPC, CRM server)
├── preload.js               # IPC ContextBridge bảo mật giữa Main và Renderer
├── package.json             # Cấu hình dự án, scripts dev và build
├── bin/                     # Bộ công cụ nhị phân portable tích hợp sẵn
│   ├── ffmpeg.exe           # FFmpeg (xử lý media, cắt ghép, trích xuất)
│   ├── ffprobe.exe          # Phân tích thông số audio/video, bitrate
│   ├── yt-dlp.exe           # Tải video tài nguyên từ mạng xã hội
│   ├── deno.exe             # Deno runtime v2.9.4
│   └── *.dll                # Thư viện liên kết động cho FFmpeg
├── engine/                  # Toàn bộ logic nghiệp vụ backend
│   ├── chrome.js            # Tự động hóa Google Chrome qua CDP
│   ├── dola-runner.js       # Engine tự động hóa Dola AI
│   ├── gflow-runner.js      # Engine tự động hóa Google Flow
│   ├── seedance-runner.js   # Engine tự động hóa Seedance
│   ├── muse-runner.js       # Engine tự động hóa Muse AI
│   ├── crm-server.js        # Local REST API Server (port 48900)
│   ├── merge.js             # Thuật toán ghép video và xử lý timeline
│   ├── vieneu-tts.js        # Tích hợp model giọng đọc VieNeu AI
│   ├── edge_tts_cli.py      # Script Python gọi Edge TTS lồng tiếng
│   ├── drama-compiler.js    # Trình biên dịch kịch bản & phân cảnh
│   └── toolkit/             # Các tiện ích bổ trợ cắt ghép, OCR
└── ui/                      # Giao diện người dùng (HTML, CSS, JS)
    ├── index.html           # Khung giao diện chính
    ├── nger-features.css    # Dark Theme & Styles
    ├── studio.js            # Giao diện Studio & hàng đợi render
    ├── edit.js              # Giao diện Timeline Edit / Ghép video
    ├── fb.js                # Giao diện đăng Facebook Reels
    ├── script.js            # Giao diện soạn kịch bản
    └── assets/              # Icon, hình ảnh, phông chữ Be Vietnam Pro
```

---

## 🚀 Hướng Dẫn Cài Đặt & Khởi Chạy

### 1. Yêu cầu hệ thống
- **Hệ điều hành**: Windows 10/11 64-bit.
- **Node.js**: Phiên bản 18+ (khuyến nghị Node 20 hoặc mới hơn).
- **Google Chrome**: Đã cài đặt trên máy để engine tự động hóa trình duyệt.
- **Python**: Phiên bản 3.10+ (cần thiết khi sử dụng tính năng giọng đọc Edge-TTS hoặc VieNeu-TTS).

### 2. Cài đặt các thư viện phụ thuộc
Mở Terminal hoặc PowerShell tại thư mục dự án:
```powershell
cd E:\creator-skill-buildCode\t1djuly-studio
npm install
```

### 3. Khởi chạy ứng dụng (Live Dev)
```powershell
npm start
# hoặc
npm run dev
```
Ứng dụng sẽ mở cửa sổ giao diện chính với độ phân giải `1400x900`, đồng thời kích hoạt Local CRM Server tại cổng `http://localhost:48900`.

### 4. Đóng gói thành file cài đặt Windows (.exe)
Sau khi tùy biến hoặc hoàn thiện tính năng, bạn có thể build bộ cài đặt Windows độc lập:
```powershell
npm run dist
```
File cài đặt sẽ được tạo tự động trong thư mục `dist/`.

---

## ⚙️ Cấu Hình Mặc Định

- **Thư mục xuất video**: `t1djuly-studio/Output-video-save` (có thể tùy chỉnh lại trong tab **Cài đặt**).
- **Profile trình duyệt**: Lưu riêng biệt tại `%APPDATA%\Sesame Studio\profiles\<accountId>` đảm bảo không ảnh hưởng đến trình duyệt Chrome cá nhân.
- **Bật cổng Remote Debugging (Tùy chọn)**:
  ```powershell
  $env:SESAME_DEBUG_PORT="9226"; npm start
  ```

