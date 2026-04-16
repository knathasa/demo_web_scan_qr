📱 HTML5 QR Code Reader (Docker + Nginx HTTPS)

ระบบสแกน QR Code ผ่านเว็บเบราว์เซอร์ที่ออกแบบมาสำหรับการใช้งานบนสมาร์ทโฟน (iOS และ Android) โปรเจกต์นี้มาพร้อมกับการตั้งค่า Docker และ Nginx ที่จำลอง HTTPS (Self-signed SSL) เพื่อให้สามารถทดสอบการเข้าถึงกล้องผ่าน Local / Private Network ได้โดยไม่ถูกเบราว์เซอร์บล็อก

✨ ฟีเจอร์หลัก (Features)

ใช้งานผ่านเบราว์เซอร์ได้ทันที: ไม่ต้องโหลดแอปพลิเคชันเพิ่มเติม

รองรับสมาร์ทโฟน: UI ปรับขนาดอัตโนมัติ (Responsive) ด้วย Tailwind CSS

เน้นกล้องหลัง (Environment Facing): พยายามเรียกใช้กล้องหลังของมือถือเป็นหลัก พร้อมระบบ Fallback สำหรับ iOS

Local HTTPS: มีการตั้งค่า Nginx Reverse Proxy พร้อม SSL เพื่อแก้ปัญหาเบราว์เซอร์บล็อกการเข้าถึงกล้องเมื่อทดสอบผ่าน IP Address ในวง LAN

🛠 เทคโนโลยีที่ใช้ (Tech Stack)

Frontend: HTML5, JavaScript, Tailwind CSS

QR Code Library: html5-qrcode

Infrastructure: Docker, Docker Compose, Nginx


📂 โครงสร้างโฟลเดอร์ (Project Structure)

├── docker-compose.yml    # ไฟล์ตั้งค่า Docker Compose

├── html/

│   └── index.html        # ไฟล์หน้าเว็บแอปพลิเคชัน (Frontend)

├── conf/

│   └── default.conf      # ไฟล์ตั้งค่า Nginx (Redirect HTTP -> HTTPS)

└── certs/                # โฟลเดอร์สำหรับเก็บไฟล์ SSL Certificate


🚀 วิธีการติดตั้งและรันโปรเจกต์ (Installation & Setup)

1. สิ่งที่ต้องมี (Prerequisites)

Docker และ Docker Compose ติดตั้งอยู่ในเครื่อง

OpenSSL (สำหรับสร้าง Self-signed Certificate)

2. สร้าง SSL Certificate

เพื่อให้เบราว์เซอร์อนุญาตให้เข้าถึงกล้องผ่าน IP Address ได้ เราต้องสร้าง SSL Certificate จำลองขึ้นมาก่อน เปิด Terminal ในโฟลเดอร์โปรเจกต์และรันคำสั่ง:

mkdir certs

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout certs/selfsigned.key -out certs/selfsigned.crt -subj "/C=TH/ST=Bangkok/L=Bangkok/O=LocalTest/CN=localhost"


3. เริ่มต้นทำงาน (Run Docker)

รันคำสั่ง Docker Compose เพื่อสร้างและเปิดใช้งาน Nginx Web Server:

docker-compose up -d


📱 วิธีการทดสอบบนสมาร์ทโฟน (Usage)

หา IP Address ของเครื่องคอมพิวเตอร์ที่รัน Docker (เช่น 192.168.1.45)

นำสมาร์ทโฟนเชื่อมต่อ Wi-Fi ให้อยู่ในวง LAN เดียวกัน

เปิดเบราว์เซอร์ (Safari หรือ Chrome) แล้วพิมพ์ URL โดยระบุ https:// และพอร์ต :8443 ต่อท้าย:

[https://192.168.1.45:8443](https://192.168.1.45:8443)


⚠️ ข้อควรระวัง: > เนื่องจากเราใช้ SSL Certificate ที่สร้างขึ้นเอง (Self-signed) เบราว์เซอร์จะขึ้นหน้าจอเตือนว่า "การเชื่อมต่อนี้ไม่เป็นส่วนตัว" (Your connection is not private) > * ให้กดปุ่ม ขั้นสูง (Advanced) แล้วเลือก ไปยัง ... (ไม่ปลอดภัย) / Proceed to ... (unsafe)

หลังจากนั้นคุณจะสามารถกดอนุญาตให้เว็บไซต์เข้าถึงกล้องได้ตามปกติ


🛑 วิธีการปิดระบบ

เมื่อทดสอบเสร็จแล้ว สามารถหยุดและลบคอนเทนเนอร์ได้ด้วยคำสั่ง:

docker-compose down


📄 License

This project is open-source and available under the MIT License.
