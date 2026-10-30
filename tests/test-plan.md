# Test Plan — Serverless Image Processing Pipeline

This is an acceptance-test plan. Mark tests as passed only after execution in the AWS account and retain sanitized evidence.

| ID | Test | Expected result | Actual result | Evidence |
|---|---|---|---|---|
| T01 | Upload valid JPEG/PNG using a pre-signed URL | Upload succeeds and job reaches `COMPLETED` | Not run | Add screenshot/log |
| T02 | Inspect thumbnail and processed output | Dimensions and selected frame/watermark are correct | Not run | Add output images |
| T03 | Upload unsupported/invalid file | Validation rejects it safely; status becomes `FAILED` | Not run | Add execution log |
| T04 | Replay same S3 event | Idempotency prevents duplicate side effects/notifications | Not run | Add DynamoDB/job evidence |
| T05 | Simulate transient processing error | Retry runs and job can complete after recovery | Not run | Add Step Functions history |
| T06 | Force repeated failure | Message moves to DLQ and alarm fires | Not run | Add SQS/DLQ screenshot |
| T07 | Attempt public S3 access | Direct public access is denied | Not run | Add access-denied evidence |
| T08 | Use expired pre-signed URL | Upload is rejected | Not run | Add request result |
| T09 | Upload a burst of images | SQS buffers work and backlog drains as processing scales | Not run | Add CloudWatch/SQS metrics |
| T10 | Trigger workflow error | Logs, metrics, and notification are available | Not run | Add CloudWatch/SNS evidence |

## Evidence Checklist

- [ ] Sanitized screenshots of S3 source and destination buckets.
- [ ] API Gateway upload endpoint and Lambda configuration.
- [ ] SQS work queue, DLQ, and redrive settings.
- [ ] Step Functions workflow execution history.
- [ ] DynamoDB metadata record.
- [ ] CloudFront distribution and OAC configuration.
- [ ] CloudWatch dashboard/alarms.
- [ ] Test outcomes and any corrective actions.
- [ ] Cost observations or estimate for the selected Region and test workload.
