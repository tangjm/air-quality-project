# Imputing null values

### The Plan

For each empty row, we want to fill it in with the value in the previous row
This means we need access to only the previous row, which we can get through the tMemorizeRows component.

But what happens when the previous row is also null/empty?

- We can check the previous row and if it is also empty, then we keep looking at previous rows until we find a non-empty row.

But tMemorizeRows requires us to specify a limit on the number of previous rows to keep in memory.

For our data set, we can be sure that some row in the last 50 is not empty, so we can memorise the last 50 rows and use the value of the last non-empty row within that set as the value to replace the current empty row.

```java
// Main Code
//TODO -> for each if statement create a for loop to set
//	    loop i to e.g 50 or 100
//        and if xxx_tMemorizeRows_1[i] != null
// 	    row3.xxx = xxx_tMemorizeRows_1[i]
// n.b. WDR_tMemorizeRows_2 is an array of Floats, it has type Float[]
// The 0th index corresponds to the current row.

int memorisedRowCount = 50;
if (column[0] == null) {
  for (int i = 1; i < memorisedRowCount; i++) {
    if (column[i] != null) {
      column[0] = column[i];
      break;
    }
  }
}
```

Actual Java code used in tJavaRow component

```java
int memorisedRowCount = ((Integer)globalMap.get("tMemorizeRows_1_NB_LINE_ROWS"));
Float[][] columns = {
  WDR_tMemorizeRows_1,
  TEMP_tMemorizeRows_1,
  WSP_tMemorizeRows_1,
  NO_tMemorizeRows_1,
  NO2_tMemorizeRows_1,
  OZONE1_tMemorizeRows_1,
  OZONE4_tMemorizeRows_1,
  PM10_tMemorizeRows_1,
  PM2_5_tMemorizeRows_1,
  HUMID_tMemorizeRows_1,
  SD1_tMemorizeRows_1
};

for (Float[] column : columns) {
  if (column[0] == null) {
    for (int i = 1; i < memorisedRowCount; i++) {
      if (column[i] != null) {
        column[0] = column[i];
        break;
      }
    }
  }
}

output_row.Datetime = input_row.Datetime;
output_row.WDR = WDR_tMemorizeRows_1[0];
output_row.TEMP = TEMP_tMemorizeRows_1[0];
output_row.WSP = WSP_tMemorizeRows_1[0];
output_row.NO = NO_tMemorizeRows_1[0];
output_row.NO2 = NO2_tMemorizeRows_1[0];
output_row.OZONE1 = OZONE1_tMemorizeRows_1[0];
output_row.OZONE4 = OZONE4_tMemorizeRows_1[0];
output_row.PM10 = PM10_tMemorizeRows_1[0];
output_row.PM2_5 = PM2_5_tMemorizeRows_1[0];
output_row.HUMID = HUMID_tMemorizeRows_1[0];
output_row.SD1 = SD1_tMemorizeRows_1[0];
```

### Future considerations

For the next iteration, we can use a 'for' loop to set the new values for the output columns.

```java
// Something along the lines of this
for (Float[] column : columns) {
  output_row.column_name = column[0]
}
```

We can also consider optimising the current code which runs $n \times m$ comparisons for each row, where $n$ is the number of columns and $m$ is the number of memorised rows. That's around 500 comparisons for each row with our current setup in the worst case scenario.


Figure out a way to perform data interpolation using values in previous and subsequent rows in Talend.

Make use of parallel processing where possible for increased performance.