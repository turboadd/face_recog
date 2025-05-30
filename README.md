👁️ CCTV Face Recognition System with Python

-----
Table of Contents

    About the Project
    Features
    Technologies Used
    Getting Started
        Prerequisites
        Installation
    Usage
    Project Structure
    Configuration
    Roadmap
    Contributing
    License
    Contact

About the Project

โปรเจกต์นี้มีวัตถุประสงค์เพื่อพัฒนาระบบรู้จำใบหน้าแบบเรียลไทม์จากกล้องวงจรปิด (CCTV) โดยใช้ Python และไลบรารี OpenCV ร่วมกับ face_recognition (หรือ YOLO ถ้าเลือกใช้ในอนาคต) ระบบนี้จะสามารถตรวจจับและระบุบุคคลที่รู้จักได้ พร้อมทั้งแจ้งเตือนเมื่อพบใบหน้าที่ไม่รู้จักหรือไม่ได้รับอนุญาต เหมาะสำหรับใช้ในการรักษาความปลอดภัย, การควบคุมการเข้าถึง, หรือการตรวจสอบบุคคลในพื้นที่ที่กำหนด

Features

    Real-time Face Detection: ตรวจจับใบหน้าในวิดีโอสตรีมจากกล้องวงจรปิดได้อย่างรวดเร็ว
    Face Recognition: รู้จำใบหน้าที่รู้จักจากฐานข้อมูล
    "Unknown" Face Identification: ระบุใบหน้าที่ไม่รู้จักและแสดงผล
    Alerting System (Planned): ระบบแจ้งเตือนเมื่อพบใบหน้าที่ไม่รู้จัก (เช่น ส่งอีเมล, Line Notify)
    Recording (Planned): บันทึกภาพนิ่งหรือวิดีโอคลิปเมื่อตรวจพบใบหน้า
    Scalable: ออกแบบให้สามารถปรับขนาดและเพิ่มฟังก์ชันได้ง่าย

Technologies Used

    Python 3.x
    OpenCV - สำหรับการประมวลผลภาพและวิดีโอ
    face_recognition - สำหรับ Face Detection และ Face Recognition (หรือ YOLOvX สำหรับ Object Detection ถ้าเลือกใช้ในภายหลัง)
    dlib - ไลบรารีพื้นฐานที่ face_recognition ใช้
    numpy - สำหรับการคำนวณทางคณิตศาสตร์
    imutils - สำหรับการประมวลผลภาพพื้นฐาน (ถ้าใช้)

Getting Started

ทำตามขั้นตอนด้านล่างเพื่อตั้งค่าและรันโปรเจกต์บนเครื่องของคุณ
Prerequisites

ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Python 3.x ไว้แล้ว
Installation

    Clone the repository:
    Bash

git clone https://github.com/YourUsername/cctv-face-recognition.git
cd cctv-face-recognition

Create a virtual environment (recommended):
Bash

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

Install the required libraries:
Bash

    pip install -r requirements.txt

    (ถ้ายังไม่มีไฟล์ requirements.txt ให้สร้างขึ้นมาจากการรัน pip freeze > requirements.txt หลังจากติดตั้งทุกอย่างแล้ว)

Usage

    เตรียมฐานข้อมูลใบหน้าที่รู้จัก:
        วางรูปภาพของบุคคลที่คุณต้องการให้ระบบรู้จักไว้ในโฟลเดอร์ known_faces/
        ตั้งชื่อไฟล์รูปภาพตามชื่อของบุคคลนั้น ๆ (เช่น known_faces/John_Doe.jpg, known_faces/Jane_Smith.png)

    เข้ารหัสใบหน้าที่รู้จัก:
    รันสคริปต์ face_encoder.py เพื่อประมวลผลรูปภาพและสร้างไฟล์ encoding:
    Bash

python face_encoder.py

ไฟล์ known_face_encodings.pkl (หรือชื่ออื่นที่คุณตั้ง) จะถูกสร้างขึ้นในโฟลเดอร์ data/

