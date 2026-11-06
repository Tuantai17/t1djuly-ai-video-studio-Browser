# Sesame Studio — Mã nguồn tái tạo hoàn chỉnh (100% Full Source)

Dự án này được giải nén và tái tạo hoàn chỉnh từ bộ cài đặt gốc `Sesame-Studio-Setup-1.0.0.exe`, giữ nguyên **100% toàn bộ chức năng**, cấu trúc logic, giao diện, các module backend và các công cụ thực thi đi kèm.

---

## 🏗️ Cấu trúc thư mục dự án

```text
sesame-studio/
├── main.js                  # Electron Main Process (quản lý cửa sổ, IPC, khởi động CRM server)
├── preload.js               # IPC ContextBridge kết nối giữa Main Process và Renderer UI
├── package.json             # Cấu hình dự án, script dev và script đóng gói electron-builder
├── bin/                     # Các công cụ nhị phân portable đi kèm
│   ├── ffmpeg.exe           # FFmpeg v8.1.3 (xử lý cắt ghép, trích xuất audio/video)
│   ├── ffprobe.exe          # Phân tích thông số media, stream, bitrate
│   ├── yt-dlp.exe           # Tải video từ YouTube / TikTok / nền tảng xã hội
│   ├── deno.exe             # Deno runtime v2.9.4
│   └── *.dll                # Các thư viện liên kết động cho FFmpeg
├── engine/                  # Toàn bộ logic nghiệp vụ backend
│   ├── chrome.js            # Tự động hóa Google Chrome qua DevTools Protocol (CDP) pipe
│   ├── dola-runner.js       # Tự động hóa tạo video trên Dola AI
│   ├── gflow-runner.js      # Tự động hóa tạo video trên Google Flow
│   ├── seedance-runner.js   # Tự động hóa BytePlus Seedance
│   ├── muse-runner.js       # Tự động hóa Muse AI
│   ├── facebook-poster.js   # Đăng video lên Facebook Reels qua Graph API v20.0
│   ├── crm-server.js        # Local REST API Server (port 48900) quản lý hàng đợi task
│   ├── merge.js             # Thuật toán ghép video và xử lý timeline
│   ├── edge_tts_cli.py      # Script Python gọi Edge TTS lồng tiếng
│   ├── vieneu-tts.js        # Tích hợp model giọng đọc VieNeu AI
│   ├── drama-compiler.js    # Trình biên dịch kịch bản & phân cảnh
│   └── toolkit/             # Các công cụ tiện ích bổ trợ
└── ui/                      # Toàn bộ giao diện người dùng (HTML, CSS, JS)
    ├── index.html           # Khung giao diện chính
    ├── nger-features.css    # Phong cách Dark Theme
    ├── studio.js            # Giao diện Studio & hàng đợi render
    ├── edit.js              # Giao diện Timeline Edit / Ghép video
    ├── fb.js                # Giao diện đăng Facebook Reels
    ├── script.js            # Giao diện soạn kịch bản
    └── assets/              # Icon, hình ảnh, phông chữ Be Vietnam Pro
```

---

## 🚀 Cách chạy và phát triển

### 1. Cài đặt môi trường phát triển
Cần cài đặt **Node.js** (khuyến nghị phiên bản 20 trở lên).

Tại thư mục `e:\creator-skill-buildCode\t1djuly-studio`, mở Terminal / PowerShell và chạy:
```bash
npm install
```

### 2. Khởi chạy ứng dụng ở chế độ Live Dev
```bash
npm start
# hoặc
npm run dev
```

### 3. Đóng gói ra file `.exe` mới (Installer)
Sau khi tùy biến hoặc chỉnh sửa tính năng, bạn có thể build lại file cài đặt Windows bất cứ lúc nào:
```bash
npm run dist
```
File cài đặt mới sẽ được tạo trong thư mục `dist/`.

---

## 🌟 Tất cả các chức năng được bảo toàn nguyên vẹn
1. **Studio AI Render**: Tự động hóa tạo video qua Dola, Google Flow, Muse AI, Seedance.
2. **Kịch bản & Phân cảnh**: Trình biên dịch phân tích kịch bản nhiều shot.
3. **Prompt đồng bộ**: Giữ cố định ngoại hình nhân vật, góc máy, ánh sáng.
4. **Edit / Ghép video**: Timeline đa lớp, cắt tỉa, bộ lọc màu, làm mờ sub, chèn watermark.
5. **Cắt video siêu tốc**: Cắt theo thời lượng, chia đều hoặc tự động dò chuyển cảnh (*Stream Copy*).
6. **Lồng tiếng AI (TTS)**: Đọc từ subtitle `.srt` bằng Microsoft Edge TTS / Google TTS.
7. **Đăng Reels Facebook**: Quét danh sách Fanpage và xuất bản video 9:16 tự động.
