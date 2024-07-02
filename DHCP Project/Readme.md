## Query executed:

### 1. DHCP Log Search:
```
index=dhcp,log.gz sourcetype=dhcp
```
### 2. Post Extraction of Key Fields:
```
Index=* sourcetype=dhcp
```
### 3. Top 10 Leased IP Address By The Server:
```
index=* sourcetype=dhcp | top limit=10 ip_address
```
### 4. Detect Unusual Patterns in IP:
```
index=* sourcetype=dhcp | timechart span=1h count by timestamps
```
### 5. Monitor Traffic Patterns:
```
index=* sourcetype=dhcp | timechart span=1d count by leased_ip
```
### 6. DHCP Requests and Responses:
```
index=* sourcetype=dhcp | timechart span=1h count by dhcp_message_type
```
### 7. Table of Client Identification:
```
index=* sourcetype=dhcp | table client_identifiers
```
### 8. Client Identifiers Per Day Of The Week:
```
index=* sourcetype=dhcp | eval date_wday=strftime(_time, "%A") | stats count by client_identifiers, date_wday | sort - count
```
### 9. Average # of Events By Month And Day Of The Week:
```
index=* sourcetype=dhcp | eval date_month=strftime(_time, "%B") | eval date_wday=strftime(_time, "%A") | stats avg(linecount) as average_events by date_month, date_wday | sort - average_events
```
### 10. Unique Client Identifiers By IP:
```
index=* sourcetype=dhcp | stats dc(client_identifiers) as unique_clients by ip_address | sort - unique_clients
```
### 11. Average Lease Duration By Month And Weekday:
```
index=* sourcetype=dhcp | eval date_month=strftime(_time, "%B") | eval date_wday=strftime(_time, "%A") | stats avg(lease_duration) as average_lease_duration by date_month, date_wday | sort - average_lease_duration
```