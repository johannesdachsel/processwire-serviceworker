# ProcessWire ServiceWorker

This is a simple module that provides a [Service Worker](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers) for viewing Processwire pages offline. It’s heavily based on the work of [Jeremy Keith](https://adactio.com) – thank you Jeremy!

## How it works

When a people visit your site and their [browser supports the use of service workers](http://caniuse.com/#feat=serviceworkers), a small JavaScript (the service worker) gets installed in their browser. The script sits in the background, intercepts network requests and then does the following:

If the requested resource is an HTML document:

1. try and fetch the page from the network
2. if that doesn’t work, try and serve the page from the cache
3. if that also fails, fall back to a specified offline page

If the requested resource is a file:

1. try and serve the file from the cache (if available)
2. if the file is not in the cache, try and request it from the network
3. if everything else fails and the requested file is an image, show a placeholder

## Installation

Copy the module directory to /site/modules/, then in Processwire Admin go to Modules > Site > Add New, click “Refresh” and install the ServiceWorker module.

During the installation, the module copies a PHP file (`serviceworker.js.php`) to your Processwire root directory. This file is served as JavaScript and contains the actual Service Worker.

## Configuration

The module offers a few configuration options:

* __Current cache version:__ cache version number. You can force the service worker to upgrade the cached pages and static assets by bumping this to a higher number. Also, the module bumps the version automatically when one of the configured offline pages is saved.
* __Max. pages in cache:__ the number of pages that can live in the page cache
* __Max. images in cache:__ the number of images that can live in the image cache
* __Offline page:__ a page that is served when the user agent has no connection to the network.
* __Additional pages to cache:__ other pages that are cached upfront when the service worker gets installed.
* __Static assets to cache:__ any static assets that need to be cached when the service worker gets installed.

## Usage

To include the service worker in your templates use `<?php $modules->get('ServiceWorker')->renderJavaScript(); ?>`.

## License

Licensed under a CC0 1.0 Universal (CC0 1.0) Public Domain Dedication

[http://creativecommons.org/publicdomain/zero/1.0/](http://creativecommons.org/publicdomain/zero/1.0/)

