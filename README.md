# 🔐 Advanced System Verification (Windows)

> ⚠️ **Important Notice:** This project is **NOT an antivirus**.

---

## 📌 About the Project

This is a `.bat` script developed as a **quick security workaround** for Windows.

It was created after **3 consecutive days trying to remove a trojan** that infected my machine.  
During this process, I gathered useful commands, techniques, and tools — and this script is basically a **compilation of those solutions**.

> 💡 In other words: this is emergency support, **not a permanent solution**.

---

## 🛠️ What the Script Does

- Terminates common suspicious processes  
- Restores the HOSTS file  
- Checks and repairs disk errors  
- Verifies system integrity (SFC)  
- Analyzes startup entries  
- Detects persistence:  
  - Registry (Run)  
  - Scheduled tasks  
  - Services  
- Runs heuristic analysis:  
  - Hidden files  
  - Executables in suspicious locations  
- Removes suspicious files from:  
  - Temp  
  - Public  
- Lists suspicious files in AppData (without deleting)  
- (Optional) Checks digital signatures with Sigcheck  

---

## ⚠️ Limitations

- ❌ Does not replace antivirus software  
- ❌ Does not detect all threats  
- ❌ May produce false positives  
- ❌ No real-time protection  

---

## 🔧 How to Use

1. Download the `.bat` file  
2. Right-click  
3. Run as **Administrator**  

---

## 🔐 About Sigcheck (Optional)

For more thorough digital signature verification:

1. Download from:  
   https://learn.microsoft.com/sysinternals/downloads/sigcheck  

2. Place `sigcheck.exe` in the same folder as the script  
   or add it to the Windows PATH  

---

## 📄 Output

The script generates a report at:  
`Desktop\security_report.txt`  

---

## ⚠️ Disclaimer

This script is made for **educational purposes and personal support**.

Use at your own risk.  

---

## 👨‍💻 Author

**Marcelo P**  
🔗 https://github.com/MpasPrime  

---

## 💬 Final Notes

This project was not born as a product — it was born out of necessity.

If it helps you, that’s already worth it 👍
