navigate: [ApiDoc](README.md) / [Release notes](Readme.md) / API-Release-v2-2023-04-001

# API-Release-v2-2021-11-001
This document describes the release of FarPay API v2, 17th of November 2021

## Version control TAG
`API-v.2.0.5` (Committed 14th of April 2023, 10:14 (by Theodor E. Johannesen), Commit message (SHA: 806b533)

## Feedback
If you have any comments, please reachout to support@farpay.dk and #farpaydev on #slack.

## Document history

state         | author             | timestamp   | description
--------------|--------------------|-------------|--------------------
`Initial`     | @theodorjohannesen | 2023-apr-14 | Initial version

## About
The release, holds following changes:
* XML Requests hold API accountable to deliver XML based content.
* `Delveries` endpoint can handle large files
* 

## Breaking changes.
No braking changes will occur - focus is scaling with larger files in deliveries.

## XML Values
As the system is based on Swagger, and testable through the https://api.farpay.io endpoint, we have been focusing on a test-framework, that have given us a media transparency, so that the tests did not capture the JSON as well as XML responses.

## Deliveries endpoint

### With a base64 file
In the common scenario, a Base64 file is attached as a `string` to the file-node. Example:
```
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

```
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

```
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

```
{

  "Id": 88460475,
  "Created": "2023-04-14T13:09:40.0750166+00:00",
  "DeliveryType": "FarPayXmlType",
  "DeliveryStatus": "PendingFile",
  "ErrorMessage": null,
  "FileUploadUri": "https://farpay.blob.core.windows.net/deliverytemp/1236f5ed-78a4-4934-9404-f0e8c582ef64?sv=2020-08-04&spr=https&se=2023-04-14T13:39:40Z&sr=b&sp=cw&sig=LPfLFrCvl3A7I3ldD7bH7K/KVAgNJs3MEbi82/jgxkY="

}

```
## Upload the file
To upload content to the `FileUploadUri`, you need to `PUT` binary content to the url.



```
Cheers from FarPay devteam!
This is coded with ❤️ and ☕.

tHe0d0r.
```
