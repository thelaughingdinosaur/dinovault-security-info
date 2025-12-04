# DinoMind Security Overview

## Transparency, Trust, and Zero-Knowledge Protection

DinoMind is built on a simple philosophy: your data belongs to you—only you. Our responsibility is to protect it using open, transparent, and industry-standard security practices. Whether you choose to keep your data offline on your device or enable Cloud Sync to access it across multiple devices, the foundations of DinoVault remain the same: strong encryption, strict zero-knowledge architecture, and complete user control.

---

# 1. Zero-Knowledge Security

Zero-Knowledge means that DinoMind has no access to your decrypted Vault data or your master password. All encryption and decryption happen exclusively on your device.

### Local Storage

* Vault data never leaves your device.
* No cloud connection is used for storage or syncing.

### Cloud Sync

* All Vault data is encrypted locally on your device before syncing.
* Firebase stores only encrypted text—never readable information.
* Even in a server breach scenario, attackers would only see unusable encrypted data.

DinoMind cannot decrypt your data, reset your password, or retrieve your master password. The encryption key is derived from your password and never transmitted to our servers.

---

# 2. The Master Password

Your master password is the single key that unlocks your vault.

### Key Principles

* It is never stored in plaintext.
* It is never transmitted over the network.
* It is impossible for us to recover if forgotten.

### Secure Verification

To enable multi-device access, DinoMind uses a one-way verification method:

1. Your master password is processed locally through PBKDF2-SHA256.
2. A unique, randomly generated salt ensures every user has a distinct hash.
3. The result is a non-reversible hash used only for verifying future login attempts.
4. Only the salt and hash are stored in Firebase for cross-device verification.
5. The actual password is never exposed or stored.

### Key Derivation

Your encryption key is created by combining your password with the stored salt using PBKDF2-SHA256 (100,000 iterations).
The result is a strong 256-bit key used to encrypt and decrypt vault data entirely on your device.

---

# 3. DinoVault Architecture

DinoVault is divided into two layers:

### 1. Encrypted Zone (Passwords and Cards)

* All sensitive fields are encrypted using XChaCha20-Poly1305.
* Encryption occurs before any data is saved, synced, or transmitted.
* Firebase stores only ciphertext that cannot be reversed without your key.

### 2. Protected Zone (General App Data)

Non-sensitive app features (Ideas, Links, Activities, etc.) are securely stored using Google Firebase Firestore.

* Encrypted transit (HTTPS/TLS) for all network operations.
* Strict Firebase Security Rules ensure only authenticated users can access their data.
* This data does not include any sensitive vault information.

---

# 4. Encryption Technology

DinoVault uses XChaCha20-Poly1305, a modern authenticated encryption cipher recommended by security experts for mobile applications.

### Why XChaCha20-Poly1305

* High resistance to cryptographic attacks.
* High performance on mobile hardware.
* Built-in authentication ensures data integrity and prevents tampering.

If encrypted vault data is ever corrupted or modified, DinoMind detects the tampering and rejects it automatically.

---

# 5. In-Memory Security

How data is handled in RAM is as important as how it is stored.

### Vault Session Manager

* When unlocked, the encryption key is held only in RAM.
* It is removed after a period of inactivity (default: 10 minutes).

### Explicit Memory Cleaning

Wherever possible, DinoMind clears sensitive data from memory immediately after use.
This includes wiping derived keys and clearing password character arrays from RAM.

---

# 6. Device-Level Protections

Several platform features add additional layers of security.

### Screenshot and Screen Recording Protection

Sensitive vault screens enforce Android’s FLAG_SECURE to prevent screenshots, screen recordings, or third-party capture.

### Secure Clipboard

Copied passwords and card details automatically clear from the clipboard after 60 seconds.

### Brute-Force Protection

Failed login attempts are tracked. After multiple incorrect attempts, a lockout timer activates with increasing delay periods to protect against guessing attacks.

---

# 7. Secure Backup, Export, and Import

When exporting your vault:

1. Data is decrypted locally in memory.
2. It is re-encrypted using XChaCha20-Poly1305 with:

   * A fresh random salt
   * A fresh random nonce
   * PBKDF2-derived key
3. The encrypted backup file contains no readable information.

DinoMind cannot decrypt or access your export files. Only your master password can.

---

# 8. Our Commitment

DinoMind is built on trust, transparency, and industry-standard security.
To uphold that:

### We Do

* Encrypt all sensitive data before storage or transmission.
* Use proven, peer-reviewed encryption algorithms.
* Keep all encryption keys in the user’s control.
* Ensure no plaintext vault data touches our servers.

### We Do Not

* Store or transmit your master password.
* Store unencrypted vault data.
* Sell, share, or analyze personal vault information.
* Access, reset, or recover your vault.

---

# Conclusion

Your privacy is the foundation of DinoMind. Whether your vault stays offline on your device or syncs across multiple devices, the system is designed with the same uncompromising principles: zero-knowledge encryption, modern cryptographic standards, and complete user control.

For questions, feedback, or security inquiries, contact:
[thelaughingdinosaurhere@gmail.com](mailto:thelaughingdinosaurhere@gmail.com)
