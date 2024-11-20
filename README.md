
# HUGINN_RECON: Dark Web Scraping Tool

## Introduction

HUGINN_RECON is a Python-based tool for searching, scraping, and summarizing data from the dark web using the Ahmia search engine. It generates detailed PDF reports, showcasing website metadata, summaries, matching keywords, and relevant links.

---

## Features

- **Dark Web Search**: Query the Ahmia search engine for relevant results.
- **Onion Scraping**: Scrape content from `.onion` websites.
- **Content Summarization**: Summarize website content with configurable sentence limits.
- **Keyword Matching**: Highlight and list links containing user-specified keywords.
- **PDF Report Generation**: Generate professional PDF reports with all scraped data.
- **Proxy Support**: Route traffic through Tor using SOCKS5 proxy.
- **Customizable User-Agent**: Randomized user agents for improved stealth.

---

## Prerequisites

- Python 3.7 or later.
- Tor must be installed and running.
- Install the required Python libraries:

```bash
pip install -r requirements.txt
```

**`requirements.txt`**:
```plaintext
beautifulsoup4
nltk
pyfiglet
requests
reportlab
```

---

## Setting Up Tor

1. **Install Tor**:
   - **Debian/Ubuntu**:
     ```bash
     sudo apt update
     sudo apt install tor
     ```
   - **Red Hat/CentOS**:
     ```bash
     sudo dnf install tor
     ```
   - **macOS (with Homebrew)**:
     ```bash
     brew install tor
     ```

2. **Start Tor Service**:
   ```bash
   sudo systemctl start tor
   sudo systemctl enable tor
   ```

3. **Verify Tor is Running**:
   Ensure Tor is listening on port `9050`:
   ```bash
   netstat -tuln | grep 9050
   ```

4. **Configure Tor (Optional)**:
   To enable control over Tor, edit `/etc/tor/torrc`:
   ```bash
   sudo nano /etc/tor/torrc
   ```
   Uncomment and set the following:
   ```plaintext
   ControlPort 9051
   CookieAuthentication 1
   ```

   Restart Tor after making changes:
   ```bash
   sudo systemctl restart tor
   ```

---

## Usage

Run the script using the following command structure:

```bash
python3 huginn_recon.py -q QUERY -n NUMBER -p -s -k KEYWORDS
```

### Arguments:
- `-q`, `--query`: The search query for Ahmia (required).
- `-n`, `--number`: Number of results to fetch (default: 10).
- `-p`, `--proxy`: Enable Tor proxy for anonymous scraping.
- `-s`, `--scrape`: Enable scraping of `.onion` sites for content and links.
- `-k`, `--keywords`: Comma-separated keywords to match in the site content and links.

### Example:
```bash
python3 huginn_recon.py -q "malware" -n 5 -p -s -k "bitcoin, hacking"
```

---

## Outputs

1. **Console Logs**:
   - Real-time progress updates.
   - Fetched results, scraped data, and identified matches.

2. **PDF Report**:
   - Contains the title, description, URL, summarized content, keywords, and links matching the specified keywords.
   - Saved as `report.pdf` in the current working directory.

---

## Notes

- Ensure Tor is running and listening on `localhost:9050` before running the tool.
- Use responsibly for ethical purposes only.
