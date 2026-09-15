# Wireshark Network Traffic Analysis

## Overview

This project demonstrates practical network traffic analysis using Wireshark from a SOC Analyst perspective.

The objective was to capture and investigate network traffic, apply display filters, identify protocols and communication patterns, and use Wireshark's statistical and expert-analysis capabilities to understand network behavior.

The project focuses on practical packet analysis rather than analyzing every packet individually.

## Objectives

- Capture and inspect live network traffic
- Apply Wireshark display filters
- Analyze DNS traffic
- Investigate TCP connections and SYN packets
- Examine TLS and QUIC traffic
- Identify communicating hosts and network conversations
- Analyze protocol distribution
- Visualize traffic activity over time
- Review Expert Information for network anomalies and protocol events
- Document findings using screenshots and investigation notes


## Environment

| Component | Details |
|---|---|
| Operating System | Windows |
| Tool | Wireshark |
| Wireshark Version | 4.4.7 |
| Network Interface | Wi-Fi |
| Host IPv4 | 192.168.1.5 |
| Capture Format | PCAPNG |



## Investigation Workflow

1. Network Traffic Capture
2. Packet Filtering
3. Protocol Identification
4. DNS Analysis
5. TCP Analysis
6. TLS / QUIC Analysis
7. Conversation Analysis
8. Protocol Statistics
9. I/O Graph Analysis
10. Expert Information Review
11. Evidence Documentation


## 1. Host-Based Traffic Filtering

Display filter used: ip.addr == 192.168.....


---

## 2. DNS Traffic Analysis

Display filters used: dns



---
## 3. TCP Analysis

Display filter: tcp
 Example:
 tcp.flags.syn == 1 && tcp.flags.ack == 0

---

## 4. TLS Analysis

Display filter: tls


---

## 5. QUIC Analysis

Display filter: quic

 Example:
 quic && udp.port == 443


 
---

## 6. Conversations Analysis

Wireshark:

**Statistics → Conversations → IPv4**

Conversation statistics were reviewed to identify:

- Communicating hosts
- Packet counts
- Byte volumes
- Connection duration
- Traffic direction
- High-volume conversations

This provides a quick way for a SOC analyst to identify network relationships that may require further investigation.

The analysis included IPv4 conversations involving the local host `192.168.1.....



## 7. Protocol Hierarchy Analysis

Wireshark:

**Statistics → Protocol Hierarchy**

The Protocol Hierarchy view was used to understand the composition of the captured traffic.

The analyzed traffic included:

- IPv4
- TCP
- UDP
- TLS
- QUIC

This provides a high-level view of the protocols present before performing deeper packet-level investigation.

## 8. I/O Graph Analysis

Wireshark:

**Statistics → I/O Graphs**

The I/O Graph was used to visualize packet activity over time.

The graph helped identify periods of increased packet activity within the capture.

Traffic spikes can provide useful investigation points for further examination of the corresponding packets, protocols, and conversations.

The graph was used as a traffic-visibility tool rather than treating a spike alone as evidence of malicious activity.


## 9. Expert Information Analysis

Wireshark:

**Analyze → Expert Information**

The Expert Information view highlighted several TCP and protocol events, including:

- Connection resets
- Suspected retransmissions
- Duplicate ACKs
- Out-of-order segments
- SYN/ACK activity
- Connection closing events

These indicators were treated as investigation points rather than automatically classified as malicious activity.

Further investigation and contextual correlation would be required before determining whether any event represents a security incident.


# Key Wireshark Display Filters

| Purpose | Display Filter |
|---|---|
| Host traffic | `ip.addr == 192.168.1... |
| Source host | `ip.src == 192.168.1... |
| Destination host | `ip.dst == 192.168.1... |
| TCP traffic | tcp |
| TCP port 443 | tcp.port == 443 |
| SSH traffic | tcp.port == 22 |
| DNS traffic | dns |
| DNS queries | dns.flags.response == 0 |
| TLS traffic | tls |
| QUIC traffic | quic |
| QUIC/HTTPS | quic && udp.port == 443 |
| TCP SYN packets | tcp.flags.syn == 1 && tcp.flags.ack == 0 |
| HTTPS SYN packets | tcp.flags.syn == 1 && tcp.flags.ack == 0 && tcp.dstport == 443 |
| HTTP requests | http.request |



## SOC Analyst Investigation Approach

A practical investigation workflow demonstrated in this project was:

1. Identify the local host.
2. Filter traffic associated with the host.
3. Identify protocols being used.
4. Investigate DNS requests.
5. Examine TCP connection attempts.
6. Review encrypted TLS/QUIC communication.
7. Identify major network conversations.
8. Review protocol statistics.
9. Examine traffic patterns over time.
10. Review Wireshark Expert Information.
11. Correlate observations before determining whether further investigation is required.


## Findings

The captured traffic showed a mixture of encrypted and name-resolution traffic.

Key observations included:

- Significant TCP/TLS traffic.
- QUIC traffic over UDP/443.
- DNS queries to multiple domains.
- Multiple external network conversations.
- TCP retransmissions and duplicate ACK events.
- TCP connection resets and connection-closing events.
- Noticeable traffic spikes in the I/O graph.

These observations demonstrate how Wireshark can be used to move from high-level traffic visibility to packet-level investigation.

**Important:** Network events such as retransmissions, resets, duplicate ACKs, and out-of-order packets are not, by themselves, proof of malicious activity. They require contextual investigation.


## Skills Demonstrated

- Network Packet Analysis
- Wireshark
- Display Filters
- TCP/IP Analysis
- DNS Analysis
- TLS Analysis
- QUIC Analysis
- Network Conversations
- Protocol Hierarchy Analysis
- Traffic Visualization
- Expert Information Analysis
- Network Troubleshooting
- SOC Investigation Methodology
- Security Evidence Documentation

## Evidence

Screenshots included in this repository demonstrate the practical analysis performed during the investigation.

Key evidence includes:

- TCP SYN analysis
- TLS traffic
- QUIC destinations
- TCP stream analysis
- Protocol hierarchy
- IPv4 conversations
- Busiest network conversations
- I/O graph
- Expert Information
- Host-based packet filtering

<img width="1580" height="615" alt="apktool" src="" />


## Lessons Learned

This project strengthened practical understanding of how a SOC analyst can use Wireshark to investigate network activity.

The main takeaway was that effective packet analysis is not simply about inspecting individual packets.

A structured approach using:

- Display filters
- Conversations
- Protocol statistics
- Traffic graphs
- Expert Information
- Packet-level inspection

allows an analyst to quickly narrow down relevant network activity and determine where deeper investigation may be required.



## Disclaimer

This project was performed for educational and cybersecurity learning purposes on network traffic available to the analyst.

Sensitive or personally identifiable network data should not be publicly shared.

Raw packet captures should be reviewed and sanitized before being published to a public repository.

The observations documented in this project are intended for educational analysis and should not be interpreted as confirmation of malicious activity without additional evidence and contextual investigation.


