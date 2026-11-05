# Week 1 Extra: Wireshark SOC Labs

**Name:** Durgaprasad Veesam
**Batch:** B084 | **Intern ID:** NW-084-000
**Program:** Networkwalks Cybersecurity Internship

## Overview
I completed 6 Wireshark SOC labs from Networkwalks. In each lab I captured traffic, filtered packets and answered 10 tasks as a SOC analyst. All labs were done in the official practice environment. I scored 100/100 in every lab.

## Labs Completed

| Lab | Topic | Score |
|-----|-------|-------|
| Lab 3 | Identify the Attacker's IP (SYN scan) | 100/100 |
| Lab 4 | Follow TCP Stream (plain-text chat) | 100/100 |
| Lab 5 | Follow TCP Stream, part 2 (hidden note in a web page) | 100/100 |
| Lab 6 | HTTP plain text credentials | 100/100 |
| Lab 7 | Brute force catch (FTP) | 100/100 |
| Lab 8 | VoIP call replay | 100/100 |

---

## Lab 3: Identify the Attacker's IP
- Used the filter `tcp.flags.syn == 1 && tcp.flags.ack == 0` to show only SYN packets.
- One IP sent SYN packets to many ports in a short time. This is a port scan.
- Open port replies with SYN, ACK. Closed port replies with RST, ACK.
- Attack type: SYN (port) scan.

**Wireshark work:**

![Lab 3 Wireshark](Screenshot%202026-11-04%20152548.png)

**Result:**

![Lab 3 result](Lab%203%20Result%20-%20Veesam%20Durgaprasad.png)

---

## Lab 4: Follow TCP Stream
- Found the chat on a non-standard port with `tcp && !(tcp.port == 80 || tcp.port == 443)`.
- Used Follow TCP Stream to read the full plain-text chat.
- The chat showed a temporary password and a Wi-Fi password in clear text.

**Wireshark work:**

![Lab 4 Wireshark](Screenshot%202026-11-04%20171035.png)

**Result:**

![Lab 4 result](Lab%204%20Result%20-%20Veesam%20Durgaprasad.png)

---

## Lab 5: Follow TCP Stream, part 2
- Used `http contains "<!--"` to find web pages with hidden HTML comments.
- Followed the stream and found a hidden IT note with a backup server address and an access code.
- Learned that comments in page source can leak secrets.

**Wireshark work:**

![Lab 5 Wireshark](Screenshot%202026-11-04%20231936.png)

**Result:**

![Lab 5 result](Lab%205%20Result%20-%20Veesam%20Durgaprasad.png)

---

## Lab 6: HTTP Plain Text Credentials
- Found the HTTP POST login request.
- The username and password were readable in the packet details.
- Fix: use HTTPS so login data is encrypted.

**Wireshark work:**

![Lab 6 Wireshark](Screenshot%202026-11-04%20233528.png)

**Result:**

![Lab 6 result](Lab%206%20Result%20-%20Veesam%20Durgaprasad.png)

---

## Lab 7: Brute Force Catch
- Used Follow TCP Stream on the FTP traffic.
- Saw many `530 Login incorrect` replies from one attacker, then `230 Login successful`.
- This is a brute-force (password guessing) attack.
- Fix: account lockout, strong passwords and SFTP.

**Wireshark work:**

![Lab 7 Wireshark](Screenshot%202026-11-04%20235154.png)

**Result:**

![Lab 7 result](Lab%207%20Result%20-%20Veesam%20Durgaprasad.png)

---

## Lab 8: VoIP Call Replay
- Found call setup (SIP) and voice traffic (RTP) with the Telephony menu.
- Identified the codec, the caller and who answered.
- Played the call back with the RTP Player.
- Fix: use encrypted VoIP (SRTP/TLS).

**Wireshark work:**

![Lab 8 Wireshark](Screenshot%202026-11-05%20002137.png)

**Result:**

![Lab 8 result](Lab%208%20Result%20-%20Veesam%20Durgaprasad.png)

---

## Wireshark Skills Used
- Display filters
- Statistics → Conversations and Endpoints
- Follow TCP Stream
- Telephony → VoIP Calls and RTP Player

## What I Learned
- How to detect a port scan, brute force and plain-text password leaks.
- Why we use HTTPS, SFTP and encrypted VoIP.
- A SOC analyst must be able to read packets, not just alerts.

## Troubleshooting
**Problem:** My first count of SYN packets was wrong because I used `tcp.ack`.
**Solution:** I used `tcp.flags.syn == 1` and then added `&& tcp.flags.ack == 0` to show only scan packets.

*All labs were done in the official Networkwalks practice environment, for learning only.*
