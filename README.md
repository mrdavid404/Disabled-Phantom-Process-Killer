
# 🧠 Disable Phantom Process Killer on Android 12 / 13  
### ⚙️ The Official “Hacky Way” to Stop Android from Killing Background Processes  

---

## 🔍 What is Phantom Process Killer?

**Phantom Process Killer** is an Android system feature that automatically terminates background “invisible” or “inactive” processes to reduce battery, RAM, and CPU usage.  

This tweak disables that behavior completely — allowing apps like **Termux, Tasker, Shizuku, or background scripts** to run freely without being killed.

---

## 🚫 Disable Commands

You can run these commands using **ADB (PC)** or directly in **A-Shell** on Android.  

### **Command 1**
```bash
/system/bin/device_config set_sync_disabled_for_tests persistent
```

> **Explanation:**  
> `device_config` is Android’s hidden configuration manager.  
> Setting `set_sync_disabled_for_tests persistent` means that test configurations will **remain persistent even after reboot**, ensuring the next values stay saved.

---

### **Command 2 (Main Command)**
```bash
/system/bin/device_config put activity_manager max_phantom_processes 2147483647
```

> **Explanation:**  
> By default, `max_phantom_processes` = **32** (an app can spawn up to 32 child/phantom processes).  
>  
> Setting it to **2147483647** (the maximum 32-bit signed integer) tells the system:
> > “Allow virtually unlimited phantom processes.”  
>
> ✅ This effectively **disables the Phantom Process Killer** trigger.

---

### **Command 3**
```bash
settings put global settings_enable_monitor_phantom_procs false
```

> **Explanation:**  
> When `true` → Android monitors and kills phantom processes.  
> When `false` → Monitoring (and killing) is **completely disabled**.

---

## 🧩 Verify if the Patch Worked

### **Verify Command 1**
```bash
/system/bin/dumpsys activity settings | grep max_phantom_processes
```

> **Output Example:**
> ```
> max_phantom_processes=2147483647
> ```
> If you see this value, the override is successful. ✅

---

### **Verify Command 2**
```bash
/system/bin/device_config get activity_manager max_phantom_processes
```

> **Expected Output:**
> ```
> 2147483647
> ```
> If it returns `32` or any other number → the tweak didn’t apply correctly.

---

## 💡 Notes

- Works perfectly on **Android 12 / 13** (and newer versions supporting `device_config`).  
- Can be executed via **ADB** or **A-Shell** without root (but some ROMs may require elevated permissions).  
- After applying, reboot your device once to ensure persistence.

---

## ⚠️ Disclaimer
Disabling Phantom Process Killer may:
- Increase **battery consumption**  
- Use more **RAM and CPU**  
- Keep background apps running indefinitely  

Use this tweak **only if you understand its impact** or need long-running background tasks (e.g., Termux sessions, automation scripts, etc.).

---

### ✨ Author
**Script by:** _AH SHOWEV_  
**Compatible with:** Android 12 / 13  
**Environment:** A-Shell / ADB

---# Disabled-Phantom-Process-Killer
How to Disable “Phantom Process Killer”..?? 
