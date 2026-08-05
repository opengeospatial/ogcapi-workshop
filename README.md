# OGC API workshop
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15846453.svg)](https://doi.org/10.5281/zenodo.15846453)

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

The workshop manual is powered by [Zensical](https://zensical.org) which facilitates easy management
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
zensical build
# serve locally
zensical serve  # website is made available on http://localhost:8000
```
### Translating the workshop to a different language

Support to multiple languages is native in Zensical. To add an additional language to the workshop, create another toml file with the locale code as part of the filename. See an example [here](./workshop/content/zensical.pt.toml). 

- To enable the language switcher, update this block at the end of [the main configuration file](./workshop/content/zensical.toml):
    ```
    alternate =[
        { name = "English", link = "/", lang = "en" },
        { name = "Português", link = "/pt/", lang = "pt" }
    ] 
    ```
- foreach `.md` page in `workshop/content/docs`, add an equivalent page in the language with the locale code as part of the filename.  For example:
  - `records.md` -> `records.pt.md`
  
<!-- TODO: add something about Action

- Update the [GitHub action](https://github.com/geopython/diving-into-pygeoapi/blob/main/.github/workflows/deploy.docs.yml), to also include a build for this language; example: `zensical build --strict --config-file zensical.pt.toml`
-->

- commit to your fork and issue a GitHub Pull Request

Note: Zensical can only serve one language at a time. Example:
 `zensical serve --config-file zensical.pt.toml`

If you want to test the language switcher: build the default English site, build the other language sites and spin up a basic local web server to view the combined output:

 ```
zensical build --config-file zensical.toml

zensical build --config-file zensical.pt.toml

python3 -m http.server --directory site
 ```

## Contributing updates

To make contributions back to the workshop, fork the repository from GitHub.  Contributions and Pull Requests are always welcome!

Changes to the GitHub repository result in an automated build and deploy of the content to [ogcapi-workshop.ogc.org](https://ogcapi-workshop.ogc.org).

## Deploying to live site

Website updates are automatically published via GitHub Actions.
