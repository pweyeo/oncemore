---
title: "Understanding Filters"
description: "Doks is a Hugo theme helping you build modern documentation websites that are secure, fast, and SEO-ready — by default eyeo."
lead: "Use this library to integrate eyeo's Ad Blocking Core for Chromium and Firefox Extensions."
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "filters"
weight: 100
toc: true
---

## Getting started

Before you begin building your extension, make sure to download the libraries you'll need and configure the `manifest.json` file.

### Downloading the libraries


The Web Extension (WebExt) library comes in two parts, which you'll need to include in the extension's background page:

* `ewe-api.js`
* `ewe-content.js`

Make sure you've downloaded [the latest builds](https://gitlab.com/eyeo/webext/webext-sdk/-/jobs/1568206051/artifacts/browse/dist) of both.


### Configuring the manifest file

Your extension's `manifest.json` file needs the following configuration:

```json
{
  "manifest_version": 2,
  "background": {
    "scripts": [
      "ewe-api.js"
    ]
  },
  "content_scripts": [
    {
      "all_frames": true,
      "js": [
        "ewe-content.js"
      ],
      "match_about_blank": true,
      "matches": [
        "http://*/*",
        "https://*/*"
      ],
      "run_at": "document_start"
    }
  ],
  "permissions": [
    "webNavigation",
    "webRequest",
    "webRequestBlocking",
    "unlimitedStorage",
    "<all_urls>"
  ]
}
```


<!--{{< alert icon="👉" text="The Tutorial is intended for novice to intermediate users." />}}

Step-by-step instructions on how to start a new Doks project. [Tutorial →](https://getdoks.org/tutorial/introduction/)-->

## Quick Start

{{< alert icon="👉" text="For installation, make sure you have Node 12.18.4 or higher on your system." />}}

### Installing dependencies

Now that you've downloaded the libraries and configured the `manifest.json` file, run the following command to update and install the dependencies.

```
npm install
```

### Building the library

Next, run the following command to build the libraries.

```
npm run build
```

### Linting your code

To lint your code, run the following command.

```
npm run lint
```

### Starting the build

Lastly, to start the extension build, run the following command.

```
npm start
```

### Blocking ads

With the libraries and dependencies installed, you're now ready to start blocking ads.  

Access the API in your own background scripts through the
global `EWE` object. Call `EWE.start()` to start blocking ads.

## Testing your extension

Now that you've got an extension up and running, be sure to test it to ensure it's functioning as expected.

### Serving test pages

Whether you manually load the test extension or use the test runner, the test suite requires locally served test pages.  Run them with the following command.

```
npm run test-server
```

### Using the test extension

The test extension is built on both the `/dist/test-mv2` and `/dist/test-mv3` folders.  You can load both folders as unpacked extensions under `chrome://extensions` in Chromium-based browsers, and under `about:debugging` in Firefox.

Once you've loaded the extension, the test suite opens in a new tab.  To test the API manually through the global `EWE` object, you can inspect your extension's background page.

Keep the following in mind when testing your extension:

* `test-mv2` contains a Manifest Version 2 extension, and `test-mv3` contains a [Manifest Version 3](https://developer.chrome.com/docs/extensions/mv3/intro/) extension.
* For popup tests, disable your browser's built-in popup blocking on `localhost`.

#### Test options

* The `timeout` option overrides the per-test timeout in milliseconds.
* The `grep` uses a regular expression to filter the tests to be run.

#### Using the test runner

Run the following command to enable the test runner.

```
npm test -- {v2|v3} {chromium|firefox|edge} [version|channel] [options]
```

#### Testing the bundle

Run the following command to make sure users can import and re-bundle your code.

```
npm run test-bundle
```

## Going further

With your build running, you may want to consider other features available for your extension.

### Module bundlers

Because `ewe-api.js` runs as a Universal Module Definition (UMD) module, you can use it with module bundlers.

If you use a module bundler, omit `ewe-api.js` from your `manifest.json` file.  As a result, your build won't contain a global `EWE` object.

Review the following snippets to see the `ewe-api.js` as both a CommonJS and ESM module.

#### CommonJS

```javascript
const EWE = require("./ewe-api.js");
EWE.start();
```

#### ESM

```javascript
import * as EWE from "./ewe-api.js";
EWE.start();
```

### Supporting snippet Filters

To enable support for [snippet filters](https://help.eyeo.com/adblockplus/snippet-filters-tutorial), download the [snippets library](https://gitlab.com/eyeo/adblockplus/abp-snippets) and make it available to the `EWE` object with the following command:

```javascript
let response = await fetch("snippets.js");
let code = await response.text();
EWE.snippets.setLibrary(code);
```

### Incorporating machine learning models

You'll find a `models` folder included with the library bundles you downloaded.  To support machine learning enabled snippets, make sure to include the `models` folder and its contents in your extension bundle.  Include the folder in the same directory as `ewe-api.js`.

{{< alert icon="👉" text="Machine learning enabled snippets are optional, though without them, your extension cannot make use of our machine learning models." />}}

### What next?

Looking to dive even deeper?  Check out our API documentation next. [API Docs →](#)


## Help

Need help?  Reach out to our team for support. [Support →]({{< relref "#" >}})
