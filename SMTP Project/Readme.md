## Query executed:

### 1. SMTP Search:
```
index="smtp.log.gz" host="Sayed" sourcetype="smtp"
```
### 2. Post Extraction Of Key Fields:
```
Index=* sourcetype=smtp
```
### 3. Top 10 IP Addresses By Email Senders:
```
index=* sourcetype=smtp | top limit=10 src_ip
```
### 4. Top 10 IP Addresses By Recipient Email:
```
index=* sourcetype=smtp | top limit=10 dest_ip
```
### 5. Unusual Patterns In Email Traffic:
```
index=* sourcetype=smtp | timechart span=1h count by timestamp
```
### 6. Email Activity Patterns And Deviations From Usual Behavior:
```
index=* sourcetype=smtp | timechart span=1d count by src_ip
```
### 7. Identifies The Top Domains Based On Traffic Volume:
```
index=* sourcetype=smtp | stats count by domain | sort - count | head 10
```
### 8. Identifies Source IPs That Are Generating The Most Error Responses:
```
index=* sourcetype=smtp | search res_code>=400 | stats count by src_ip | sort - count
```
### 9. Response Messages Over Time:
```
index=* sourcetype=smtp | timechart span=1h count by res_msg
```
### 10. Combines Multiple Fields To Provide A Comprehensive Analysis:
```
index=* sourcetype=smtp | stats count by host, source, sourcetype, dest_ip, domain, index, punct, res_msg, src_ip, timestamp | sort - count
```
