# Cleaning headers

### Table for header details

(Set aside for future iterations considering how we're not using Redshift)

Create a separate table containing details for table header abbreviations.

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

### Complete for version 1

### Schema

Data value unification

They should all be FLOAT/DOUBLE except for DATE and TIME
All 1 d.p.
SD1 - 2 d.p.

### Formatting Date and Time into a Datetime

Put Date and Time together to produce a datetime string and then convert it into a Date object formatted as `"dd/MM/yyyy'T'HH:mm:ss"`.

```java
String seconds = "00";
String date = input_row.Date;
String time = input_row.Time + ":" + seconds;

String datetimeString = date + "T" + time;


Date datetime = TalendDate.TO_DATE(datetimeString, "dd/MM/yyyy'T'HH:mm:ss");

output_row.Datetime = datetime;
output_row.WDR = input_row.WDR;
output_row.TEMP = input_row.TEMP;
output_row.WSP = input_row.WSP;
output_row.NO = input_row.NO;
output_row.NO2 = input_row.NO2;
output_row.OZONE1 = input_row.OZONE1;
output_row.OZONE4 = input_row.OZONE4;
output_row.PM10 = input_row.PM10;
output_row.PM2_5 = input_row.PM2_5;
output_row.HUMID = input_row.HUMID;
output_row.SD1 = input_row.SD1;
```

### Context groups

| variable            | details                                                      |
| ------------------- | ------------------------------------------------------------ |
| local_folder        | path to local folder where downloads land; must end with '/' |
| aws_access_key      |                                                              |
| aws_secret_key      |                                                              |
| aws_initial_bucket  | name of S3 staging bucket                                    |
| aws_final_bucket    | name of S3 production bucket                                 |
| raw_data_filename   | name for raw data file                                       |
| final_data_filename | name for final cleaned data file                             |
