# 🧬 Guide: Uploading Raw Sequencing Data to NCBI SRA via FTP (macOS)

**Reference:** Rachael Lappan’s SRA Guide: https://rachaellappan.github.io/SRA/

---

## 📁 Step 1: Prepare Your Raw Data

- Place all your `.fastq.gz` files into **one folder**.
- **Avoid spaces** in folder names to prevent command-line issues.

**Example folder path:**

```
/path/to/your/data_folder
```

---

## 🔐 Step 2: Check and Fix File Permissions

To avoid FTP errors like `550 Operation not permitted`, ensure your files are readable.

Run:

```bash
ls -l /path/to/your/data_folder/*.fastq.gz
```

If you see output like:

```
-rwx------  1 username  staff  36927639  Apr  8  2021 sample_file.fastq.gz
```

It means only the owner can access the file. Fix this by making the files readable:

```bash
chmod +r /path/to/your/data_folder/*.fastq.gz
```

---

## 🧾 Step 3: Start Your SRA Submission

Go to: https://submit.ncbi.nlm.nih.gov/subs/sra/
Choose **FTP upload** when prompted.

You’ll receive:

- FTP server address (e.g., `ftp-private.ncbi.nlm.nih.gov`)
- Username (e.g., `subftp`)
- Password
- Upload folder path (e.g., `uploads/your.email_example_abc123`)

---

## 💻 Step 4: Upload via FTP on macOS

### 🔧 Install FTP Client
macOS no longer includes the FTP command by default. Install it via Homebrew:

```bash
brew install inetutils
```

### 🔌 Connect to FTP Server

```bash
ftp ftp-private.ncbi.nlm.nih.gov
```

Enter your **username** and **password** when prompted.

### 📂 Navigate to Your Upload Folder

```bash
cd uploads/your.email_example_abc123
```

### 📁 Create and Enter a Subfolder (Required)

```bash
mkdir my_submission_folder
cd my_submission_folder
```

### 📍 Set Your Local Directory

```bash
lcd "/path/to/your/data_folder"
```

### 🚀 Upload Your Files

To avoid confirmation prompts for each file:

```bash
prompt
mput *.fastq.gz
```

---

## 📝 Notes

- Uploads may take time depending on your internet speed and file size.
- If you get disconnected due to inactivity (`421 Idle timeout`), simply reconnect and resume.
- For large or repeated uploads, consider using a more robust tool like `lftp`.
