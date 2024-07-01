## Query executed:

### 1. DNS Events Search:
```
source="dns.log.gz" host="Sayed" sourcetype="dns"
```
### 2. post extraction of key fields:
```
index=* sourcetype=dns | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```
### 3. In order to identify anomalies:
```
index=* sourcetype=dns  | stats count by fqdn
```
### 4. Finding top 10 DNS sources:
```
index=* sourcetype=dns | top 10 fqdn
```
### 5. Table of fqdn (src, des ip):
```
index=* sourcetype=dns | table fqdn, Src_ip, Dst_ip
```
### 6. Deduction of fqdn with src_ip:
```
index=* sourcetype=dns fqdn=HPE8AA67 | table src_ip | dedup src_ip
```
