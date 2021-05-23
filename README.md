## Local Execution

### AWS Configure

### Local TF State

### Execution


## Team Execution

### IAM Role for terraform execution

### s3 bucket for TF state files

### Execution
* Login to Azure DevOps
* Setup Access Key and Secrete inside Azure Secrete create for Terraform role
* Run pipeline
    1. Check for S3 bucket to store the TF state file if does not exist then create one.
    2. Execute the terraform to spin up the infrastructure, Which will provide:
        1. Network load balancer (To deal with TCP requests)
        2. AWS Secret Manager to store the DynamoDB connection string and credentials
        3. Lambda (Serverless API Layer)
        4. DynamoDB (DB where timestamp is being written)
        5. Event bus (A scheduled event bus to trigger the lambda function to generate the custom metric for DB and Lambda)





### Misc (notes)

```json
    "/": {
      "function": "write_timestamp",
      "method": ["GET"],
      "path": "/",
      "description": "Application homepage"
    },
```




### OutBound to ephemeral port and 443 is extremely important on NACL

### Need hosted zone and register domain for multi-region fail-over of application layer.

### DynamoDB Global Table can handle multi-region at DB layer

### DynamoDB Endpoint access
    * Creation of endpoint
    * Enabling inbound access on Ephemral ports 1024 - 65355 for IPs ["52.94.24.0/23", "52.94.26.0/23", "52.94.5.0/24", "52.119.240.0/21"] <--- Important DynnamoDB specific AWS regional IPs
    * Outbound connection of internal pn 443