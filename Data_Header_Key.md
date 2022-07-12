Include in version 2.

### Table for header details

1. Remove the "EARLWORD" prefix
2. Create a table mapping column abbreviations to their details and units
3. Rename CO to CO_avg for the final column to distinguish the two CO columns.

Schema: `EARLWOOD [COL_NAME] [COL_DESC] [UNIT]`
Example: `EARLWOOD WDR 1h average [°]`

| name   | desc               | unit    |
| ------ | ------------------ | ------- |
| WDR    | 1h average         | [°]     |
| TEMP   | 1h average         | [°C]    |
| WSP    | 1h average         | [m/s]   |
| NO     | 1h average         | [pphm]  |
| NO2    | 1h average         | [pphm]  |
| CO     | 1h average         | [ppm]   |
| OZONE  | 1h average         | [pphm]  |
| OZONE  | 4h rolling average | [pphm]  |
| PM10   | 1h average         | [µg/m³] |
| PM2.5  | 1h average         | [µg/m³] |
| HUMID  | 1h average         | [%]     |
| SD1    | 1h average         | [°]     |
| CO_avg | 8h rolling average | [ppm]   |

### Headers

Date
Time
EARLWOOD WDR 1h average [°]
EARLWOOD TEMP 1h average [°C]
EARLWOOD WSP 1h average [m/s]
EARLWOOD NO 1h average [pphm]
EARLWOOD NO2 1h average [pphm]
EARLWOOD CO 1h average [ppm]
EARLWOOD OZONE 1h average [pphm]
EARLWOOD OZONE 4h rolling average [pphm]
EARLWOOD PM10 1h average [µg/m³]
EARLWOOD PM2.5 1h average [µg/m³]
EARLWOOD HUMID 1h average [%]
EARLWOOD SD1 1h average [°]
EARLWOOD CO 8h rolling average [ppm]


Complete for version 1
### Schema

Data value unification

They should all be FLOAT/DOUBLE except for DATE and TIME
All 1 d.p.
SD1 - 2 d.p.


### Formatting Date and Time into a Datetime

Put Date and Time together to produce a datetime string and then convert it into a Date object formatted as "dd/MM/yyyy'T'HH:mm:ss".

```java
String seconds = "00";
String date = removeEmptyCols.Date;
String time = removeEmptyCols.Time + ":" + seconds;

String datetimeString = date + "T" + time;


Date datetime = TalendDate.TO_DATE(datetimeString, "dd/MM/yyyy'T'HH:mm:ss");
String datetimeFormatted = TalendDate.formatDate("yyyy-MM-dd'T'HH:mm:ss", datetime);

output_row.Datetime = datetime;
```