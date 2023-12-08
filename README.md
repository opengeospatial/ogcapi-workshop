# OGC API workshop

Welcome to the OGC API workshop!

## Overview

OGC is globally known for its proven widely implemented open standards. The OGC open consensus-based standards development process has evolved to move at the pace of innovation, with constant input from technology forecasting, practical prototyping, real-world testing, certification and compliance and community engagement. Today we are revolutionizing how geospatial/location information is shared, accessed, integrated, and analyzed via the OGC’s revolutionary APIs- the building blocks for location information.

[OGC APIs](https://ogcapi.ogc.org) are designed to make it easy for ANYONE to provide and use geospatial data on the web, and to integrate this data with ANY other type of information. These Standards build upon the legacy of the OGC Web Service Standards (WMS, WFS, WCS, WPS, etc.), but define resource-centric APIs that take advantage of modern web development practices. This web page provides information on these Standards in a consolidated location.

These Standards are being constructed as "building blocks" that can be used to assemble novel APIs for web access to geospatial content. The building blocks are defined not only by the requirements of the Standards specified in the [OGC's Standards Program](https://www.ogc.org/standards), but also through interoperability prototyping and testing in the [OGC's Collaborative Solutions and Innovation Program](https://www.opengeospatial.org/ogc/programs/ip).

## For users

Are you a workshop participant or want to dive-in individually?  Go to [ogcapi-workshop.ogc.org](https://ogcapi-workshop.ogc.org) to follow the lessons and exercises.

## For authors

Below are guidelines for authoring and/or improving the workshop's content.

### Building the workshop content locally

The workshop manual is powered by [MkDocs](https://www.mkdocs.org) which facilitates easy management
of content and publishing. Workshop content is written in Markdown.


### Setting up the manual environment locally

```bash
# build a virtual Python environment in isolation
python3 -m venv .
. bin/activate
# fork or clone from GitHub
git clone https://github.com/opengeospatial/ogcapi-workshop.git
cd ogcapi-workshop/workshop/content
# install required dependencies
pip3 install -r requirements.txt
# build the website
mkdocs build
# serve locally
mkdocs serve  # website is made available on http://localhost:8000
```

## Contributing updates

To make contributions back to the workshop, fork the repository from GitHub.  Contributions and Pull Requests are always welcome!

Changes to the GitHub repository result in an automated build and deploy of the content to [ogcapi-workshop.ogc.org](https://ogcapi-workshop.ogc.org).

## Deploying to live site

Website updates are automatically published via GitHub Actions. To publish manually:

```bash
# NOTE: you require access privileges to the GitHub repository
# to publish live updates
mkdocs gh-deploy -m 'add new page on topic x'
```
