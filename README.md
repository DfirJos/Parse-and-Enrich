# Parse-and-Enrich - finding indicators in doc(x), xlsx(x), pdf, txt, and csv

This script searches for indicators in doc(x), xls(x), pdf, txt, and csv files. It also enriches IP addresses with additonal IP address data from ipinfo.io.

Default indicators that it looks for
- URL's
- E-mail addresses
- mobile phone numbers
- IP addresses
- MD5 hashes
- SHA1 hashes
- SHA256 hashes
- custom indicators

It outputs them to a csv file:

```bash
  $ Parse-and-Enrich.py -i Input/*.csv

  2022-08-11_132728_results.csv

  | Regex result  | Count | Type      | Found in file(s) | City          | Country | Organization       | Full | Error
  |---------------|-------|-----------|------------------|---------------|---------|--------------------|------|------
  | 8.8.8.8       | 4     | ipaddress | ['file1.txt']    | Mountain View | US      | AS15169 Google LLC | ...  |
  | j@mail.com    | 1     | email     | ['random.csv']   |               |         |                    |      |

```




## How to enrich Office365 UAL logs (or other CSV's) with ipinfo.io data

```bash
  $ Parse-and-Enrich.py -i Input/AuditRecords.csv -csv_e
```

AuditRecords.csv
```
timestamp, user, ip
2022-08-11 13:05:01, user1@company.nl, 8.8.8.8
```

Becomes AuditRecords.csv_enriched.csv:

```
timestamp, user, ip, ip_info
2022-08-11 13:05:01, user1@company.nl, 8.8.8.8, {"ip": "8.8.8.8", "hostname": "dns.google", "anycast": "True", "city": "Mountain View", "region": "California", "country": "US", "loc": "37.4056,-122.0775", "org": "AS15169 Google LLC", "postal": "94043", "timezone": "America/Los_Angeles", "country_name": "United States", "latitude": "37.4056", "longitude": "-122.0775"}
```


## Limitations

- csv files must be of the same encoding type. You can specify the type with, for example: -csv_c UTF8