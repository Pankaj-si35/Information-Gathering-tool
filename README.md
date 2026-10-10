# Information-Gathering-tool
Information Gathering Tool | Python-based cybersecurity tool for DNS lookup, WHOIS information collection, HTTPS response headers analysis, and JSON report generation on authorized domains.
# 🔎 Information Gathering Tool

### A Python-Based Cybersecurity Reconnaissance Project

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue)
![Domain](https://img.shields.io/badge/Focus-DNS%20%7C%20WHOIS%20%7C%20HTTPS-green)
![Project](https://img.shields.io/badge/Project-Educational-orange)

## 📌 Project Overview

The Information Gathering Tool is a beginner-friendly cybersecurity
project developed using Python. It automates the collection of basic
publicly available information about a domain.

Information gathering, also known as reconnaissance, is an important
early stage of a cybersecurity assessment. It helps security
professionals understand a domain's publicly observable network and
web-related information before conducting an authorized security review.

This tool collects DNS resolution results, attempts to retrieve WHOIS
registration information, examines HTTPS response headers, and saves
the collected results in a structured JSON report.

The project demonstrates Python programming, DNS resolution, command
execution, HTTP communication, error handling, and structured data
storage in a practical cybersecurity context.

> **Important:** This is an educational information-gathering tool.
> It is not a vulnerability scanner, exploitation framework, or
> comprehensive security assessment solution.

---

## 🎯 Project Objectives

The primary objectives of this project are:

- Understand the fundamentals of cybersecurity reconnaissance.
- Retrieve IP addresses associated with a domain through DNS resolution.
- Collect available domain registration information using WHOIS.
- Inspect HTTPS response headers.
- Automate basic information collection using Python.
- Store results in a structured JSON format.
- Practise error handling and network-related programming.
- Understand the limitations of publicly available information.

---

## ⚙️ Features

### 1. DNS Information Gathering

The tool uses Python's built-in `socket` module to resolve a hostname
into IP addresses.

**Information collected:**
- IPv4 addresses, when available.
- IPv6 addresses, when available.
- DNS resolution errors, when resolution fails.

**Why it matters:**

DNS resolution helps analysts understand which IP addresses a domain
currently resolves to. A domain may resolve to multiple addresses,
and results can vary because of DNS configuration, geographic location,
caching, and content delivery networks.

**Limitation:** The tool uses system name resolution. It does not
implement a complete DNS record enumeration engine and does not
directly collect every record type, such as MX, TXT, NS, or SOA.

### 2. WHOIS Information Collection

The tool invokes the system's `whois` command to request available
domain registration information.

Depending on the domain registry and WHOIS server, the response may
contain:
- Registrar information.
- Registration and expiration dates.
- Domain status.
- Name server information.
- Registrant information, if publicly available.

**Why it matters:**

WHOIS data can provide useful context about domain registration and
administrative information during an authorized assessment.

**Limitation:** WHOIS information may be redacted, incomplete,
unavailable, rate-limited, or affected by registry-specific policies.
The tool does not guarantee that all registration details will be
returned.

### 3. HTTPS Response Header Inspection

The tool sends an HTTPS `HEAD` request to the target domain and
attempts to collect response headers.

Depending on the server response, this may reveal:
- HTTP response status.
- Final response URL.
- Server-related headers, if provided.
- Content and caching metadata, if provided.
- Security-related headers, if configured by the website.

**Why it matters:**

HTTP response headers provide insight into how a web server responds
to requests. Security professionals may examine headers as one part
of a broader web security review.

**Limitation:** The tool does not automatically determine whether a
website is secure. A missing header does not, by itself, prove a
vulnerability. Some servers may reject `HEAD` requests or behave
differently from `GET` requests.

### 4. JSON Report Generation

The collected information is stored in a JSON file.

Example output location:

`reports/example_com_report.json`

JSON makes the results easier to read, archive, process, or use in
future automation workflows.

---

## 🧰 Technologies Used

| Technology | Purpose |
|---|---|
| Python 3 | Main programming language |
| socket | Hostname resolution |
| subprocess | Running the system WHOIS command |
| urllib | Sending HTTPS requests |
| json | Structured report generation |
| pathlib | File and directory handling |
| argparse | Command-line argument handling |
| Kali Linux | Development and testing environment |
| WHOIS utilities | Domain registration information requests |
| DNS utilities | Optional manual DNS troubleshooting |

Most Python modules used by the project are included in Python's
standard library.

---

## 🖥️ System Requirements

- Kali Linux or another compatible Linux distribution.
- Python 3.
- WHOIS utility.
- Internet connectivity for external lookups.
- Permission to assess the selected domain.

DNS and HTTPS results depend on network connectivity and the target
domain's configuration.

---

## 📥 Installation

### Step 1: Update package information

```bash
sudo apt update
```

### Step 2: Install required packages

```bash
sudo apt install -y python3 whois dnsutils
```

The `dnsutils` package is useful for manual DNS troubleshooting.
The Python script itself uses Python's `socket` module for hostname
resolution.

### Step 3: Clone the repository

Replace `YOUR_USERNAME` with your GitHub username.

```bash
git clone https://github.com/YOUR_USERNAME/information-gathering-tool.git
```

### Step 4: Enter the project directory

```bash
cd information-gathering-tool
```

### Step 5: Verify Python installation

```bash
python3 --version
```

---

## 🚀 Usage

Run the tool with a domain that you own or are authorized to assess.

### Basic command

```bash
python3 info_gather.py example.com
```

The tool attempts to:

1. Normalize the supplied domain.
2. Resolve its IP addresses.
3. Request WHOIS information.
4. Send an HTTPS `HEAD` request.
5. Display the collected information in the terminal.
6. Save the results to a JSON report.

### Using a full URL

The script accepts a URL and extracts its hostname.

Example:

```bash
python3 info_gather.py https://example.com
```

The current implementation uses the extracted hostname for its
HTTPS request. It does not preserve arbitrary URL paths or query
parameters.

---

## 📊 Sample Output

The following is an illustrative example of the output format.
Actual IP addresses, headers, and WHOIS results may differ.

```text
=======================================================
       INFORMATION GATHERING TOOL
=======================================================
Target domain: example.com

DNS INFORMATION
{
    "ip_addresses": [
        "<resolved-ip-address>"
    ]
}

HTTPS RESPONSE HEADERS
{
    "url": "https://example.com",
    "status": 200,
    "headers": {
        "Content-Type": "text/html"
    }
}

WHOIS INFORMATION
<Available WHOIS response>

=======================================================
Report saved to:
reports/example_com_report.json
=======================================================
```

A successful HTTP response is not guaranteed. DNS resolution,
WHOIS requests, or HTTPS requests may fail because of network
restrictions, server configuration, timeouts, or service availability.

---

## 📁 Project Structure

```text
information-gathering-tool/
│
├── info_gather.py
├── README.md
└── reports/
    └── example_com_report.json
```

### File descriptions

**`info_gather.py`**

Contains the Python implementation for domain normalization,
DNS resolution, WHOIS information collection, HTTPS header
inspection, and JSON report generation.

**`README.md`**

Documents the project's purpose, setup, usage, features, limitations,
and ethical considerations.

**`reports/`**

Stores JSON reports generated by the tool.

Generated reports may contain third-party domain information.
Review them before publishing them in a public repository.

---

## 🧪 Testing and Validation

### 1. Verify Python syntax

```bash
python3 -m py_compile info_gather.py
```

If the command returns no output, Python found no syntax errors.

This does not guarantee that every feature will work correctly.

### 2. Run the tool

```bash
python3 info_gather.py example.com
```

Check whether the tool displays DNS, WHOIS, and HTTPS results.

### 3. Verify report generation

```bash
ls -l reports/
```

### 4. Inspect the JSON report

```bash
cat reports/example_com_report.json
```

### 5. Validate JSON formatting

```bash
python3 -m json.tool reports/example_com_report.json
```

The report must exist before running the JSON validation command.

### 6. Troubleshoot DNS resolution

```bash
dig example.com A +short
```

To check IPv6 records:

```bash
dig example.com AAAA +short
```

These commands can help determine whether DNS resolution works
independently of the Python script.

---

## 🔐 Cybersecurity and Ethical Considerations

This project is intended for educational purposes and authorized
cybersecurity work.

Users should:

- Assess only domains they own or have explicit permission to test.
- Follow applicable laws, organizational policies, and authorization
  requirements.
- Avoid publishing private, confidential, or sensitive information.
- Review generated reports before sharing them publicly.
- Respect service rate limits and acceptable-use policies.

The tool performs basic information collection. It does not attempt
password attacks, exploitation, unauthorized access, or vulnerability
exploitation.

Public availability of information does not automatically authorize
every possible use of that information.

---

## ⚠️ Limitations

The current version has the following limitations:

- It collects only a limited set of domain-related information.
- DNS resolution relies on the system's name-resolution facilities.
- WHOIS results depend on external services and registry policies.
- HTTPS header collection uses a `HEAD` request.
- HTTPS requests may fail for some domains.
- The tool does not verify all TLS security properties.
- It does not perform port scanning or subdomain enumeration.
- It does not detect or confirm vulnerabilities.
- It does not perform comprehensive security testing.
- Network errors may result in incomplete reports.

Results should be interpreted as preliminary technical observations,
not as proof that a domain is secure or vulnerable.

---

## 🔮 Future Improvements

Potential improvements for future versions include:

- Support for additional DNS record types.
- Better validation of domain names and internationalized domains.
- Configurable request timeouts and retry policies.
- More detailed logging and error reporting.
- Unit tests for individual functions.
- Automated report summaries.
- CSV and HTML report export.
- Optional command-line output formatting.
- Improved TLS certificate metadata collection.
- Additional checks for selected HTTP security headers.

Any future network checks should remain within the scope of authorized
testing and should include appropriate rate limiting.

---

## 🎓 Learning Outcomes

Through this project, I practised:

- Python scripting for cybersecurity tasks.
- Hostname resolution and basic DNS concepts.
- Calling external system utilities safely through argument lists.
- Making HTTPS requests.
- Handling exceptions and network failures.
- Structuring data using JSON.
- Creating command-line tools.
- Documenting installation, usage, and limitations.
- Understanding ethical reconnaissance practices.

---

## 👨‍💻 Author

Pankaj Singh

Cybersecurity Learner | Python | Kali Linux | Information Gathering

GitHub: https://github.com/YOUR_USERNAME

Replace the placeholder values with your actual name and GitHub
username before publishing.

---

## 📄 License

If you want others to reuse and modify this project, consider
adding an appropriate open-source license, such as the MIT License,
after reviewing its terms.

If no license is included, do not assume that others automatically
have permission to reuse, modify, or redistribute the code.

---

## ⭐ Acknowledgment

This project was created as a hands-on learning exercise to explore
basic information gathering and Python automation in cybersecurity.
