# DNS-over-HTTPS-Set-Up

This guide provides step-by-step instructions for configuring DoH using either Windows 11's built-in DoH settings or alternative third-party tools for older versions of Windows.

---

# Setting Up DNS over HTTPS (DoH) on Windows Machines

DNS over HTTPS (DoH) enhances privacy and security by encrypting DNS queries through the HTTPS protocol, protecting your browsing data from third-party interception. This guide outlines the steps to configure DoH on Windows 11 (which has built-in support) and Windows 10 (using third-party tools).

---

## Table of Contents
- [Requirements](#requirements)
- [Setting Up DoH on Windows 11](#setting-up-doh-on-windows-11)
- [Setting Up DoH on Windows 10 Using Third-Party Tools](#setting-up-doh-on-windows-10-using-third-party-tools)
- [Testing DoH Setup](#testing-doh-setup)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)

---

## Requirements

- **Windows 11**: Direct DoH support.
- **Windows 10**: Requires a third-party tool (e.g., [DNSCrypt-Proxy](https://github.com/DNSCrypt/dnscrypt-proxy) or [Simple DNSCrypt](https://simplednscrypt.org/)).
- **Internet connection**

---

## Setting Up DoH on Windows 11

### Step 1: Open Network & Internet Settings

1. Click on the **Start** menu and go to **Settings**.
2. Navigate to **Network & Internet**.
3. Select **Wi-Fi** (if connected via Wi-Fi) or **Ethernet** (if connected via a wired connection).

### Step 2: Access DNS Settings

1. Click on **Hardware properties** under your active network.
2. Scroll down to the **DNS server assignment** section and click on **Edit**.

### Step 3: Configure DoH Servers

1. In the **Edit DNS settings** window:
   - Set **DNS settings** to **Manual**.
   - Toggle **IPv4** or **IPv6** as needed, then enter DoH server addresses (e.g., Cloudflare, Google, Quad9).
   
   **Example DoH Servers**:
   - **Cloudflare**:
     - Primary: `1.1.1.1`
     - Secondary: `1.0.0.1`
   - **Google**:
     - Primary: `8.8.8.8`
     - Secondary: `8.8.4.4`
   - **Quad9**:
     - Primary: `9.9.9.9`
     - Secondary: `149.112.112.112`

2. Under **Preferred DNS encryption**, select **Encrypted only (DNS over HTTPS)** for each DNS server.

3. Click **Save** to apply the settings.

### Step 4: Verify Configuration

- After configuring DoH, open your browser and visit [https://1.1.1.1/help](https://1.1.1.1/help) (for Cloudflare) or [https://dns.google/](https://dns.google/) (for Google) to verify that DoH is active.

---

## Setting Up DoH on Windows 10 Using Third-Party Tools

Since Windows 10 doesn’t natively support DoH, you’ll need to use a third-party tool. Here’s how to set it up with DNSCrypt-Proxy.

### Step 1: Download DNSCrypt-Proxy

1. Download the latest release of **DNSCrypt-Proxy** from [https://github.com/DNSCrypt/dnscrypt-proxy/releases](https://github.com/DNSCrypt/dnscrypt-proxy/releases).
2. Extract the downloaded zip file to a desired location.

### Step 2: Configure DNSCrypt-Proxy

1. Open the extracted folder and locate `dnscrypt-proxy.toml`.
2. Open `dnscrypt-proxy.toml` in a text editor (e.g., Notepad) and find the `server_names` section.
3. Choose your preferred DoH providers by uncommenting their names (e.g., `cloudflare`, `google`, `quad9-doh`) or add any other supported DoH server.

   ```toml
   server_names = ['cloudflare', 'google', 'quad9-doh']
   ```

4. Save and close the file.

### Step 3: Install DNSCrypt-Proxy as a Service

1. Open **Command Prompt** as an administrator.
2. Navigate to the DNSCrypt-Proxy folder and run:

   ```bash
   dnscrypt-proxy.exe --install
   ```

3. Start the DNSCrypt-Proxy service:

   ```bash
   net start dnscrypt-proxy
   ```

### Step 4: Update DNS Settings

1. Go to **Network & Internet settings** in Windows.
2. Under **Network & Sharing Center**, click on **Change adapter settings**.
3. Right-click your active network connection and select **Properties**.
4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click on **Properties**.
5. Set the **Preferred DNS server** to `127.0.0.1` (loopback address).

### Step 5: Verify Configuration

- Open [https://1.1.1.1/help](https://1.1.1.1/help) (for Cloudflare) or [https://dns.google/](https://dns.google/) to check if DoH is active.

---

## Testing DoH Setup

To verify your DoH configuration, visit any of the following test sites:
- **Cloudflare**: [https://1.1.1.1/help](https://1.1.1.1/help)
- **Google**: [https://dns.google/](https://dns.google/)

These sites will show if DoH is active and confirm that your DNS requests are encrypted.

---

## Troubleshooting

- **DNS Resolution Issues**: If websites fail to load, double-check your DNS server addresses and ensure that the DNSCrypt-Proxy service is running.
- **Flushing DNS Cache**: Sometimes, clearing the DNS cache can resolve issues. Open Command Prompt and run:

  ```bash
  ipconfig /flushdns
  ```

- **Firewall Settings**: Ensure no firewall is blocking DNSCrypt-Proxy or your DNS queries.

---

## Resources

- [DNSCrypt-Proxy GitHub Repository](https://github.com/DNSCrypt/dnscrypt-proxy)
- [Cloudflare DoH Setup Guide](https://developers.cloudflare.com/1.1.1.1/dns-over-https/)
- [Google DoH Documentation](https://developers.google.com/speed/public-dns/docs/dns-over-https)

---

This README should provide everything you need to configure DoH on your Windows machine, protecting your DNS queries from interception. If you encounter any issues, feel free to consult the resources or raise an issue.
