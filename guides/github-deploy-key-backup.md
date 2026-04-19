# 🔐 Secure GitHub Backup for .openclaw (Ubuntu Server)
> Set up a surgical Git backup for your `.openclaw` folder using a **Deploy Key**. This ensures your server can only access this specific repository, keeping your main GitHub account secure.

---

## 🏗️ 1. Create the Repository on GitHub
1.  Go to **GitHub.com**.
2.  **Name it**: (e.g., `openclaw-backup`).
3.  Set it to **Private**.
4.  **Do not** initialize with a README or .gitignore.
5.  Click **Create repository**.

---

## 🔑 2. Generate a Dedicated SSH Key
On your Ubuntu server, run the following command to generate a key specific to this backup task:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/openclaw_deploy_key -C "openclaw-server"
```

> [!TIP]
> When prompted for a passphrase, press **Enter twice** to leave it blank for automated backup capability.

---

## 🚀 3. Authorize the Key on GitHub
1.  **Copy the public key text**:
    ```bash
    cat ~/.ssh/openclaw_deploy_key.pub
    ```
2.  On GitHub, navigate to **Settings > Deploy keys** within your new repository.
3.  Click **Add deploy key**.
4.  Paste the key and Title it: `"Ubuntu Server"`.
5.  **CRITICAL**: Check the box **"Allow write access"**.
6.  Click **Add key**.

---

## ⚙️ 4. Configure the SSH Client
Instruct your server to use this specific key for GitHub connections.

1.  **Open (or create) the config file**:
    ```bash
    nano ~/.ssh/config
    ```
2.  **Paste the following configuration**:
    ```text
    Host github.com
      IdentityFile ~/.ssh/openclaw_deploy_key
    ```
    *(Save and exit: `Ctrl+O`, `Enter`, `Ctrl+X`)*

---

## 📤 5. Initialize and Push Data
Replace `your-username` and `your-repo-name` with your actual GitHub details.

```bash
# Navigate to the folder
cd ~/.openclaw

# Initialize git
git init

# (Optional) Create a .gitignore to hide sensitive configs
# echo "config.json" >> .gitignore

# Add and commit files
git add .
git commit -m "Initial backup"

# Set the remote (ensure you use the SSH URL)
git remote add origin git@github.com:your-username/your-repo-name.git

# Push to the main branch
git branch -M main
git push -u origin main
```

---

## 🔄 Future Backups
Whenever you want to save your progress again, run these simple commands:

```bash
git add .
git commit -m "update progress"
git push
```

---
<p align="center">
  <i>Part of the <a href="../README.md">Docs & Guides Collection</a></i>
</p>
