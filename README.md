🔐 Secure QR Code Scanner

A simple and secure QR code generator and decoder tool built using Python. This project allows you to:
Take user input and generate a QR code.
Decode the QR code on demand to retrieve the original encoded data.


📌 Features
✅ Encode text into a QR code.
✅ Save the QR code as an image file.
✅ Decode QR codes from images using OpenCV and Pyzbar.
✅ Clean, secure, and easy-to-use interface.

🛠️ Installation
Before running the project, ensure the following dependencies are installed.

📦 Install Required Libraries
Run the following commands in order:
!apt-get install libzbar0
!pip install pyzbar opencv-python
!pip install qrcode[pil]
🔍 Note: The first command installs a system-level dependency required for pyzbar to function properly.


🚀 How to Use
🧪 Preferred: Run on Google Colab
Open Google Colab
Create a new notebook or open the provided one.

Install Dependencies
Run this in a code cell:

!apt-get install libzbar0
!pip install pyzbar opencv-python
!pip install qrcode[pil]
Run the Code
Enter your text when prompted to generate a QR code.
View the generated image directly in Colab.
Decode the QR code to retrieve the original text.
✅ Google Colab is highly recommended to avoid any local environment issues.
Encode input to generate and save a QR code.
Choose to decode it whenever required.




📂 Project Structure
secure-qr-code-scanner/
├── qr_scanner.py       # Main script to generate and decode QR codes
├── README.md           # Project documentation
└── qr_code.png         # (Generated) QR code image

🔐 Security Considerations
All QR generation and decoding happens locally or within a secure Colab session.
No external API or third-party service is used—your data stays with you.

🧑‍💻 Author
Md Ziaur Rahman
