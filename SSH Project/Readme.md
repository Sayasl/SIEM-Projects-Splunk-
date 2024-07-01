## Query executed:

### 1. Searching the event query:
```
Index=ssh.log.gz sourcetype=ssh
```
### 2. Post Extraction of Key Fields:
```
Index=* sourcetype=ssh
```
### 3. Top 10 ip address users:
```
Index=* sourcetype=ssh | top limit=10 user src_ip
```
### 4. Login attempts by action:
```
Index=* sourcetype=ssh | stats count by action
```
### 5. Unusual SSH activity patterns:
```
Index=* sourcetype=ssh | timechart span=1h count by timestamps
```
### 6. Failed login attempts:
```
Index=* sourcetype=ssh | search action="failure"
```
### 7. Investigating suspicious ip address:
```
Index=* sourcetype=ssh | search src_ip="192.168.202.140"
```
### 8. Users with multiple failed attempts:
```
Index=* sourcetype=ssh | search action="failure" | stats count by username
```
### 9. Top Source IPs for SSH Logins:
```
Index=* sourcetype=ssh | stats count by src_ip | sort - count
```
