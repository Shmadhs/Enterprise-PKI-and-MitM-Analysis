# Enterprise PKI Implementation & Man-in-the-Middle (MitM) Vulnerability Analysis

## Project Overview
This project demonstrates the end-to-end implementation of a secure Public Key Infrastructure (PKI) hierarchy, the configuration of an Apache web server using Elliptic Curve (EC) cryptography, and the enforcement of Mutual TLS (mTLS) authentication. 

Following the defensive setup, an offensive simulation was conducted using ARP Poisoning and Social Engineering to demonstrate the catastrophic impact of Man-in-the-Middle (MitM) attacks on poorly configured local networks, concluding with actionable mitigation strategies.

**Technologies Used:** Kali Linux, OpenSSL, Apache2, Ettercap, Social-Engineer Toolkit (SET), sslscan.

---

## Part 1: Defensive Architecture (Blue Team)

### 1. Root CA & Directory Structure Initialization
To establish a chain of trust, a Root Certificate Authority (CA) was created.

```bash
# Create directory structure
mkdir -p my_pki/{rootCA,interCA,server,client} 
cd my_pki 

# Generate Root CA private key & self-signed certificate
openssl genrsa -aes256 -out rootCA/rootCA.key 4096 
openssl req -x509 -new -nodes -key rootCA/rootCA.key -sha256 -days 3650 -out rootCA/rootCA.crt -subj "/C=GR/O=MyLab/CN=RootCA"
