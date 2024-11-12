# Deliveries
This endpoint supports slipping XML file-payloads as files into FarPay, simular to the SFTP connection.
With this endpoint you can ship off a file, with filename and content.

The Use-Case scenarios are:
* Insert a new delivery with an attached file
* Get the existing delivery (Status and details)
* Get a collection of deliveries, filtered by status, start- and enddate.


Remark that [all requests must have](../Common/Readme) an `X-API-KEY`, and a `Accept` mentioned in the header of the request.

# Insert a new Delivery
Use `POST` to the endpoint `https://api.farpay.io/{version}/deliveries` to insert a file with following data:

## Parameters
There are two parameters, that are governing the inserted type.

### DeliveryFormat
| Value               | Description                     |
|---------------------|---------------------------------|
| `xml`  or  `oioxml` | XML format                      |
| `601`               | BS Payment file                 |
| `605`               | BS Agreement                    |
| `rd07`              | Domestic format (Faroe Islands) |
| `farpayxml`         | FarPay propritary format        |

*Remark!* The if the format is not set in the request, the receiver will try to determine the format of the attached file.
It will do a right classification if the file has a rootnode of `agreements` or `statement` or `bill`.





As JSON:
```javascript
{
  "DeliveryType": "TransmissionReceipt",
  "File": {
    "Filename": "mySuperFileName.xml",
    "Data": "<base64 file content>"
  }
}
```

As XML:
```xml
<?xml version="1.0"?>
<Delivery>
  <DeliveryType>TransmissionReceipt</DeliveryType>
  <File>
    <Filename>mySuperFileName.xml</Filename>
    <Data>base64-fileContent</Data>
  </File>
</Delivery>
```

When the data has successfully posted into the endpoint, the result is a ```Delivery``` that is presented by following:

```javascript
{
  "Id": <unique fileId>,
  "Created": "2018-10-02T16:19:42.001Z",
  "DeliveryType": "TransmissionReceipt",
  "DeliveryStatus": "New", "Processing" "Ok" | "Error",
  "ErrorMessage": "<Description of the error>" | ""
}
```

# Get the existing delivery
This endpoints gives you an elaborated detail of the delivery, including the file data if wanted.
A single delivery is available as `GET` from `https://api.farpay.io/{version}/deliveries/{deliveryId}?includeFile=false` or 
`https://api.farpay.io/{version}/deliveries/{deliveryId}?includeFile=true`

The ```File``` is null when not included in the request

```javascript
{
  "Id": <unique delivery id>,
  "DeliveryFormat": "string",
  "DeliveryStatus": "string",
  "ErrorMessage": "string",
  "DeliveryType": "string",
  "File": {
    "Filename": "string",
    "Data": "<64 based string of the file content>" 
  } | null
}
```

# Get a collection of deliveries
The collection is wrapped in a container, that in addition the the collection of deliveries, holds the
count of how many deliveries you have retreived.
The endpoint is available from a `GET` from `https://api.farpay.io/{version}/deliveries`
with the optional filters of:
* `status`
* `fromDate`
* `toDate`

Example a return container:

```
{
  "DeliveryReferences": [
          "Id": 1234,
      "Created": "2018-10-12T04:46:33",
      "DeliveryType": "FarPayXmlType",
      "DeliveryStatus": "Error",
      "ErrorMessage": "Line number 1 Current format is ither not set or not supported. Please make sure that the PrepareFactory method is called"
    },
    {
      "Id": 1235,
      "Created": "2018-09-05T11:02:20.00",
      "DeliveryType": "FarPayXmlType",
      "DeliveryStatus": "Ok",
      "ErrorMessage": ""
    },
  ],
  "Count": 2
}
```
