# Task 8: Capture Network Traffic with Wireshark

## 🎯 Objective
Capture live network traffic on a local network using Wireshark, filter for HTTP packets, and analyze the captured data.

## 🛠️ Tools Used
- Wireshark (v4.6.6)
- Windows 11
- Browser: Microsoft Edge

## 📋 Steps Performed

1. **Installed Wireshark** along with the Npcap packet capture driver.
2. **Selected the Wi-Fi interface** as the capture source.
3. **Started a live capture** on the local Wi-Fi network.
4. **Generated HTTP traffic** by visiting `http://neverssl.com`, a website that intentionally uses plain (unencrypted) HTTP instead of HTTPS.
5. **Stopped the capture** after the page fully loaded.
6. **Applied the display filter** `http` to isolate only HTTP packets from the full capture.
7. **Saved the capture** as `wireshark_capture.pcapng`.

## 🔍 Packet Analysis

After applying the `http` filter, 6 HTTP packets were identified:

| No. | Protocol | Description |
|-----|----------|-------------|
| 1 | HTTP | `GET /online HTTP/1.1` — Browser requests the initial page |
| 2 | HTTP | `301 Moved Permanently` — Server redirects to a corrected URL |
| 3 | HTTP | `GET /online/ HTTP/1.1` — Browser follows the redirect |
| 4 | HTTP | `200 OK (text/html)` — Server sends the actual webpage content |
| 5 | HTTP | `GET /favicon.ico HTTP/1.1` — Browser requests the site icon |
| 6 | HTTP | `200 OK (PNG)` — Server sends the favicon image |

### Key Observations
- **HTTP requests** were sent in plain text and could be read directly inside Wireshark — including the **Host header** (`neverssl.com`), the **User-Agent** (Edge browser on Windows 10), and the requested path.
- Since HTTP is **unencrypted**, anyone capturing traffic on the same network (e.g., via Wireshark) can read the full request and response data — including headers, hostnames, and content.
- Most modern websites use **HTTPS (TLS-encrypted)** instead, which would show up as `TLSv1.2`/`TLSv1.3`/`QUIC` traffic with encrypted, unreadable payloads.
- This demonstrates why **HTTPS is critical** for protecting user privacy — plain HTTP exposes browsing activity, headers, and potentially sensitive data to anyone monitoring the network.

## 📁 Files in this Repository
- `wireshark_capture.pcapng` — The saved packet capture file
- `README.md` — This analysis document

## 📌 Conclusion
This task demonstrated how to use Wireshark to capture live network traffic, filter for a specific protocol (HTTP), and interpret the structure of HTTP requests and responses — highlighting the security implications of unencrypted communication.
