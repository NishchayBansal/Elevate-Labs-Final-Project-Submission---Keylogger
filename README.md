# Elevate-Labs-Final-Project-Submission---Keylogger

**Keylogger with Encrypted Data Exfiltration**       
Objective: Build a proof-of-concept keylogger that encrypts logs and simulates exfiltration.    

**Tools:** Python, pynput, cryptography, base64     
**Mini Guide:**
a. Capture keystrokes using pynput.     
b. Encrypt data using cryptography.fernet.    
c. Store logs locally with timestamp.       
d. Simulate sending to a remote server (localhost).    
e. Add startup persistence and kill switch.    

![image](https://github.com/user-attachments/assets/9eddcf20-65db-4d5b-a457-fb6a1ee65073)

![image](https://github.com/user-attachments/assets/1787008b-f066-41a7-821b-d97105ae4197)

![image](https://github.com/user-attachments/assets/60fe28d4-6bbe-436a-baa3-fa645d883e95)


**Deliverables: Encrypted Keylogger PoC with Ethical Constraints and Logs**

### 1. **Main Python Script**

**Filename:** `keylogger.py`     
**Contains:**

* Fernet key generation and loading
* Keystroke capture using `pynput`
* AES encryption of logs
* Log writing with timestamps
* Localhost TCP exfiltration using sockets
* Kill switch (`q!exit`)
* Windows startup persistence via registry

### 2. **Generated Key File**

**Filename:** `key.key`    
**Purpose:** Stores the Fernet symmetric encryption key.

### 3. ✅ **Encrypted Log File**

**Filename:** `encrypted_log.txt`    
**Contains:** 
Encrypted, timestamped keystroke entries.    

![image](https://github.com/user-attachments/assets/62caff5a-ddcd-4717-8e44-b33aa052944d)    
These are encrypted keystroke logs, sent from your keylogger to the local server (localhost:4444).


### 4. **Decryption Script (Optional but Recommended)**

**Filename:** `decrypt_logs.py`    
**What it does:** Reads `key.key` and `encrypted_log.txt`, decrypts entries, and displays readable logs.

```python
from cryptography.fernet import Fernet

with open("key.key", "rb") as key_file:
    key = key_file.read()

fernet = Fernet(key)

with open("encrypted_log.txt", "rb") as log_file:
    for line in log_file:
        try:
            decrypted = fernet.decrypt(line.strip()).decode()
            print(decrypted)
        except Exception as e:
            print(f"Failed to decrypt: {e}")
```


