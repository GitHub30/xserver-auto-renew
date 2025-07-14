# Xserver Auto Renew

An automated tool for renewing Xserver's free VPS service to prevent expiration.

## Overview

This Python application automatically renews your Xserver free VPS service by simulating the manual renewal process through web scraping. It uses session cookies to authenticate and perform the renewal operation, helping you maintain your free VPS without manual intervention.

## Features

- **Automated Renewal**: Automatically renews your Xserver free VPS service
- **Session Management**: Uses browser cookies for authentication
- **Error Handling**: Validates renewal success and provides clear error messages
- **Environment Configuration**: Secure configuration through environment variables
- **User Agent Spoofing**: Uses realistic browser headers to avoid detection

## Installation

1. Clone the repository:

```bash
git clone https://github.com/fa0311/xserver-auto-renew.git
cd xserver-auto-renew
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Set up environment variables:
   Create a `.env` file in the root directory:

## Configuration

### Environment Variables

Create a `.env` file with the following variables:

- `ID_VPS`: Your VPS ID from Xserver (required)
- `USERNAME`: Your Xserver account username (required for automatic login)
- `PASSWORD`: Your Xserver account password (required for automatic login)

```env
ID_VPS=your_vps_id_here
USERNAME=your_username_or_email_here
PASSWORD=your_password_here
```

<img src="image/README/1752250288684.png" alt="image" style="width: 50%;">

### Cookie Setup

You have two options for setting up cookies:

#### Option 1: Automatic Cookie Generation (Recommended)

Use the automated login script to generate cookies:

```bash
python -m xserver-auto-renew.login
```

This script will:

- Open a Chrome browser window
- Automatically log in using your credentials from `.env`
- Generate the `cookies.json` file automatically

**Note**: Make sure you have Chrome installed and accessible in your PATH.

#### Option 2: Manual Cookie Export

1. Log in to your Xserver account in your browser
2. Navigate to the VPS management page
3. Export cookies for the `secure.xserver.ne.jp` domain
4. Save the cookies as `cookies.json` in JSON format

Example `cookies.json` structure:

```json
[
  {
    "domain": "secure.xserver.ne.jp",
    "name": "X2SESSID",
    "path": "/",
    "value": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  },
  {
    "domain": "secure.xserver.ne.jp",
    "name": "XSERVER_DEVICEKEY",
    "path": "/",
    "value": "xxxxxxx"
  }
]
```

### File Structure

```filetree
xserver-auto-renew/
├── xserver-auto-renew/
│   └── ...
├── .env                 # Environment variables
├── cookies.json        # Browser cookies
└── ...
```

## Usage

### Step 1: Generate Cookies (First Time Setup)

Generate authentication cookies using the automated login:

```bash
python -m xserver-auto-renew.login
```

### Step 2: Run the Renewal Script

Run the renewal script:

```bash
python -m xserver-auto-renew.main
```

### Automation

You can combine both steps for fully automated operation:

```bash
python -m xserver-auto-renew.login && python -m xserver-auto-renew.main
```

## Automate with GitHub Actions

### 1. Fork this repository

https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo#forking-a-repository

### 2. Set secrets ID_VPS, USERNAME, PASSWORD

`Settings` > `Secrets and variables` > `Actions` > `Repository secrets` > `New repository secret`

https://docs.github.com/en/actions/how-tos/security-for-github-actions/security-guides/using-secrets-in-github-actions#creating-secrets-for-an-environment

### 3. Run a workflow

`Actions`

![](https://user-images.githubusercontent.com/17570430/224348663-7a50746f-73ae-44c2-b61f-98d8522a1690.png)
