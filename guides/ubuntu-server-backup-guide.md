# 📸 Ubuntu Server Snapshot & Reset Guide (Timeshift)

> Use Timeshift as a "System Restore" point to safely experiment, wipe testing projects, or return your server to a clean state.

---

## 🛠️ Installation

Install Timeshift via the terminal:

```bash
sudo apt update && sudo apt install timeshift -y
```

---

## 🏗️ 1. Choose Your Reset Strategy

By default, Timeshift ignores your personal files (`/home`). Depending on your goals, choose one of the following configurations.

### Option A: Total Reset (Wipe Everything)

Use this if you want a **clean slate** that deletes projects, downloaded models, and any files created in your home folder after the save point.

1.  **Open the config file:**
    ```bash
    sudo nano /etc/timeshift/timeshift.json
    ```
2.  **Locate the `"exclude"` list** and change the patterns to include your home and root directories:
    ```json
    "exclude" : [
        "+ /home/YOUR_USERNAME/**",
        "+ /root/**"
    ],
    ```
    _(Replace `YOUR_USERNAME` with your actual username)_

### Option B: System Only (Keep Personal Files)

Use this to undo software installations and system changes, but **keep** your project files, AI models, and scripts in `/home`.

- **Config:** This is the default setting. Ensure your `/etc/timeshift/timeshift.json` **excludes** home:
  ```json
  "exclude" : [
      "/home/YOUR_USERNAME/**",
      "/root/**"
  ],
  ```

---

## 💾 2. Creating a Snapshot (The "Save" Point)

Run this **before** starting a new experiment or installing heavy AI tools:

```bash
sudo timeshift --create --comments "Before AI Testing" --tags D
```

---

## 🔄 3. Restoring (The "Undo" Button)

To return to your saved state:

```bash
sudo timeshift --restore
```

1.  **Select Snapshot**: Enter the number of your desired save point.
2.  **Confirm Restore**: Press Enter for default partitions.
3.  **Review Deletions**:
    - **Option A**: Any file created in `/home` after the save point will be deleted.
    - **Option B**: Files in `/home` will remain untouched.

> [!CAUTION]
> **Automatic Reboot**: The system will automatically reboot to complete the restoration process. Ensure all work is saved.

---

## 📉 4. Maintenance Tips

- **Check Space:** Monitor space using `df -h`. Some projects are large and can fill your drive quickly.
- **List Snapshots**: `sudo timeshift --list`
- **Delete Old Snapshots**: `sudo timeshift --delete --snapshot 'DATE_STRING'`
- **Full Cleanup**: To delete all old points and free up space: `sudo timeshift --delete`

---

<p align="center">
  <i>Part of the <a href="../README.md">Docs & Guides Collection</a></i>
</p>
