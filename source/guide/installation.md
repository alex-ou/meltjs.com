---
title: Installation
type: guide
order: 1
dev_size: "90.18"
min_size: "36.74"
gz_size: "10.93"
---
<div id="downloads">
<a class="button" href="/js/meltjs.js" download>Development Version</a><span class="light info">{{dev_size}}kb</span>

<a class="button" href="/js/meltjs.min.js" download>Production Version</a><span class="light info">{{gz_size}}kb min+gzip</span>
</div>

## NPM
```bash
# latest stable
$ npm install meltjs
```

## Using a CDN
Both the development and the minified production version are hosted on [unpkg](https://unpkg.com).

Development version:
```html
<script src="https://unpkg.com/meltjs"></script>
```

Minified production version:
```html
<script src="https://unpkg.com/meltjs/dist/melt.min.js"></script>
```