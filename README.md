# DNS-over-HTTPS-Set-Up

This guide provides step-by-step instructions for configuring DoH using either Windows 11's built-in DoH settings or alternative third-party tools for older versions of Windows.

---

# Setting Up DNS over HTTPS (DoH) on Windows Machines

DNS over HTTPS (DoH) enhances privacy and security by encrypting DNS queries through the HTTPS protocol, protecting your browsing data from third-party interception. This guide outlines the steps to configure DoH on Windows 11 (which has built-in support) and Windows 10 (using third-party tools).

---

## Table of Contents
- [Requirements](#requirements)
- [Setting Up DoH on Windows 11](#setting-up-doh-on-windows-11)
- [Testing DoH Setup](#testing-doh-setup)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)

---

## Requirements

- **Windows 11**: Direct DoH support.
- **Internet connection**

---

## Setting Up DoH on Windows 11

### Step 1: Open Network & Internet Settings

1. Click on the **Start** menu and go to **Settings**.
2. Navigate to **Network & Internet**.
3. Select **Wi-Fi** (if connected via Wi-Fi) or **Ethernet** (if connected via a wired connection).

## Step 2: Update DNS Settings

1. Go to **Network & Internet** settings in Windows.
2. Right-click your active network connection and select **Properties**.
3. Click on **edit** on **More adapter options**
![image](https://github.com/user-attachments/assets/dee13bbd-fb74-49a3-a5aa-c24f2ca8aa04)

4. Select Internet **Protocol Version 4 (TCP/IPv4)** and click on **Properties**.

   
![image](https://github.com/user-attachments/assets/1f6fd31a-1608-48e1-baa9-ef02a4efe592)

6. Set the **Preferred DNS Server** to `9.9.9.9` and **Alternate DNS Server**: `1.1.1.1`. Then click on **Ok** to save the configuration.

   
![image](https://github.com/user-attachments/assets/3612ca05-137e-4394-aeb5-15dc7676372d)

### Step 3: Access DNS Settings

1. Click on **Hardware properties** under your active network.
2. Scroll down to the **DNS server assignment** section and click on **Edit**.

### Step 3: Configure DoH Servers

1. In the **Edit DNS settings** window:
   - Set **DNS settings** to **Manual**.

     ![image](https://github.com/user-attachments/assets/5136aa35-36ea-4e0b-89d1-7ae299360c6d)

   - Toggle **IPv4** or **IPv6** as needed, then enter DoH server addresses (e.g., Cloudflare, Google, Quad9).
2. Under **Preferred DNS encryption**, select **Encrypted only (DNS over HTTPS)** for each DNS server.

    **Example DoH Servers**:
   - **Quad9**:
     - Prefered DNS: `9.9.9.9`
     - DNS over HTTPS template: [https://dns.quad9.net/dns-query](149.112.112.112)
   - **Cloudflare**:
     - Alternate DNS: `1.1.1.1`
     -  DNS over HTTPS template: [https://one.one.one.one/dns-query](1.0.0.3)
 

     ![image](https://github.com/user-attachments/assets/2d448c71-40a1-4df8-b2b1-ddf2f9bed0ef)


4. Click **Save** to apply the settings.

## Testing DoH Setup

To verify your DoH configuration, visit any of the following test sites:
- **Cloudflare**: [https://1.1.1.1/help](https://1.1.1.1/help)
- **Google**: [https://dns.google/](https://dns.google/)
- **Quad9** : [https://dns.quad9.net:5053/dns-query?name=quad9.net](https://dns.quad9.net:5053/dns-query?name=quad9.net)

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
