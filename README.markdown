### A fork of JSZip that aligns all files in generated ZIPs to 64 bits of the start, so that they can be accessed directly with `mmap`

The purpose is to ensure that all uncompressed data starts
with a particular alignment relative to the start of the file.  This
allows those portions to be accessed directly with mmap() even if they
contain binary data with alignment restrictions.
Some data needs to be word-aligned for easy access, others might benefit
from being page-aligned.  The adjustment is made by altering the size of
the "extra" field in the zip Local File Header sections.  Existing data
in the "extra" fields may be altered by this process.

### ORIGINAL README

JSZip [![Build Status](https://api.travis-ci.org/Stuk/jszip.svg?branch=master)](http://travis-ci.org/Stuk/jszip) [![Code Climate](https://codeclimate.com/github/Stuk/jszip/badges/gpa.svg)](https://codeclimate.com/github/Stuk/jszip)
=====

[![Selenium Test Status](https://saucelabs.com/browser-matrix/jszip.svg)](https://saucelabs.com/u/jszip)

A library for creating, reading and editing .zip files with JavaScript, with a
lovely and simple API.

See https://stuk.github.io/jszip for all the documentation.

```javascript
var zip = new JSZip();

zip.file("Hello.txt", "Hello World\n");

var img = zip.folder("images");
img.file("smile.gif", imgData, {base64: true});

zip.generateAsync({type:"blob"}).then(function(content) {
    // see FileSaver.js
    saveAs(content, "example.zip");
});

/*
Results in a zip containing
Hello.txt
images/
    smile.gif
*/
```
License
-------

JSZip is dual-licensed. You may use it under the MIT license *or* the GPLv3
license. See [LICENSE.markdown](LICENSE.markdown).
