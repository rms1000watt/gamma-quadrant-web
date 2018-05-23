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

TODO: minify/uglify

## Upload

```bash
export AWS_PROFILE=gamma-quadrant
aws s3 cp   index.html s3://gamma-quadrant-us-west-2-global-gammaquadrant.io/index.html --acl public-read
aws s3 sync assets/    s3://gamma-quadrant-us-west-2-global-gammaquadrant.io/assets/    --acl public-read
aws s3 sync images/    s3://gamma-quadrant-us-west-2-global-gammaquadrant.io/images/    --acl public-read
```

## Credits

- `Dimension` by [HTML5 UP](https://html5up.net/)
