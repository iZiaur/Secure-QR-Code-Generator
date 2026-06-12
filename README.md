<div align="center">

# 🔐 Secure Expiring QR Code Generator

### A Python-based utility to encrypt, generate, and decode time-sensitive QR codes.

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer_Vision-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org/)
[![Cryptography](https://img.shields.io/badge/Cryptography-Fernet-430098?style=for-the-badge&logo=letsencrypt&logoColor=white)](https://cryptography.io/en/latest/)

</div>

---

## 📌 About

This project is a powerful security utility that combines symmetric encryption with QR code generation to create **time-sensitive, encrypted QR codes**. By leveraging the Fernet encryption algorithm, any text data is securely locked behind a generated key and timestamped. Once the designated expiration period elapses, the data becomes invalid and cannot be successfully verified, making this ideal for temporary ticketing, secure access tokens, or sensitive data sharing.

---

## ✨ Features

- **Symmetric Encryption** — Data is heavily encrypted using `cryptography.fernet` before being embedded into the QR code.
- **Time-Bomb Expiration** — Embeds a Unix timestamp; decoded data is automatically rejected if the current time exceeds the expiration limit.
- **Dynamic QR Generation** — Utilizes the `qrcode` library to build scalable, machine-readable matrices.
- **Computer Vision Decoding** — Integrates `cv2` (OpenCV) and `pyzbar` to accurately scan and extract data from the generated image files.
- **No Internet Required** — All cryptographic functions and image processing happen 100% locally.

---

## 🏗️ System Architecture

```mermaid
graph TB
    subgraph Input["📝 User Input"]
        RAW["Raw Data String"]
        TIME["Expiration Minutes"]
    end

    subgraph Crypto["🔐 Cryptography Engine"]
        KEY["Fernet Key"]
        ENC["Encrypted Payload<br/><i>(Data + Timestamp)</i>"]
    end

    subgraph Output["🖼️ Image Processing"]
        QR["QR Code Generator"]
        IMG["expiring_qr_code.png"]
    end

    RAW -->|"Combined"| ENC
    TIME -->|"Converted to Timestamp"| ENC
    KEY -->|"Encrypts"| ENC
    ENC -->|"Encoded"| QR
    QR -->|"Rendered"| IMG
```

---

## 🔄 Request Flow (Verification Process)

```mermaid
sequenceDiagram
    participant U as 👤 User
    participant CV as 👁️ OpenCV / Pyzbar
    participant C as 🔐 Cryptography (Fernet)
    participant T as ⏱️ Time Check

    U->>CV: decode_qr_code("image.png")
    CV->>CV: Read & extract QR string
    CV-->>U: Return encrypted string
    U->>C: verify_qr_code(encrypted_string)
    C->>C: Decrypt using Key
    C-->>T: Yield (Raw Data, Timestamp)
    T->>T: Compare Timestamp vs Current Time
    alt Time > Expiration
        T-->>U: Print: "The QR code has expired."
    else Time <= Expiration
        T-->>U: Print: "Valid. Decrypted Data: [Data]"
    end
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|:---:|:---|:---|
| **Language** | Python 3 | Core scripting and execution |
| **Cryptography** | `cryptography` (Fernet) | Advanced symmetric encryption |
| **Image Encoding**| `qrcode[pil]` | Generating the visual QR matrix |
| **Image Decoding**| `opencv-python`, `pyzbar` | Reading and interpreting QR matrices |

---

## 📂 Project Structure

```text
Secure-QR-Code-Generator/
├── index.py              # Main execution script containing all logic
├── README.md             # Project documentation
└── expiring_qr_code.png  # (Generated dynamically upon script execution)
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- System level library for pyzbar (e.g., `libzbar0` on Linux)

### 1. Install Dependencies
It is highly recommended to run this in a virtual environment or a Google Colab notebook to avoid local dependency conflicts.

```bash
# Linux (Ubuntu/Debian) requirement for Pyzbar:
sudo apt-get install libzbar0

# Install Python packages:
pip install pyzbar opencv-python qrcode[pil] cryptography
```

### 2. Run the Script
```bash
python index.py
```

### 3. Usage Steps
1. The script automatically generates a secure Fernet key.
2. You will be prompted to enter a string: `Enter the data to store in QR:`
3. The script embeds a hardcoded 1-minute expiration timer (configurable in code).
4. `expiring_qr_code.png` is generated and saved in the directory.
5. The script prompts `do you want to decode the qr y/n` — press `y` to test the decryption and expiration validation.

---

## 📄 License

This project is open source and available under the MIT License.

---

<div align="center">

**Built with ❤️ by [Ziaur Rahman](https://github.com/iZiaur)**

</div>
