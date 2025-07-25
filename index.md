# 🛡️ DinoMind Security: Your Trust, Secured

Welcome to the **DinoMind security and transparency page**.  
We believe that when it comes to your most sensitive data, trust isn't given — it's **earned through transparency** and a relentless commitment to security.  
This document explains in clear terms how **DinoVault** is engineered to protect your digital life.

---

## 🔐 Zero-Knowledge Security

Our core principle is **Zero-Knowledge Security**.  
This means we, the developers of DinoMind, can **never see, access, or decrypt your stored information**.  
Your data is **yours and yours alone**.

---

## 🔑 The Heart of DinoVault: Your Master Password

Your **Master Password** is the single most important piece of information for your vault.  
It is the **one and only key** to your data.

- **It's Never Stored, Never Sent:**  
  We do **not store your Master Password** on your device or our servers.  
  It exists **only in your memory**.  
  This means we can never access it, and we also **cannot recover it** for you if you forget it.  
  This is a **critical security feature** that guarantees **only you** can open your vault.

- **How We Verify Your Password Without Storing It (Hashing):**  
  When you create your Master Password, we don't save the password itself.  
  Instead, we use a **one-way cryptographic function** called **PBKDF2-SHA256** to create a unique, irreversible **"hash" or fingerprint** of your password.  
  This hash is **stored on your device**.  
  When you log in, we hash the password you enter and compare it to the stored hash.  
  If they match, the vault unlocks.  
  ✅ This process allows us to **verify you are the correct user** without ever needing to see or store your actual password.

- **Deriving Your Encryption Key (PBKDF2):**  
  This same secure process is used to **generate your vault's unique encryption key**.  
  Your Master Password is combined with a **unique, randomly generated value** called a **salt** (stored on your device) and put through the strong **PBKDF2 algorithm**.  
  This transforms your password into a powerful **256-bit encryption key** that is used to **lock and unlock your data**.

---

## 🧠 The Encryption Engine: XChaCha20-Poly1305

Once your unique encryption key is derived, DinoVault uses it to **lock down your data**.  
Every single piece of sensitive information — every password, card number, PIN, and custom field — is **encrypted individually** on your device **before it's ever saved**.

DinoVault uses the **XChaCha20-Poly1305** authenticated encryption cipher.  
While the name is complex, its benefits are simple and powerful:

- **Modern and Secure:**  
  It is a **state-of-the-art encryption algorithm** recommended by leading security experts (including Google) for its **high performance** and **robust security** against a wide range of cryptographic attacks.

- **Authenticated Encryption:**  
  It doesn't just encrypt your data; it also **authenticates** it.  
  This means it protects against attempts to **tamper with or modify your encrypted data** without your knowledge.

🔐 Because of this **on-device encryption**, the data stored in the DinoMind database is **completely unreadable** to anyone or any app **without your Master Password**.

---

## 🧩 Smart In-Memory Protection

Security doesn't stop once data is stored.  
How an app **handles information while you're using it** is just as important.

- **The Vault Session Manager:**  
  When you unlock DinoVault, your encryption key is held **temporarily and securely in your device's memory** by our `VaultSessionManager`.  
  This allows you to access your items without re-entering your password every time.

- **Automatic Lock & Memory Wipe:**  
  This session is **not permanent**.  
  The `VaultSessionManager` is designed to **automatically lock** the vault and **securely wipe** the encryption key from memory after a period of inactivity (**5 minutes**).  
  This ensures that if you forget to close the app, your data is automatically protected.

- **Secure Caching:**  
  To provide a smooth experience, decrypted passwords and cards are held in a **temporary in-memory cache**:
  - `DecryptedPasswordCache`
  - `DecryptedCardsCache`  
  This cache is **immediately and securely cleared** the moment your vault session ends, ensuring **no decrypted data is left behind**.

- **Explicit Memory Cleaning:**  
  Throughout the code, we **proactively "zero out" or wipe sensitive information** (like passwords and encryption keys) from memory as soon as it is no longer needed, **minimizing exposure time**.

---

## 📱 Platform and Application Security Features

DinoVault includes several features you can see and interact with, all designed to add **layers of protection**:

- **Screenshot & Screen Recording Prevention:**  
  On all sensitive screens within DinoVault, we enable Android’s `FLAG_SECURE`.  
  This system-level feature blocks anyone (including you and other apps) from taking screenshots or recording the screen.

- **Secure Clipboard:**  
  When you copy a password or card number, our `ClipboardUtils` feature **automatically clears** that information from your device’s clipboard after **60 seconds**.  
  This prevents sensitive data from being accidentally pasted into the wrong place.

- **Brute-Force Protection:**  
  To prevent attackers from guessing your password, the `LockoutTimerManager` **tracks failed login attempts**.  
  After **10 incorrect tries**, the vault will lock for an **exponentially increasing amount of time**.

- **Secure Data Export & Import:**  
  The **"Export Vault"** feature is also designed with security as the top priority.  
  Your data is:
  1. First **decrypted in memory**
  2. Then **re-encrypted** with your Master Password using the **same powerful XChaCha20-Poly1305 cipher**
  3. Then saved to a file  
  ✅ This ensures your backup file is **just as secure** as your vault itself.

---

## 🤝 Our Security Promise

To build your trust, we make these commitments:

### ✅ We DO:
- Encrypt **every piece** of your sensitive data on your device.
- Use **modern, peer-reviewed**, and **industry-standard** cryptographic algorithms.
- Give **you, and only you**, control over your data.

### ❌ We DO NOT:
- Store or transmit your **Master Password**.
- Store or transmit your **unencrypted vault data**.
- Sell or share **any of your personal information**.

---

## 🧬 Final Word

Your **privacy and security** are the foundation of **DinoMind**.  
We are dedicated to protecting your digital life.

If you have any further questions, please don’t hesitate to contact us at:

📧 <thelaughingdinosaurhere@gmail.com>
