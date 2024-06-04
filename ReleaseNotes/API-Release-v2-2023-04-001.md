navigate: [ApiDoc](../Readme) / [Release notes](Readme.md) / API-Release-v2-2023-04-001

# API-Release-v2-2021-11-001
This document describes the release of FarPay API v2, 17th of November 2021

# Release state
Release information in the table below.

| Value            | description                                  |
|------------------|----------------------------------------------|
| Environment      | `Staging`                                    |
| Url              | https://farpay-api-staging.azurewebsites.net |
| Expected release | 3rd of May                                   |

## Version control TAG
`API-v.2.0.5` (Committed 14th of April 2023, 10:14 (by Theodor E. Johannesen), Commit message (SHA: 806b533)

## Feedback
If you have any comments, please reachout to support@farpay.dk and #farpaydev on #slack.

## Document history

| state     | author             | timestamp   | description     |
|-----------|--------------------|-------------|-----------------|
| `Initial` | @theodorjohannesen | 2023-apr-14 | Initial version |

## About
The release, holds following changes:
* XML Requests hold API accountable to deliver XML based content.
* `Delveries` endpoint can handle large files

## Breaking changes.
No braking changes will occur - focus is scaling with larger files in deliveries.

## XML Values
As the system is based on Swagger, and testable through the https://api.farpay.io endpoint, we have been focusing on a test-framework, that have given us a media transparency, so that the tests did not capture the JSON as well as XML responses.

## Deliveries endpoint

### With a base64 file
In the common scenario, a Base64 file is attached as a `string` to the file-node. Example:
```javascript
{
  "DeliveryType": "Invoice",
  "DeliveryFormat": "XML",
  "File": {
    "Filename": "MyFile.xml",
    "Data": "ewogICJKb2IiIDogIklmIHlvdSBhcmUgbG9va2luZyBmb3IgYSBqb2IsIHBsZWFzZSBjb250YWN0IHVzIiwKICAiQ29udGFjdCIgOiAiYmhhQGZhcnBheS5kayBvciB0ZWpAZmFycGF5LmRrIgp9"
  }
}
  
```
Where the response is a confirmation of receiving the file:

```javascript
{
  "Id": nnnnnnnn,
  "Created": "2023-04-14T09:21:44.270Z",
  "DeliveryType": "Invoice",
  "DeliveryStatus": "New",
  "ErrorMessage": "<when an error, it is written here>",
  "FileUploadUri": "null"
}

```

### With no file
When no filedata is set, the result is an url, that can be used, to upload the file to.

```javascript
{
  "DeliveryType": "Invoice",
  "DeliveryFormat": "XML",
  "File": {
    "Filename": "MyFile.xml",
    "Data": null
  }
}
  
```
Where the response is a confirmation of receiving the file:

```javascript
{

  "Id": 88460475,
  "Created": "2023-04-14T13:09:40.0750166+00:00",
  "DeliveryType": "FarPayXmlType",
  "DeliveryStatus": "PendingFile",
  "ErrorMessage": null,
  "FileUploadUri": "https://farpay.blob.core.windows.net/deliverytemp/1236f5ed-78a4-4934-9404-f0e8c582ef64?sv=2020-08-04&spr=https&se=2023-04-14T13:39:40Z&sr=b&sp=cw&sig=LPfLFrCvl3A7I3ldD7bH7K/KVAgNJs3MEbi82/jgxkY="

}
```
**Upload the file**
1. Grab the url in `FileUploadUri`
2. Get hold of your file
3. Read the binary content of the file
4. Set the header `x-ms-blob-type`: `blockblob`
5. `PUT` binary content to the url.
6. Received an HTTP Created (201)

You have now completed an upload, and the file will now be processed accordingly. In order to see the orderstatus, You can always request the status of the order in the `GET` `Orders/{id}` endpoint.



```
Cheers from FarPay devteam!
This is coded with ❤️ and ☕.

tHe0d0r.
```
