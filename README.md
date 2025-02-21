# Project: Document Handling Using Amazon Textract and Amazon Polly
Date:  2025-02-20

## Description
This procedure outlines the steps to extract text from a sample document using Amazon Textract, convert the extracted text into MP3 audio format using Amazon Polly, and use an AWS Lambda function to automate the process. The final step verifies the generated MP3 file in an Amazon Simple Storage Service (Amazon S3) bucket.

## Objectives
- Extract and view raw text from a sample document.
- Convert the extracted text into MP3 audio format.
- Run an AWS Lambda function to convert an image file containing text into an MP3 audio file.

## Tools Used
- AWS Textract
- AWS Polly
- AWS S3
- AWS Lambda
  
---

## Architecture Diagram
<img src="https://imgur.com/LdL5mQs.jpg" height="80%" width="80%" alt="Architecture Diagram"/>

---

## Begin: Open the AWS Console
<img src="https://imgur.com/mzb2xM0.jpg" height="80%" width="80%" alt="Open AWS Console"/>

---

## Step 1: Extract Text Using Amazon Textract
**Concept:** Amazon Textract is a machine learning (ML) service that automatically extracts text, handwriting, layout elements, and data from scanned documents.

1. Navigate to the [Amazon Textract console](https://console.aws.amazon.com/textract/).
2. In the left navigation pane, click **Analyze Document**.
3. On the Analyze Document page, explore the extracted information by clicking the available tabs.
4. Proceed to the next step.

<img src="https://imgur.com/ztNO5EI.jpg" height="80%" width="80%" alt="Navigate to Textract and View Formats"/>

---

## Step 2: Convert Text to Speech Using Amazon Polly
**Concept:** Amazon Polly uses deep learning technologies to synthesize natural-sounding speech, enabling the conversion of text into audio.

1. Navigate to the [Amazon Polly console](https://console.aws.amazon.com/polly/).
2. In the left navigation pane, select **Text-to-Speech**.
3. Review the history of completed S3 synthesis tasks under the **Text-to-Speech** section.
4. Click **Listen** to preview the synthesized audio.
5. Proceed to the next step.

<img src="https://imgur.com/AQzXBtm.jpg" height="80%" width="80%" alt="Navigate to Polly and test Polly"/>

---

## Step 3: Access the Amazon S3 Bucket
**Concept:** Amazon S3 is an object storage service providing scalability, data availability, security, and performance.

1. Navigate to the [Amazon S3 console](https://console.aws.amazon.com/s3/).
2. On the **General purpose buckets** tab, click the S3 bucket name that begins with `labdatabucket-`.
3. Proceed to the next step.

<img src="https://imgur.com/oQtTPS4.jpg" height="80%" width="80%" alt="Navigate to S3 to select Bucket"/>

---

## Step 4: Review the Sample Document
**Concept:** Amazon S3 allows storage of large volumes of data, with individual objects ranging from 0 bytes to 5 TB.

1. In the **Objects** tab, locate and review the JPEG file.
2. Proceed to the next step.

<img src="https://imgur.com/yWsfSc3.jpg" height="80%" width="80%" alt="Review file"/>

---

## Step 5: Locate the AWS Lambda Function
**Concept:** The AWS Lambda **Functions** page lists all functions in the current AWS Region. Recently created functions may take some time to appear.

1. Navigate to the [AWS Lambda console](https://console.aws.amazon.com/lambda/).
2. In the left navigation pane, click **Functions**.
3. Under the **Functions** section, select the function named **TextToSpeech**.
4. Proceed to the next step.

---

## Step 6: Review the Lambda Function Code
**Concept:** Use the `DetectDocumentText` API operation to extract text from documents with Amazon Textract.

1. Scroll to the **Code source** section.
2. In the **Code** tab, review the `lambda_function.py` file:
   - **Line 4:** References an environment variable for the S3 bucket name.
   - **Lines 12 and 29:** Utilize the `detect_document_text` and `start_speech_synthesis_task` API calls. End user has the ability to modify `VoiceID` and `Engine` parameters.
3. Click the **Test** tab.
4. Proceed to the next step.

<img src="https://imgur.com/QNgVh94.jpg" height="80%" width="80%" alt="Text to speech code review in Lambda"/>

---

## Step 7: Create a Test Event
**Concept:** Events serve as inputs to AWS Lambda functions. Up to 10 test events can be created per function.

1. In the **Event name** field, enter: `TextToSpeechTest`.
2. Click **Save**.
3. Proceed to the next step.

<img src="https://imgur.com/GzKLogV.jpg" height="80%" width="80%" alt="Create Lambda function"/>

---

## Step 8: Execute the Test Event
**Concept:** Running a test event synchronously invokes the Lambda function with the provided input.

1. Click **Test** to execute the event.
2. Proceed to the next step.

<img src="https://imgur.com/3pFCke7.jpg" height="80%" width="80%" alt="Test Lambda function"/>

---

## Step 9: Verify the Speech Synthesis Task
**Concept:** The `start_speech_synthesis_task` API call asynchronously converts the extracted text into an MP3 file.

1. In the **Details** section, review the `taskId`.
2. Under **Log output**, verify the extracted text from the image file.
3. Proceed to the next step.

<img src="https://imgur.com/MnbAURb.jpg" height="80%" width="80%" alt="Verify Lambda function"/>

---

## Step 10: Download and Listen to the MP3 File
**Concept:** Amazon Polly provides synthesized speech in formats like MP3 and Ogg Vorbis, suitable for web and mobile applications.

1. In the [Amazon S3 console](https://console.aws.amazon.com/s3/), navigate to the `labdatabucket` bucket.
2. Under the **Objects** tab, select the checkbox next to the generated MP3 file.
3. Click **Download**.
4. Open the file with a local audio player to listen to the converted text.
5. **Process complete.**

<img src="https://imgur.com/7VJkMYG.jpg" height="80%" width="80%" alt="Download file from S3"/>
<img src="https://imgur.com/pCZIJzA.jpg" height="80%" width="80%" alt="Test of downloaded MP3 file from AWS"/>
