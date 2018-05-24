# Gamma Quadrant Web

## Introduction

Website for Gamma Quadrant

## Contents

- [Dev](#dev)
- [Build](#build)
- [Upload](#upload)
- [Credits](#credits)

## Dev

```bash
open http://localhost:8000
python -m SimpleHTTPServer
```

## Build



```bash
# Cache all sources locally, one time
while read -r url; do
	echo "Fetching: $url"
	curl -o "$(basename $url)" "$url"
done <<< "$(grep src < source-sans-pro.css | cut -d ',' -f 3 | cut -d ' ' -f 2 | sed 's|url(||g' | sed 's|)||g')"

# Install
npm install uglify-js html-minifier csso-cli -g

# Clean
rm assets/js/min.js

# Run CSS
sed 's|@import url(.*||g' < assets/css/main.css > assets/css/tmp.css
cat assets/css/tmp.css assets/css/font-awesome.min.css assets/css/source-sans-pro.css | csso > assets/css/min.css
rm assets/css/tmp.css

# Run JS & HTML
uglifyjs --compress --mangle -o assets/js/min.js -- assets/js/*.js
html-minifier  --collapse-boolean-attributes --collapse-whitespace --decode-entities --html5 --process-conditional-comments --remove-attribute-quotes --remove-comments --remove-empty-attributes --remove-optional-tags --sort-attributes --sort-class-name --trim-custom-fragments --use-short-doctype index.raw.html > index.html
```

## Upload

```bash
export AWS_PROFILE=gamma-quadrant
aws s3 cp   index.html s3://gammaquadrant.io/index.html --acl public-read
aws s3 sync assets/    s3://gammaquadrant.io/assets/    --acl public-read
aws s3 sync images/    s3://gammaquadrant.io/images/    --acl public-read
```

## Credits

- `Dimension` by [HTML5 UP](https://html5up.net/)

## TODO

- [ ] Add favicon.ico
