# air-quality-project

### Tech stack

-	Amazon RDS
-	Amazon S3
-	Amazon Quicksight (Tableau as a backup)
-	Talend (KNIME as a backup)


### Serverless stck

- S3
- Lambda

#### Data flow
1. Upload file to S3
2. Use Talend to access S3
3. Clean data
4. Upload updated file to S3
5. Serve the S3 Bucket as a REST API end point using AWS Lambda
6. Users can use HTTP(S) requests to access the file object in S3
