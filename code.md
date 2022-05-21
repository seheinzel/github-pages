---
layout: page
title: Code & Query
permalink: code
---
<h3><center>The Leaky Faucet: A SQL Based Real World Project</center></h3>

A local municipality discovered that it was being charged for more water consumption than what was indicated by the residents' meters. After no underground leaks were detected, it become more likely that the discrepancy stemmed from problematic water useage data collection/reporting. I volunteered to examine the town's water useage and billing data to see if the mystery of the missing water could be sovled.

```
SELECT name FROM sqlite_master WHERE type='table';
```

| name                 |
| :--- |
| Company              | 
| Rates                |
| System History       |
| System Meters        |
| new_customer_history |

```
PRAGMA table_info(new_customer_history);
```

| cid | name              | type     | notnull | 
|:----|:------------------|:---------|:--------|
| 0   | Route             | DOUBLE   | 0       | 
| 1   | Service Adr       | TEXT     | 0       |
| 2   | Beginning Reading | DOUBLE   | 0       |
| 3   | Beginning Date    | DATETIME | 0       |
| 4   | Current Reading   | DOUBLE   | 0       |
| 5   | Current Date      | DATETIME | 0       |
| 6   | Useage            | DOUBLE   | 0       |
| 7   | Amount            | DOUBLE   | 0       |
| 8   | BaseRate          | DOUBLE   | 0       |

```
SELECT * FROM new_customer_history;
```

| Route | Service Adr | Beginning Reading | Beginning Date      | Current Reading | Current Date        | Useage     | Amount    | BaseRate | Other1 | Other1 Amount | Other 2 | Other 2 Amount | Other 3 | Other 3 Amount | Taxable Amount | Local Tax | County Tax | State Tax | Total Tax | Previous Balance | Late | Total Amount | Trans Date          | Trans Type | Period Total | Memo | CustID | rateSched | proRate | estReading | Posted | DueDate | LogDate | mtrMult |
|:------|:------------|:------------------|:--------------------|:----------------|:--------------------|:-----------|:----------|:---------|:-------|:--------------|:--------|:---------------|:--------|:---------------|:---------------|:----------|:-----------|:----------|:----------|:-----------------|:-----|:-------------|:--------------------|:-----------|:-------------|:-----|:-------|:----------|:--------|:-----------|:-------|:--------|:--------|:--------|
| 193.0 | RR Towanda  | 31027100.0        | 2002-12-23 00:00:00 | 47651000.0      | 2003-01-24 00:00:00 | 16623900.0 | 94770.68  | 0.0      |        | 0.0           |         | 0.0            |         | 0.0            | 94770.68       | 4738.53   | 0.0        | 0.0       | 4738.53   | 0.0              | 0.0  | 99509.21     | 2003-01-29 00:00:00 | I          | 99509.21     |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     |
| 193.0 | RR Towanda  | 47651000.0        | 2003-01-24 00:00:00 | 62270000.0      | 2003-02-24 00:00:00 | 14619000.0 | 83342.75  |          |        | 0.0           |         | 0.0            |         | 0.0            | 83342.75       | 4167.14   | 0.0        | 0.0       | 4167.14   | 99509.21         | 0.0  | 187019.1     | 2003-02-25 00:00:00 | I          | 87509.89     |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     |
| 193.0 | RR Towanda  | 62270000.0        | 2003-02-24 00:00:00 | 76614000.0      | 2003-03-25 00:00:00 | 14344000.0 | 81775.25  |          |        | 0.0           |         | 0.0            |         | 0.0            | 81775.25       | 4088.76   | 0.0        | 0.0       | 4088.76   | 187019.1         | 0.0  | 272883.11    | 2003-03-26 00:00:00 | I          | 85864.01     |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     |
| 193.0 | RR Towanda  | 76614000.0        | 2003-03-25 00:00:00 | 148755000.0     | 2003-07-28 00:00:00 | 72141000.0 | 411218.15 |          |        | 0.0           |         | 0.0            |         | 0.0            | 411218.15      | 20560.91  | 0.0        | 0.0       | 20560.91  | 272883.11        | 0.0  | 704662.17    | 2003-07-28 00:00:00 | I          | 431779.06    |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     |
| 193.0 | RR Towanda  | 148755000.0       | 2003-07-28 00:00:00 | 178186975.0     | 2003-08-25 00:00:00 | 29431975.0 | 167776.71 |          |        | 0.0           |         | 0.0            |         | 0.0            | 167776.71      | 8388.84   | 0.0        | 0.0       | 8388.84   | 704662.17        | 0.0  | 880827.72    | 2003-08-25 00:00:00 | I          | 176165.55    |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     |

