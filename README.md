# barcode-detector-polyfill

Polyfill for the Barcode Detection API based on [Dynamsoft Barcode Reader](https://www.dynamsoft.com/barcode-reader/overview/).

[Online demo](https://extraordinary-taiyaki-4769a5.netlify.app/)

## Include the library

1. Via CDN:

    ```html
    <script src="https://cdn.jsdelivr.net/npm/dynamsoft-javascript-barcode@9.0.2/dist/dbr.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/barcode-detection@latest/dist/barcode-detector.umd.js"></script>
    ```

2. Via npm:

    ```
    npm install barcode-detection
    ```
    
    Then import the package:
    
    ```
    import {default as BarcodeDetectorPolyfill} from "barcode-detection"    
    ```

## Usage

```js
let barcodeDetector;

async function init() {
  if ("BarcodeDetector" in window) {
    alert('Barcode Detector supported!');
  }else{
    alert('Barcode Detector is not supported by this browser, using the Dynamsoft Barcode Reader polyfill.');
    
    //initialize the Dynamsoft Barcode Reader with a license
    BarcodeDetectorPolyfill.setLicense("DLS2eyJoYW5kc2hha2VDb2RlIjoiMjAwMDAxLTE2NDk4Mjk3OTI2MzUiLCJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSIsInNlc3Npb25QYXNzd29yZCI6IndTcGR6Vm05WDJrcEQ5YUoifQ==");
    await BarcodeDetectorPolyfill.init();
    window.BarcodeDetector = BarcodeDetectorPolyfill;
    
  }
  barcodeDetector = new window.BarcodeDetector({ formats: ["qr_code"] });
}

async function decode(imgEl) {
  //decode an image element
  let barcodes = await barcodeDetector.detect(imgEl);
}
```

You can apply for a license [here](https://www.dynamsoft.com/customer/license/trialLicense?product=dbr).

## Supported Barcode Symbologies

* Code 11
* Code 39
* Code 93
* Code 128
* Codabar
* EAN-8
* EAN-13
* UPC-A
* UPC-E
* Interleaved 2 of 5 (ITF)
* Industrial 2 of 5 (Code 2 of 5 Industry, Standard 2 of 5, Code 2 of 5)
* ITF-14 
* QRCode
* DataMatrix
* PDF417
* GS1 DataBar
* Maxicode
* Micro PDF417
* Micro QR
* PatchCode
* GS1 Composite
* Postal Code
* Dot Code
* Pharmacode

