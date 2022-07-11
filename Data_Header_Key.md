

Clean header 

1. Remove the "EARLWORD" prefix
2. Create a table mapping column abbreviations to their details and units
3. Rename CO to CO_avg for the final column to distinguish the two CO columns.

Schema: `EARLWOOD [COL_NAME] [COL_DESC] [UNIT]`
Example:  `EARLWOOD WDR 1h average [°]`

| name   | desc               | unit      |
| ------ | ------------------ | --------- |
| WDR    | 1h average         | [°]       | 
| TEMP   | 1h average         | [°C]      |
| WSP    | 1h average         | [m/s]     |
| NO     | 1h average         | [pphm]    |
| NO2    | 1h average         | [pphm]    |
| CO     | 1h average         | [ppm]     |
| OZONE  | 4h rolling average | [pphm]    |
| PM10   | 1h average         | [µg/m³]   |
| PM2.5  | 1h average         | [µg/m³]   |
| SD1    | 1h average         | [°]       |
| CO_avg | 8h rolling average | [ppm]     |



DOUBLE (Java/Talend)
Data consolidation

Data value unification 

All 1 d.p.
SD1 - 2 d.p.