กำหนดค่ากล้องวงจรปิด:
แก้ไขไฟล์ config.py และระบุ URL ของ RTSP stream จากกล้องวงจรปิดของคุณ:
Python

# config.py
CCTV_STREAM_URL = "rtsp://user:password@ip_address:port/stream"

สำคัญ: อย่าลืมเปลี่ยน user:password@ip_address:port/stream ให้เป็นข้อมูลกล้องของคุณจริง ๆ

รันระบบ:
Bash

    python main.py

    หน้าต่างแสดงผลจะปรากฏขึ้น แสดงวิดีโอจากกล้องพร้อมกรอบใบหน้าและชื่อที่ระบุได้

Project Structure

cctv-face-recognition/
├── main.py                     # สคริปต์หลักสำหรับรันระบบรู้จำใบหน้า
├── face_encoder.py             # สคริปต์สำหรับเข้ารหัสใบหน้าที่รู้จัก
├── known_faces/                # โฟลเดอร์เก็บรูปภาพบุคคลที่รู้จัก
│   ├── somchai.jpg
│   └── somsri.png
├── data/                       # โฟลเดอร์สำหรับเก็บข้อมูลที่เกี่ยวข้อง
│   └── known_face_encodings.pkl # ไฟล์เก็บ encoding ของใบหน้าที่รู้จัก
├── logs/                       # โฟลเดอร์สำหรับเก็บไฟล์ log (ถ้ามี)
├── captured_unknown_faces/     # โฟลเดอร์สำหรับเก็บภาพใบหน้าที่ไม่รู้จัก (ถ้ามีการแจ้งเตือน)
├── config.py                   # ไฟล์สำหรับเก็บการตั้งค่าต่างๆ (URL กล้อง, thresholds)
├── requirements.txt            # รายการไลบรารีที่จำเป็น
└── README.md                   # ไฟล์อธิบายโปรเจกต์นี้

Configuration

คุณสามารถปรับแต่งการตั้งค่าบางอย่างได้ในไฟล์ config.py:

    CCTV_STREAM_URL: URL ของ RTSP stream กล้องวงจรปิด
    TOLERANCE: เกณฑ์ความคล้ายคลึงในการรู้จำใบหน้า (ค่าเริ่มต้น 0.6 ยิ่งน้อยยิ่งเข้มงวด)
    PROCESS_EVERY_N_FRAMES: ประมวลผลทุกๆ N เฟรมเพื่อประสิทธิภาพ (เช่น 5 เพื่อประมวลผลทุกๆ 5 เฟรม)

Roadmap

นี่คือแผนการพัฒนาสำหรับฟังก์ชันในอนาคต:

    [ ] Implement Alerting System (Email, Line Notify, Telegram) for unknown faces.
    [ ] Add Logging functionality to track detections and events.
    [ ] Develop a simple GUI (e.g., using Tkinter/PyQt/Streamlit) for better user interaction.
    [ ] Explore using YOLO for more robust and faster face detection.
    [ ] Implement Database integration (e.g., SQLite) for storing attendance logs.
    [ ] Enhance performance with multithreading for video stream reading and processing.

Contributing

ยินดีรับฟังทุกข้อเสนอแนะและการมีส่วนร่วม! หากคุณต้องการช่วยพัฒนาโปรเจกต์นี้:

    Fork โปรเจกต์นี้
    สร้าง Branch ใหม่ของคุณ (git checkout -b feature/AmazingFeature)
    Commit การเปลี่ยนแปลงของคุณ (git commit -m 'Add some AmazingFeature')
    Push ไปยัง Branch (git push origin feature/AmazingFeature)
    เปิด Pull Request

License

โปรเจกต์นี้อยู่ภายใต้ MIT License. ดูไฟล์ LICENSE สำหรับรายละเอียดเพิ่มเติม
Contact

Your Name - your.email@example.com

Project Link: https://github.com/YourUsername/cctv-face-recognition