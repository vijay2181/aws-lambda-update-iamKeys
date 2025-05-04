# aws-lambda-update-iamKeys

```
issue:
To explain this as a recently faced issue, you can describe it like this:

"Recently, we encountered an issue where our application, which uses AWS KMS for chat encryption, started throwing an error during the encryption stage. The error message was:

botocore.exceptions.ClientError: An error occurred (UnrecognizedClientException) when calling the Encrypt operation: The security token included in the request is invalid.

After investigating, we found that this issue occurred because our IAM keys had been rotated as part of our scheduled key rotation policy, which happens every 60 days. The application was still using the old, expired credentials that were valid before the rotation. This caused the security token to be invalid during the encryption operation.

To resolve this, we updated the application to use the new IAM keys, which fixed the issue."



SOLUTION:
we need to update db with new iam keys when user rotated iam keys automatically/manually 
- when user rotates iam keys, it creates an event, we need to capture that event from cloud watch event bridge
- trigger lamba function for that event, where lambda function with python script updates the db with new iam keys
- DB create new record and mark flag active as true
- And old one mark as false
- If you're able to correlate with username
```
