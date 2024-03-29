# NativeScript Jumio

[nativescript-jumio](https://github.com/mattCCC/nativescript-jumio)

Jumio Mobile SDK plugin for NativeScript.

This plugin is compatible only with NativeScript 7.1+. Please file an issue or make a PR if you spot any problems or you have any further requests regarding the functionality.

Currently only ID verification is implemented. Please check [Usage](#usage) or demo/ directory for more details.

## Prerequisites / Requirements

Nativescript 7.1+ is required for the plugin to run properly.

## Installation

```javascript
tns plugin add nativescript-jumio

or

npm install nativescript-jumio
```

## Usage

[nativescript-jumio](https://www.npmjs.com/package/nativescript-jumio)

Make sure to include this activity inside the consumer's Android Manifest:

```
<activity
    android:theme="@style/Theme.Netverify"
    android:hardwareAccelerated="true"
    android:name="com.jumio.nv.NetverifyActivity"
    android:configChanges="orientation|screenSize|screenLayout|keyboardHidden" />
```


Ensure that Kotlin version is set to 1.4.30 inside gradle.properties file

kotlinVersion=1.4.30

```javascript
import { Jumio } from 'nativescript-jumio';

try {
    const jumio = new Jumio({
        merchantApiToken: 'YOUR_API_TOKEN',
        merchantApiSecret: 'YOUR_API_SECRET',
        datacenter: 'EU | US | SG',
    });

    jumio.init({
        customerId: 'customerId',
        callbackUrl: 'Custom callback URL',
        preSelectedData: {
            country: 'Alpha2 Country Code',
            documentType: 'passport | identity_card | driver_license | visa',
        },
        cancelWithError: (error) => {
            // User cancelled after error
        },
        finishInitWithError: (error) => {
            // Finished initialization with an error
        },
        finishedScan: (documentData, scanReference) => {
            // Scan is successful
        },
    });
} catch (err) {
    console.log("EXCEPTION", err)
}

```
## API

| Property | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| merchantApiToken | string | yes |  | API token |
| merchantApiSecret | string | yes |  | API secret |
| datacenter | string | yes | | Data Center to use
| customerId | string | yes | | Customer ID
| callbackUrl | string | No | | Custom Callback URL
| preSelectedData | Object | No | null | Pre-selected country as alpha2 code and document type
| cancelWithError | funct |  |  | Callback triggered when User cancels. It accepts error object with code and message. |
| finishInitWithError | funct |  |  | Callback triggered when initialization fails. It accepts error object with code and message. |
| finishedScan | funct |  |  | Callback triggered when scan is finished. It contains an extended Document Data with all necessary information about processing results. |

## License

Apache License Version 2.0, January 2004
