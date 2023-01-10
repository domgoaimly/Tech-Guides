## Create S3 Bucket
**For static resources**

### Create a new bucket
   * Need bucket name and AWS Region
   * Everything is default

### Create a new Policy
   * Create a new policy ‘bucketname-access’
   * Service ‘s3’
   * Actions
     - Read ‘GetObject
     - Write ‘PutObject’ ‘DeleteObject’
   * Resources
   * Add ARN
     - bucket name
     - Object name: any

### Create a IAM User
   * Represents the web app
   * username: aimly-web-test’
   * access type: access key - programmatic access
   * attach policy ‘bucketname-access’
   * get the access key id and secret access key
