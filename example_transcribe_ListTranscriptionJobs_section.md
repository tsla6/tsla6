# List Amazon Transcribe transcription jobs using an AWS SDK<a name="example_transcribe_ListTranscriptionJobs_section"></a>

The following code examples show how to list Amazon Transcribe transcription jobs\.

------
#### [ JavaScript ]

**SDK for JavaScript V3**  
Create the client\.  

```
const { TranscribeClient } = require("@aws-sdk/client-transcribe");
// Set the AWS Region.
const REGION = "REGION"; //e.g. "us-east-1"
// Create anAmazon EC2 service client object.
const transcribeClient = new TranscribeClient({ region: REGION });
export { transcribeClient };
```
List transcription jobs\.  

```
// Import the required AWS SDK clients and commands for Node.js

import { ListTranscriptionJobsCommand } from "@aws-sdk/client-transcribe";
import { transcribeClient } from "./libs/transcribeClient.js";

// Set the parameters
export const params = {
  JobNameContains: "KEYWORD", // Not required. Returns only transcription
  // job names containing this string
};

export const run = async () => {
  try {
    const data = await transcribeClient.send(
      new ListTranscriptionJobsCommand(params)
    );
    console.log("Success", data.TranscriptionJobSummaries);
    return data; // For unit tests.
  } catch (err) {
    console.log("Error", err);
  }
};
run();
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javascriptv3/example_code/transcribe#code-examples)\. 
+  For more information, see [AWS SDK for JavaScript Developer Guide](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/transcribe-examples-section.html#transcribe-list-jobs)\. 
+  For API details, see [ListTranscriptionJobs](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-transcribe/classes/listtranscriptionjobscommand.html) in *AWS SDK for JavaScript API Reference*\. 

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
def list_jobs(job_filter, transcribe_client):
    """
    Lists summaries of the transcription jobs for the current AWS account.

    :param job_filter: The list of returned jobs must contain this string in their
                       names.
    :param transcribe_client: The Boto3 Transcribe client.
    :return: The list of retrieved transcription job summaries.
    """
    try:
        response = transcribe_client.list_transcription_jobs(
            JobNameContains=job_filter)
        jobs = response['TranscriptionJobSummaries']
        next_token = response.get('NextToken')
        while next_token is not None:
            response = transcribe_client.list_transcription_jobs(
                JobNameContains=job_filter, NextToken=next_token)
            jobs += response['TranscriptionJobSummaries']
            next_token = response.get('NextToken')
        logger.info("Got %s jobs with filter %s.", len(jobs), job_filter)
    except ClientError:
        logger.exception("Couldn't get jobs with filter %s.", job_filter)
        raise
    else:
        return jobs
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/transcribe#code-examples)\. 
+  For API details, see [ListTranscriptionJobs](https://docs.aws.amazon.com/goto/boto3/transcribe-2017-10-26/ListTranscriptionJobs) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, including help getting started and information about previous versions, see [Using this service with an AWS SDK](getting-started-sdk.md#sdk-general-information-section)\.