
# Huginn Recon

Huginn Recon is a dark web scraping tool that categorizes websites based on pre-defined categories. The tool generates a report in PDF format along with a graphical representation of categorized results.

## Features
- Scrape dark web sites via Ahmia search engine.
- Categorize scraped results into configurable categories.
- Generate a PDF report with categorized URLs and a graph.
- Supports Tor proxy for anonymous scraping.

---

## Installation

### 1. Clone the repository:
```bash
git clone [<repository_url>](https://github.com/nadimjsaliby/huginn_recon.git)
cd huginn_recon
```

### 2. Install dependencies:
Make sure Python 3.9 or later is installed. Install the required Python libraries using `requirements.txt`:
```bash
pip install -r requirements.txt
```

### 3. Set up Tor

#### Configure Tor to work with the tool:
- **Create a hashed password for the Tor control port**:
  ```bash
  tor --hash-password P@ssw0rd
  ```
  Replace `Cypherw0lf9.1` with your desired password. Copy the output hash and replace it in the `HashedControlPassword` field in `/etc/tor/torrc`.

- **Edit the Tor configuration file (`/etc/tor/torrc`) to include the following lines**:
```
DNSPort 5353
AutomapHostsOnResolve 1
ControlPort 9051
CookieAuthentication 1
HashedControlPassword 16:ABCD1234EF567890FEDCBA9876543210FEDCBA1234567890ABCDEF1234567890
Log debug file /var/log/tor/debug.log
Log notice file /var/log/tor/notices.log
```


- **Restart Tor** to apply the changes:
  ```bash
  sudo systemctl restart tor
  ```

- **Verify Tor is working**:
  Use Telnet to authenticate with the ControlPort using your password:
  ```bash
  telnet 127.0.0.1 9051
  Trying 127.0.0.1...
  Connected to 127.0.0.1.
  Escape character is '^]'.

  authenticate "P@ssw0rd"
  250 OK

  resolve 3g2upl4pq6kufc4m.onion
  250 OK

  quit
  250 closing connection
  ```

#### Configure Torsocks:
Edit the Torsocks configuration file (`/etc/tor/torsocks.conf`) as follows:
```
TorAddress 127.0.0.1
TorPort 9050
OnionAddrRange 127.42.42.0/24
AllowOutboundLocalhost 2
EnableIPv6 1
```

### 4. Verify Tor connectivity:
Run the following command to test connectivity:
```bash
curl --proxy socks5h://127.0.0.1:9050 http://check.torproject.org
```

You should see a message indicating you are using the Tor network.

---

## Usage

### Command-line options:
```bash
python3 huginn_recon.py -q <query> -n <number_of_results> -p -s
```

#### Parameters:
- `-q` or `--query`: The search query string.
- `-n` or `--number`: Number of results to scrape (default: 10).
- `-p` or `--proxy`: Enable Tor proxy for anonymous scraping.
- `-s` or `--scrape`: Scrape additional site content.

### Example:
Search for the term "malware" and categorize results based on the keywords "crypto" and "bug":
```bash
python3 hi.py -q "malware" -n 10 -p -s -k "crypto,bug"
```

---

## Configuration

The categorization is defined in `config.json`. Update the file with your desired categories and associated keywords.

### Example `config.json`:
```json
{
  "Malware Services": ["malware", "ransomware", "exploit", "rat"],
  "Illegal Drugs": ["drugs", "cocaine", "marijuana", "meth"],
  "Financial Fraud": ["fraud", "carding", "counterfeit"],
  "Trafficking": ["child", "woman", "sex"],
  "Identity": ["fake passport", "fake identity"]
}
```

---

## Output

- **PDF Report**: A PDF report named `report.pdf` is generated in the current directory. It includes categorized results and their URLs.
- **Graph**: A graphical representation of categorized results is saved as `category_graph.png`.

---

## Notes

- Ensure Tor is installed and running before using the tool.
- Update `config.json` to match your categorization needs.

---
