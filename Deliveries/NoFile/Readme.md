Navigate: [ApiDoc](../../Readme.md) / [Delivery](../Readme.md) / Delivery with no file

# Delivery with no file.

The delivery endpoint can be used to upload a large file, that is to be processed by FarPay.
Such scenarios are applicable when handling large files, that oterwise would result in
timeout, and durable processing time.

## Step 1: Create the delivery

Post into delivery

```
    POST https://api.farpay.io/v2/deliveries
```

Body:
```JSON
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

  "Id": 1,
  "Created": "2023-04-14T13:09:40.0750166+00:00",
  "DeliveryType": "FarPayXmlType",
  "DeliveryStatus": "PendingFile",
  "ErrorMessage": null,
  "FileUploadUri": "https://farpay.blob.core.windows.net/deliverytemp/1236f5ed-78a4-4934-9404-f0e8c582ef64?sv=2020-08-04&spr=https&se=2023-04-14T13:39:40Z&sr=b&sp=cw&sig=LPfLFrCvl3A7I3ldD7bH7K/KVAgNJs3MEbi82/jgxkY="
}
```

## Step 2: Put the file into the blob storage

* Convert the file contents to Bas64
* Create a request
  * Set `x-ms-blob-type` to `blockblob`
  * `PUT` the contents of the file to `FileUploadUri`
* Received an HTTP Created (201)

**Remark!** The file needs to be formated as a Base64 format, that is put into the blob storage.


### Request example
```javascript
// Example of how to upload a file to the blob storage

$(function() {
    var request = require('request');
    var fs = require('fs');
    var file = fs.readFileSync('MyFile.xml');
    var base64 = Buffer.from(file).toString('base64');
    var options = {
        method: 'PUT',
        url: 'https://farpay.blob.core.windows.net/deliverytemp/1236f5ed-78a4-4934-9404-f0e8c582ef64?sv=2020-08-04&spr=https&se=2023-04-14T13:39:40Z&sr=b&sp=cw&sig=LPfLFrCvl3A7I3ldD7bH7K/KVAgNJs3MEbi82/jgxkY=',
        headers: {
            'x-ms-blob-type': 'blockblob',
            'Content-Type': 'application/octet-stream',
            'Content-Length': Buffer.byteLength(base64)
        }
    };

    // Execute the request with JSON:
    options.body = base64;
    request(options, function (error, response, body) {
        if (error) throw new Error(error);
         console.log(body);
    });
});
```


