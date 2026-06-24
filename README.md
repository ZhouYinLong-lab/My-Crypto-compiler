# My Crypto Compiler

[![Blog](https://img.shields.io/badge/Blog-Read%20the%20Article-orange?style=for-the-badge)](https://zylatent.com/blog/my-compile/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Web Crypto API](https://img.shields.io/badge/Web%20Crypto-AES--256--GCM-green?style=for-the-badge)](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
[![Frontend Only](https://img.shields.io/badge/Frontend-Only-blue?style=for-the-badge)](#)

A browser-based natural-language encryption experiment that combines **AES-256-GCM**, **PBKDF2 key derivation**, **BigInt conversion**, and a customizable **Base-N character dictionary**.

The project can transform ordinary plaintext into a seemingly random sequence made only from user-defined characters, such as:


哈基米哈哈米基米哈米米……

It is designed as a lightweight pure-frontend cryptographic toy / interactive web experiment.

Related article: 自然语言加密器：自定义 Base-N 文本隐写实验

Features
Pure frontend implementation
No backend, database, or server-side storage
AES-256-GCM encryption through the browser Web Crypto API
PBKDF2-based key derivation
Random salt and IV generation for each encryption
BigInt-based binary-to-number conversion
Custom Base-N encoding with user-defined characters
Supports arbitrary natural-language plaintext
Supports custom disguise dictionaries such as 哈基米, 喵呜, 芝士雪豹, etc.
Cyber-terminal style interface
How It Works

The tool follows a simple pipeline:

Plaintext
   ↓
Password + PBKDF2
   ↓
AES-256-GCM Encryption
   ↓
Salt + IV + Ciphertext Packing
   ↓
Uint8Array → BigInt
   ↓
Custom Base-N Encoding
   ↓
Disguised Ciphertext

During decryption, the process is reversed:

Disguised Ciphertext
   ↓
Custom Base-N Decoding
   ↓
BigInt → Uint8Array
   ↓
Extract Salt / IV / Ciphertext
   ↓
AES-256-GCM Decryption
   ↓
Plaintext
Usage
1. Open the Project

Clone this repository:

git clone https://github.com/ZhouYinLong-lab/My-Crypto-compiler.git
cd My-Crypto-compiler

Then open index.html directly in a modern browser.

No installation is required.

2. Set the Shared Protocol

Both sender and receiver must use exactly the same:

Shared password
Custom dictionary

Example dictionary:

哈基米

This creates a Base-3 encoding system where every encrypted message is represented only by these three characters.

Rules for the dictionary:

Length should be between 2 and 16 characters
Characters should not repeat
Sender and receiver must use the exact same dictionary
3. Encrypt a Message
Enter the shared password.
Enter the custom dictionary.
Type the plaintext message in the encryption area.
Click 生成密文.
Copy the generated disguised ciphertext.
4. Decrypt a Message
Paste the disguised ciphertext into the decryption area.
Enter the same shared password.
Enter the same custom dictionary.
Click 还原明文.
The original plaintext will appear in the output area.
Project Structure
My-Crypto-compiler/
├── index.html   # Main page structure
├── style.css    # Cyber-terminal visual design
└── app.js       # Encryption, decryption, Base-N encoding, and UI logic
Core Implementation
Encryption Layer

The project uses the browser-native Web Crypto API:

PBKDF2 for deriving an encryption key from the password
AES-GCM with 256-bit key length for encryption and authentication
Random 16-byte salt
Random 12-byte IV

The encrypted payload is packed as:

salt + iv + ciphertext
BigInt Conversion

Because encrypted binary data can be much larger than ordinary JavaScript numbers, the project converts the byte array into a BigInt.

A sentinel byte is added before conversion to prevent leading zero loss during encoding and decoding.

Custom Base-N Encoding

The user-defined dictionary is treated as a numeral system.

For example:

Dictionary: 哈基米
Base: 3

The encrypted BigInt is repeatedly divided by the dictionary length, and each remainder is mapped to a character from the dictionary.

This produces ciphertext that looks like natural-language nonsense while still being reversible.

Security Notes

This project uses real browser cryptography primitives, but it should be treated as an educational and experimental tool.

Please note:

Security depends heavily on the strength of the shared password.
The password should be exchanged through a secure channel.
Losing or changing the dictionary makes decryption impossible.
The same dictionary and password must be used for both encryption and decryption.
This project has not undergone professional cryptographic audit.
Do not rely on it for high-risk or legally sensitive communication.
Browser Compatibility

A modern browser with support for the Web Crypto API is required.

Recommended browsers:

Chrome
Edge
Firefox
Safari
Development

Since this is a static frontend project, you can edit and preview it directly.

For local development, you may also use a lightweight static server:

python -m http.server 8000

Then visit:

http://localhost:8000
Possible Improvements
Add export / import for encrypted messages
Add dictionary validation hints
Add password strength indicator
Add copy-to-clipboard button
Add mobile layout optimization
Add example presets for common disguise dictionaries
Add unit tests for Base-N encode / decode logic
Add deployment through GitHub Pages
License

No license has been specified yet.

Consider adding a license file such as MIT, Apache-2.0, or GPL-3.0 if you want others to reuse or modify this project clearly.

Author

Created by ZhouYinLong-lab.

Blog: 寒柳别苑
