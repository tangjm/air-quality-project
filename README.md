# air-quality-project

### Final tech stack

- S3
- Talend
- QuickSight
### Tech stack

-	Amazon RDS
-	Amazon S3
-	Amazon Quicksight (Tableau as a backup)
-	Talend (KNIME as a backup)

### Serverless stck

S3 + Lambda
#### Data flow
1. Upload file to S3
2. Use Talend to access S3
3. Clean data in Talend
4. Upload updated file to S3
5. Serve the S3 Bucket as a REST API end point using AWS Lambda
6. Users can use HTTP(S) requests to access the file object in S3

S3 + Redshift + QuickSight

1. Upload file to S3
2. Use Talend to access S3
3. Clean data in Talend
4. Connect Redshift to S3
5. Connect QuickSight to Redshift
6. Users can use SQL queries in QuickSight to visualise data. 

S3 + Talend + QuickSight

1. Upload file to S3
2. Use Talend to access S3
3. Clean data in Talend
4. Upload cleaned data to S3
5. Use QuickSight to query data in S3