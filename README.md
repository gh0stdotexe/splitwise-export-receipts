# Splitwise Export Receipts

A user-friendly tool to export all your Splitwise transaction data—including any/all receipts—into a single spreadsheet (CSV/XLSX). Designed for both technical and non-technical users.

## Features
- Export all expenses (optionally by group/date)
- Download and link all available receipts
- Output a single spreadsheet with all relevant data and clickable receipt links
- Easy-to-use CLI
- Cross-platform (Windows, Mac, Linux)

## 🚨 Splitwise API Setup (Required Before First Use)

> **Note**
> You must create a Splitwise app to obtain your API keys before using this tool. This is a one-time setup required by Splitwise for all third-party tools.
>
> **Steps:**
> 1. Go to [https://secure.splitwise.com/apps/new](https://secure.splitwise.com/apps/new) and create a new app.
> 2. Set the callback URL to anything (e.g., `http://localhost:8080`).
> 3. After creating the app, copy your **Consumer Key** and **Consumer Secret**.
> 4. When you run this tool for the first time, you will be prompted to enter these keys and complete the authorization process in your browser.
> 5. Your credentials will be saved securely in `~/.splitwise_auth.json` for future use.

## ⚡ How to Use (Step-by-Step Flow)

1. **Install dependencies** (in a virtual environment):
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   python -m pip install --upgrade pip
   python3 -m pip install -r requirements-lock.txt
   ```
   > **Note:**
   > - For reproducible installs, use `requirements-lock.txt` (recommended for most users).
   > - `requirements.txt` contains version ranges and is intended for development or as a reference.
2. **Run the tool:**
   ```bash
   python src/splitwise_export_receipts.py
   ```
3. **Authenticate with Splitwise:**
   - Enter your Consumer Key and Secret when prompted.
   - Open the provided authorization URL in your browser.
   - **After authorizing, you will see a browser error (page not found).**

> **Important: Getting the OAuth Verifier**
> - This is expected! Splitwise will redirect you to your callback URL (e.g., `http://localhost:8080`) and the page will not load.
> - **Look at the URL in your browser's address bar.**
> - Find the part that says `oauth_verifier=...` and copy the value after the `=`.
> - Paste this value into the terminal when prompted for the verification code.

> _Example:_
> ```
> http://localhost:8080/?oauth_token=...&oauth_verifier=YOUR_CODE_HERE
> ```
> Copy `YOUR_CODE_HERE` and paste it into the script prompt.

4. **Choose output options:**
   - The script will prompt you for the output file path (default: `splitwise_export.csv`).
   - You can choose `.csv` (recommended) or `.xlsx`.
   - You can also specify the receipts directory (default: `receipts`).

5. **Open your exported spreadsheet:**
   - For CSV: Open in Excel or Google Sheets. The `Receipt` column contains a clickable link for each transaction with a receipt. Click "View Receipt" to open the local file (if it exists on your machine).
   - For XLSX: The `Receipt` column contains the local file path.

6. **Receipts are saved in the specified directory.**

## 📂 Specifying Output Locations

You can control where the spreadsheet and receipts are saved using command-line options:

- **Spreadsheet output file:**
  - Use `--output` (or `-o`) to set the spreadsheet file path:
    ```bash
    python src/splitwise_export_receipts.py --output /path/to/your/spreadsheet.csv
    ```
  - Example:
    ```bash
    python src/splitwise_export_receipts.py --output ~/Desktop/splitwise_export.csv
    ```

- **Receipts directory:**
  - Use `--receipts-dir` to set the receipts folder:
    ```bash
    python src/splitwise_export_receipts.py --receipts-dir /path/to/receipts_folder
    ```
  - Example:
    ```bash
    python src/splitwise_export_receipts.py --receipts-dir ~/Desktop/splitwise_receipts
    ```

- **Combine both:**
  ```bash
  python src/splitwise_export_receipts.py --output ~/Desktop/splitwise_export.csv --receipts-dir ~/Desktop/splitwise_receipts
  ```

- **If you don't specify these options:**
  - The script will prompt you for the output file path (default: `splitwise_export.csv` in the current directory).
  - Receipts will be saved in the `receipts` folder in your current directory by default.

- **See all options:**
  ```bash
  python src/splitwise_export_receipts.py --help
  ```

## Troubleshooting
- If you see a browser error after authorizing Splitwise, this is normal. Just copy the `oauth_verifier` from the URL as described above.
- If you get a `ModuleNotFoundError`, make sure you installed all dependencies in your virtual environment.
- If the receipt links do not work, make sure the receipt files are present at the specified paths on your computer.

## Requirements
- Python 3.10+
- Splitwise account (you will need to create an API app for OAuth)

## Roadmap
- [x] Splitwise API authentication
- [x] Expense fetching
- [x] Receipt downloading
- [x] Data export to spreadsheet
- [x] CLI improvements
- [x] Documentation

## License
MIT
