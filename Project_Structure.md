inline-defect-inspection/
├── .github/
│   └── workflows/              # CI/CD pipeline (Linting, Docker Build)
├── assets/                     # Sơ đồ kiến trúc & hình ảnh cho README
│   └── architecture_diagram.png
├── config/                     # Quản lý cấu hình (YAML) - Không hardcode
│   ├── camera_config.yaml      # Cấu hình Resolution, FPS, Camera Index
│   ├── model_config.yaml       # Cấu hình Path, Threshold, Anomaly Score Limit
│   └── hardware_config.yaml    # Cấu hình Baudrate Serial, GPIO Pins, Timeout
├── data/                       # Bộ dữ liệu (Thêm vào .gitignore)
│   ├── raw/                    # Ảnh thô chụp từ Webcam (OK & NG)
│   ├── processed/              # Ảnh đã qua tiền xử lý (Resize, Crop)
│   └── calibration/            # Ảnh dùng để INT8 Quantization trong TensorRT
├── deploy/                     # Đóng gói & Triển khai Docker trên Edge
│   ├── Dockerfile.jetson       # Dockerfile tối ưu cho Nvidia Jetson (CUDA/TensorRT)
│   ├── Dockerfile.x86          # Dockerfile cho PC/Laptop (OpenVINO/ONNX Runtime)
│   └── docker-compose.yml      # Khởi chạy AI Service + Fast-API Dashboard
├── models/                     # Quản lý Trọng số & Engine AI
│   ├── raw_weights/            # File gốc sau khi Train: PyTorch (.pt) / TorchScript
│   ├── export/                 # File định dạng trung gian: (.onnx)
│   └── engines/                # File đã Compile chạy Local: TensorRT (.engine)
├── scripts/                    # Scripts tiện ích chạy độc lập
│   ├── capture_dataset.py      # Script chụp nhanh 50-100 ảnh mẫu OK để train
│   ├── export_onnx.py          # Script chuyển đổi PyTorch -> ONNX
│   └── build_tensorrt.py       # Script compile ONNX -> TensorRT Engine (FP16/INT8)
├── src/                        # MÃ NGUỒN CHÍNH (Core Source Code)
│   ├── __init__.py
│   ├── main.py                 # Entry-point: Chạy luồng Real-time chính
│   ├── train/                  # Giai đoạn 1: Training & Fine-tuning Local
│   │   ├── __init__.py
│   │   ├── dataset_loader.py   # Load dataset ảnh OK
│   │   ├── feature_extractor.py# Khởi tạo Pre-trained Backbone (ResNet50)
│   │   └── train_patchcore.py  # Script fit Memory Bank & CoreSet Sampling
│   ├── camera/                 # Quản lý Luồng Video & Capture
│   │   ├── __init__.py
│   │   └── camera_stream.py    # Multi-threading đọc Webcam không gây nghẽn
│   ├── inference/              # Giai đoạn 2: Local Edge Inference (Siêu nhanh)
│   │   ├── __init__.py
│   │   ├── base_engine.py      # Class giao diện chung cho Engine
│   │   ├── trt_engine.py       # Local Inference bằng TensorRT C++/Python API
│   │   └── anomaly_detector.py # Logic tính Anomaly Score & Bounding Box lỗi
│   ├── hardware/               # Giao tiếp Cảm biến & Vi điều khiển
│   │   ├── __init__.py
│   │   └── serial_bridge.py    # Lắng nghe Trigger & Gửi lệnh EJECT qua USB Serial
│   └── utils/                  # Hàm bổ trợ
│       ├── __init__.py
│       ├── image_processing.py # Crop, Normalize, Draw Bounding Box/Heatmap
│       ├── logger.py           # Logging ghi log lỗi & thời gian suy luận
│       └── metrics.py          # Đo đạc Latency (ms), FPS, Memory Usage
├── firmware/                   # Mã nguồn cho Vi điều khiển (Nạp riêng cho ESP32)
│   └── esp32_hardware_controller/
│       └── esp32_hardware_controller.ino # Arduino Code: Đọc ngắt ngắt Cảm biến & Xoay Servo
├── tests/                      # Unit Test cho từng Module
│   ├── test_camera.py
│   ├── test_inference.py
│   └── test_serial.py
├── .gitignore
├── README.md                   # Tài liệu hướng dẫn (Yếu tố thu hút HR/Tech Lead)
└── requirements.txt            # Thư viện Python phụ thuộc
