---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://ikarus.ai/contact-us'>Get in touch for an API Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

search: true

code_clipboard: true
---

# Introduction

Welcome to the Allspark API documentation! You can use our API to access Allspark endpoints for uploading, processing & retrieving data. 
Currently we have examples in Shell. We will keep on adding examples from more languages.

In order to use these APIs, please feel free to <a href='https://ikarus.ai/contact-us'>visit our website</a> or write to us at <a href="mailto:info@ikarus.ai">info@ikarus.ai</a>

# API Key Generation

Please login to your <a href='https://allspark.ikarus.ai/'>Allspark</a> account and visit APIs section on the left to generate an API key. You can also configure additional settings like callback URL & IP whitelisting.

Allspark API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`API-KEY: dummyapikey`

<aside class="notice">
You must replace <code>dummyapikey</code> with your personal API key.
</aside>

# Callback URL

If you have setup callback URL in your API configuration, an API call will be made to your callback url with the data when a case is completely processed.

# Cases

## Direct Upload of File

```shell
curl -X POST \
  https://api-prod.ikarus.ai/api/v1/cases/direct-upload/ \
  -H 'API-KEY: dummyapikey' \
  -H 'content-type: multipart/form-data' \
  -F 'file=@/home/file.pdf'
```

> The above command returns JSON structured like this:

```json
{"case_id": 1}
```

This endpoint can be used to directly upload a file. A case is created after upload and subsequently processed. In scenarios, where a case consists of only one file, this API can be used.

### HTTP Request

`POST https://api-prod.ikarus.ai/api/v1/direct-upload/`

### Body Parameters

Parameter | Required | Description
--------- | ------- | -----------
file | true | Content-Type for file will be `multipart/form-data`


## Create Case

```shell
curl "curl -X POST \
  https://api-prod.ikarus.ai/api/v1/cases/ \
  -H 'API-KEY: dummyapikey'"
```

> The above command returns JSON structured like this:

```json
{"case_id": 2}
```

It is the alternative way to process a document. More suitable for scenarios where a case can have multiple files. Using this API we first create a case and then use subsequent APIs to upload files to the case and start processing.

### HTTP Request

`POST https://api-prod.ikarus.ai/api/v1/cases`


## File Upload

```shell
curl -X POST \
  https://api-prod.ikarus.ai/api/v1/cases/5/add-file/ \
  -H 'API-KEY: dummyapikey'\
  -H 'content-type: multipart/form-data' \
  -F 'file=@/home/file.pdf'"
```

> The above command returns JSON structured like this:

```json
{
  "status":"success",
  "message":"file successfully uploaded."
}
```

After creating a case through `Create Case` API, this API can be used to upload file to the case

### HTTP Request

`POST https://api-prod.ikarus.ai/api/v1/cases/{case_id}/add-file/`

### URL Parameters

Parameter | Description
--------- | -----------
case_id | Case ID to which file needs to be added

### Body Parameters

Parameter | Required | Description
--------- | ------- | -----------
file | true | Content-Type for file will be `multipart/form-data`

## Start Processing

```shell
curl -X POST \
  https://api-prod.ikarus.ai/api/v1/cases/5/mark-complete/ \
  -H 'API-KEY: dummyapikey'
```

> The above command returns JSON structured like this:

```json
{
  "status":"success",
  "message":"request accepted."
}
```

After all the files have been uploaded to the case through `File Upload` API, this API can be used to trigger processing for the case

### HTTP Request

`POST https://api-prod.ikarus.ai/api/v1/cases/{case_id}/mark-complete/`

### URL Parameters

Parameter | Description
--------- | -----------
case_id | Case ID which needs to be processed


## Get Case Detail

```shell
Curl command will be updated shortly.
```

> The above command returns JSON structured like this:

```json
Response will be updated shortly.
```

This API can be used to fetch data for a single case.

### HTTP Request

`GET https://api-prod.ikarus.ai/api/v1/cases/{case_id}`

### URL Parameters

Parameter | Description
--------- | -----------
case_id | Case ID for which data needs to be fetched


## Get Cases

```shell
Curl command will be updated shortly.
```

> The above command returns JSON structured like this:

```json
Response will be updated shortly.
```

This API can be used to fetch data for multiple cases at once using query parameters.

### HTTP Request

`GET https://api-prod.ikarus.ai/api/v1/cases/`

### Query Parameters

Parameter | Possible Values | Default Value | Description
--------- | --------------- | ------------- | -----------
order | `asc`,`desc` | | Order the response in ascending or descending order
status | `pending`,`completed` | | Only fetch the cases for mentioned state. It can also be a custom value.
sort_by | `case_id`,`created_at`,`updated_at` | | Sort the response by mentioned field
limit | An Integer Number | | Number of cases to be returned
offset | An Integer Number | | Number of cases to be skipped


## Get OCR Result

```shell
Curl command will be updated shortly.
```

> The above command returns JSON structured like this:

```json
Response will be updated shortly.
```

This API can be used to fetch raw OCR test of a file associated with any case.

### HTTP Request

`GET https://api-prod.ikarus.ai/api/v1/cases/{case_id}/ocr-output?file_name={file_name}`

### URL Parameters

Parameter | Description
--------- | -----------
case_id | Case ID associated with the file for which data needs to be fetched

### Query Parameters

Parameter | Description
--------- | -----------
file_name | File name for which data needs to be fetched 
