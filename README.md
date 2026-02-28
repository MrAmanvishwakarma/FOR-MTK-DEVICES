# FOR-MTK-DEVICES
SP Flash Tool errors and the important warnings and process to install custom ROM and recovery 
I try on Realme 6i RMX2002.

# For Connecting to PC
1. Install MTK driver
2. Install LibUSB driver
3. MtkBypassExe *(recommended)* for connecting in SP Flash Tool

---

# For Unlock Bootloader
1. MTK Client Tool v2.0
2. Before unlocking **and** locking the bootloader: Erase `metadata` and `userdata` (and `md_udc` if existing)

---

# For Fastboot Mode
1. First, unlock the bootloader
2. Open MTK Client Tool v2.0 → **Read** section → Read `lk.bin`
3. Upload `lk.bin` to the [LK Patcher website](https://lkpatcher.r0rt1z2.com/) → Click **Apply All** → Download as `.img`
4. Convert `.img` to `.bin` → you will get `lk-patched.bin`
5. Open MTK Client Tool v2.0 → **Write** section → Select `lk-patched.bin` for both `lk` and `lk2` partitions → Flash
6. Power off the device
7. To enter Fastboot mode: **Hold Power (Home) + Volume Down**

---

# For Flashing Custom Recovery
1. Boot into Fastboot mode using Platform Tools
2. Check unlock status:
   ```
   fastboot getvar unlocked
   ```
   > ⚠️ If it says `no` → you must unlock first

3. Flash recovery:
   ```
   fastboot flash recovery recovery.img
   ```
   > If error: `partition not found` — use:
   ```
   fastboot flash recovery_a recovery.img
   ```

4. Flash vbmeta:
   ```
   fastboot flash vbmeta vbmeta.img
   ```

5. Reboot to recovery:
   ```
   fastboot reboot recovery
   ```
   > When the screen appears, press the **Power (Home)** button

---

# For Flashing Custom ROM
1. Boot into Recovery → go to **ADB Sideload** section → start sideload
2. Connect to PC with Platform Tools and run:
   ```
   adb sideload /path/to/rom.zip
   ```

---

# ⚠️ IMPORTANT THINGS YOU SHOULD KNOW

> **DO NOT use "Format All + Download" in SP Flash Tool** — it will erase `nvram` and other critical partitions where your IMEI is stored. **You will lose your IMEI.**

| Action | Consequence |
|---|---|
| Erasing `seccfg` incorrectly | Hard brick |
| Erasing `preloader` | Dead phone |
| Erasing `nvram` | IMEI loss |

**Never erase `nvram`, `nvdata`, or modem partitions.**

---

# For Unbrick
1. Use the folder: `Format All Fix.zip`
2. After extracting, copy the files and paste them into: `DECRYPTED_C19_RMX2002_INDIAN`
3. Flash using SP Flash Tool in **Download Only** mode

---

# SP Flash Tool Errors

| Error | Fix |
|---|---|
| Verified Boot Error | Select `DA_6765_6785_6768_6873_6885_6853.bin` from SPFT |
| End of Life Error | Disable **Storage Life Cycle Check** in General section |
| LIB DA Match Error | Reconnect the device |