```
SELECT DISTINCT "Service Adr"
FROM new_customer_history
WHERE Useage >=0;
ORDER BY "Service Adr"```

| Service Adr      |
|:-----------------|
|  1167 Main Street |
|  1167 Main St.    |
|  1168 Main Street | 
| 1170 E. Cook   |



SELECT *,
    substr("Current Date", 6, 2) || '/' || substr("Current Date", 9,2)|| '/' || substr("Current Date", 1,4) AS date_reformatted
FROM new_customer_history
WHERE Useage >=0;
| Route | Service Adr | Beginning Reading | Beginning Date      | Current Reading | Current Date        | Useage     | Amount    | BaseRate | Other1 | Other1 Amount | Other 2 | Other 2 Amount | Other 3 | Other 3 Amount | Taxable Amount | Local Tax | County Tax | State Tax | Total Tax | Previous Balance | Late | Total Amount | Trans Date          | Trans Type | Period Total | Memo | CustID | rateSched | proRate | estReading | Posted | DueDate | LogDate | mtrMult | date_reformatted |
|:------|:------------|:------------------|:--------------------|:----------------|:--------------------|:-----------|:----------|:---------|:-------|:--------------|:--------|:---------------|:--------|:---------------|:---------------|:----------|:-----------|:----------|:----------|:-----------------|:-----|:-------------|:--------------------|:-----------|:-------------|:-----|:-------|:----------|:--------|:-----------|:-------|:--------|:--------|:--------|:-----------------|
| 193.0 | RR Towanda  | 31027100.0        | 2002-12-23 00:00:00 | 47651000.0      | 2003-01-24 00:00:00 | 16623900.0 | 94770.68  | 0.0      |        | 0.0           |         | 0.0            |         | 0.0            | 94770.68       | 4738.53   | 0.0        | 0.0       | 4738.53   | 0.0              | 0.0  | 99509.21     | 2003-01-29 00:00:00 | I          | 99509.21     |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     | 01/24/2003       |
| 193.0 | RR Towanda  | 47651000.0        | 2003-01-24 00:00:00 | 62270000.0      | 2003-02-24 00:00:00 | 14619000.0 | 83342.75  |          |        | 0.0           |         | 0.0            |         | 0.0            | 83342.75       | 4167.14   | 0.0        | 0.0       | 4167.14   | 99509.21         | 0.0  | 187019.1     | 2003-02-25 00:00:00 | I          | 87509.89     |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     | 02/24/2003       |
| 193.0 | RR Towanda  | 62270000.0        | 2003-02-24 00:00:00 | 76614000.0      | 2003-03-25 00:00:00 | 14344000.0 | 81775.25  |          |        | 0.0           |         | 0.0            |         | 0.0            | 81775.25       | 4088.76   | 0.0        | 0.0       | 4088.76   | 187019.1         | 0.0  | 272883.11    | 2003-03-26 00:00:00 | I          | 85864.01     |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     | 03/25/2003       |
| 193.0 | RR Towanda  | 76614000.0        | 2003-03-25 00:00:00 | 148755000.0     | 2003-07-28 00:00:00 | 72141000.0 | 411218.15 |          |        | 0.0           |         | 0.0            |         | 0.0            | 411218.15      | 20560.91  | 0.0        | 0.0       | 20560.91  | 272883.11        | 0.0  | 704662.17    | 2003-07-28 00:00:00 | I          | 431779.06    |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     | 07/28/2003       |
| 193.0 | RR Towanda  | 148755000.0       | 2003-07-28 00:00:00 | 178186975.0     | 2003-08-25 00:00:00 | 29431975.0 | 167776.71 |          |        | 0.0           |         | 0.0            |         | 0.0            | 167776.71      | 8388.84   | 0.0        | 0.0       | 8388.84   | 704662.17        | 0.0  | 880827.72    | 2003-08-25 00:00:00 | I          | 176165.55    |      | 6      | 3         | 0       | 0          | 1      |         |         | 1.0     | 08/25/2003       |