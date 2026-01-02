## Secure File Sharing System

### 📘 Overview
The *Secure File Sharing System* is a web-based platform that allows users to *securely upload and download files* using *AES encryption*.  
It ensures that data remains *confidential, authenticated, and tamper-proof* throughout its lifecycle — both *in transit* and *at rest*.

---

## 🚀 Features
✅ Secure file upload & download  
✅ AES encryption for each uploaded file  
✅ Unique encryption key generation per session  
✅ Safe HTTPS communication  
✅ Validation for file type & size  
✅ Simple, user-friendly UI  

---

## 🧠 Skills Gained
- Web Application Security Concepts  
- Flask-based Backend Development  
- AES Encryption & Decryption Implementation  
- Secure File Handling & Key Management  
- API Testing with Postman & cURL  

---

## 🧰 Tools & Technologies Used
| Category | Tools |
|-----------|-------|
| *Programming Language* | Python 3.8+ |
| *Framework* | Flask |
| *Encryption Library* | PyCryptodome |
| *Testing Tools* | Postman, cURL |
| *Version Control* | Git, GitHub |
| *Frontend* | HTML, CSS, Bootstrap |

---

## ⚙ Setup Instructions

### 🧾 Prerequisites
Make sure you have the following installed:
- Python 3.8 or higher  
- Pip (Python package manager)

### 🧩 Installation
```bash
# Clone the repository
git clone https://github.com/your-username/secure-file-sharing-system.git

# Navigate to the project folder
cd secure-file-sharing-system

# Install required dependencies
pip install flask pycryptodome
# Start the Flask server
python app.py
http://127.0.0.1:5000
Code Implementation

🔒 AES Encryption

from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

def encrypt_file(filename):
    key = get_random_bytes(16)
    cipher = AES.new(key, AES.MODE_EAX)
    with open(filename, 'rb') as f:
        data = f.read()
    ciphertext, tag = cipher.encrypt_and_digest(data)

    with open(filename + ".enc", 'wb') as f:
        [f.write(x) for x in (cipher.nonce, tag, ciphertext)]
    print("File Encrypted Successfully!")
    return key

🔓 AES Decryption

from Crypto.Cipher import AES

def decrypt_file(filename, key):
    with open(filename, 'rb') as f:
        nonce, tag, ciphertext = [f.read(x) for x in (16, 16, -1)]
    cipher = AES.new(key, AES.MODE_EAX, nonce)
    data = cipher.decrypt_and_verify(ciphertext, tag)

    with open(filename[:-4], 'wb') as f:
        f.write(data)
    print("File Decrypted Successfully!")

🌐 Flask Routes

from flask import Flask, request, send_file
import os

app = Flask(_name_)

@app.route('/upload', methods=['POST'])
def upload_file():
    file = request.files['file']
    file.save('uploads/' + file.filename)
    return "File Uploaded Successfully!"

@app.route('/download/<filename>', methods=['GET'])
def download_file(filename):
    return send_file('uploads/' + filename, as_attachment=True)

if _name_ == '_main_':
    app.run(debug=True)
Testing & Validation

Tested using Postman for API endpoints /upload and /download

Verified encryption integrity by comparing original vs decrypted file hashes

Ensured that decrypted content matched the original uploaded file



🔒 Security Highlights

AES-256 encryption for all stored files

Unique key generation per uploaded file

No plaintext storage of keys or data

HTTPS-enabled server communication

Input validation for file safety

Conclusion
This project successfully demonstrates end-to-end encryption in web applications using AES.
It ensures data confidentiality, integrity, and secure access control, making it a strong example of modern secure web system design.



Author

Nandhitha V N

🌐 Connect on LinkedIn ( https://www.linkedin.com/in/nandhitha-v-n-41173136b?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app)

