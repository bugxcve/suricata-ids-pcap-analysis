# suricata-ids-pcap-analysis
Implemented Suricata IDS to analyze PCAP traffic, detect HTTP GET requests via custom rules, and perform log analysis using eve.json and jq.

## 🎯 Objective
Detect HTTP traffic using IDS
Write custom Suricata rules
Analyze alerts from logs
Simulate real-world SOC workflow

## 🛠️ Tools Used
Suricata (IDS/IPS)
PCAP (Packet Capture)
jq (JSON parser)
Linux (Parrot OS)

## ⚙️ Custom Rule
alert http $HOME_NET any -> $EXTERNAL_NET any \
(msg:"GET on wire"; flow:established,to_server; content:"GET"; http_method; sid:12345; rev:3;)

## ▶️ Execution Steps
sudo suricata -r sample.pcap -S custom.rules -k none

## 🚨 Output & Alerts
📌 fast.log
Shows alert summary
Example: "GET on wire"

## 📌 eve.json
Detailed JSON logs
Includes IPs, protocol, HTTP data

## 🔎 Log Filtering using jq
jq -c '[.timestamp,.flow_id,.alert.signature,.proto,.dest_ip]' eve.json

## 📸 Screenshots
🔹 IDS Alert (fast.log)
🔹 JSON Logs (eve.json)
🔹 Filtered Output (jq)

## 📊 Analysis Summary
Detected HTTP GET requests
Traffic from internal IP to external server
Observed redirect response (301)
User-Agent identified (curl)

## 🧠 Key Learnings
IDS rule creation (Suricata)
PCAP traffic analysis
Log analysis (fast.log & eve.json)
JSON parsing using jq
SOC-level alert investigation
