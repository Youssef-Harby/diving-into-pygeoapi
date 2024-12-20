---
title: Standards
---

# Overview

This section provides a high level overview of standards support in pygeoapi.

# Standards

Open standards are core to pygeoapi, and allow for broad interoperability and plug and play capability. pygeoapi supports
a number of open standards (both formal standards and defacto or community driven).

## API standards

### OGC API

pygeoapi implements the [OGC API](https://ogcapi.ogc.org) suite of standards from the [Open Geospatial Consortium](https://www.ogc.org/) (OGC). From the OGC API website:

!!! Citation

    The OGC API family of standards are being developed to make it easy for anyone to provide geospatial data to the web. These standards build upon the legacy of the OGC Web Service standards (WMS, WFS, WCS, WPS, etc.), but define resource-centric APIs that take advantage of modern web development practices. This web page provides information on these standards in a consolidated location.

    These standards are being constructed as "building blocks" that can be used to assemble novel APIs for web access to geospatial content. The building blocks are defined not only by the requirements of the specific standards, but also through interoperability prototyping and testing in OGC's Innovation Program. 

!!! Tip

    You can learn more about OGC APIs in the [OGC API workshop](https://ogcapi-workshop.ogc.org)

#### OGC API - Common

[OGC API - Common](https://ogcapi.ogc.org/common/) is a common framework used in all OGC API's. 
OGC API - Common provides the following functionality:

- based on [OpenAPI 3.0](https://spec.openapis.org/oas/latest.html)
- HTML and JSON as the dominant encodings, alternative encodings are possible
- shared endpoints such as:
    - `/` (landing page)
    - `/conformance`
    - `/openapi`
    - `/collections`
    - `/collections/foo`
- aspects such as pagination, links between resources, basic filtering, query parameters (`bbox`, `datetime`, etc.)
- shared models (exceptions, links, etc.)

OGC API - Common allows for specification developers to focus on the key functionality of a given API (i.e. data access, etc.)
while using common constructs. This harmonizes OGC API standards and enables deeper integration with less code. This also
allows for OGC API client software to be more streamlined.

The `/conformance` endpoint indicates which standards and extensions are supported by a deployment of OGC API.

#### OGC API building blocks

The OGC API approach allows for modularity and "profiling" of APIs depending on your requirements.  This means you
can mix and match OGC APIs together.

![OGC API building blocks](assets/images/ogc-api-building-blocks.png)

You can read more about this topic in the [building blocks website](https://blocks.ogc.org/).

#### More OGC APIs

The OGC API effort is rapidly evolving. Numerous OGC API standards are in development, and will be implemented in
pygeoapi over time:

- [Routes](https://ogcapi.ogc.org/routes) provides access to routing data
- [Styles](https://ogcapi.ogc.org/styles) defines a Web API that enables map servers, clients as well as visual style editors, to manage and fetch styles
- [3D GeoVolumes](https://ogcapi.ogc.org/geovolumes) facilitates efficient discovery of and access to 3D content in multiple formats based on a space-centric perspective
- [Moving Features](https://ogcapi.ogc.org/movingfeatures) defines an API that provides access to data representing features that move as rigid bodies
- [Joins](https://ogcapi.ogc.org/joins)  supports the joining of data, from multiple sources, with feature collections or directly with other input files
- [Discrete Global Grid System](https://ogcapi.ogc.org/dggs) enables applications to organise and access data arranged according to a Discrete Global Grid System (DGGS)

![Approved and candidate OGC API standards](assets/images/ogcapis.png)

#### OGC APIs supported by pygeoapi

pygeoapi implements numerous OGC API standards and draft standards. In addition, it is compliance certified and even a Reference Implementation (RI) for some of them. Compliance certification is important to remove interoperability risks. RI are always compliance certified. From OGC [Compliance Testing Program Policies & Procedures 08-134r11](https://docs.ogc.org/pol/08-134r11.html#toc26):

!!! Citation

    Candidate Products that pass all the tests in a Compliance Test Package, and that OGC has reviewed and certified as having passed those tests, are considered compliant with that Implementation Standard version. 

!!! Citation

    A Reference Implementation is a fully functional, licensed copy of a tested, branded software that has passes the test for an associated conformance class in a version of an Implementation Standard and that is free and publicly available for testing via a web service or download.


| Standard                               | pygeoapi status | Included in this workshop |
|----------------------------------------|-----------------|---------------------------|
| OGC API - Features                     | Reference       | ✅                        |
| OGC API - Coverages                    | Implementing    | ✅                        |
| OGC API - Tiles                        | Reference       | ✅                        |
| OGC API - Maps                         | Implementing    | ✅                        |
| OGC API - Processes                    | Certified    | ✅                        |
| OGC API - Records                      | Implementing    | ✅                        |
| OGC API - Environmental Data Retrieval | Reference       | ✅                        |
| SpatioTemporal Asset Catalog           | Implementing    |                           |
| OGC API - Routes                       | Planned         |                           |
| OGC API - Styles                       | Planned         |                           |
| OGC API - Moving Features              | Planned         |                           |
| OGC API - DGGS                         | Planned         |                           |

In the next section we will dive into the dedicated API's related to specific types of information. You will
notice that all APIs are combined and available via a single OGC API endpoint, thanks to OGC API - Common.

#### OpenAPI

Core to OGC API - Common is the [OpenAPI initiative](https://www.openapis.org/about) to help
describe and document an API. OpenAPI defines its structure in an OpenAPI document. 
OGC API - Common suggests this document to be located at `/openapi`. With pygeoapi in a browser 
[this URL](https://demo.pygeoapi.io/master/openapi) opens an interactive HTML page which facilitates 
an API query. Append `?f=json` to view the document in JSON. The OpenAPI document indicates which
endpoints are available in the service, which parameters it accepts and 
what types of responses can be expected. The OpenAPI document is a similar concept to Capabilities
XML as part of the first genration OGC Web Service standards.

!!! question "OpenAPI Specification parsing in a browser" 

    A common approach to interact with Open API's using json is to use a program like 
    [Postman](https://www.postman.com/). Also there are browser plugins which enable to define api 
    requests interactively within a browser. For firefox download the plugin 
    [poster](https://pluginsaddonsextensions.com/mozilla-firefox/poster-mozilla-addon). For Chrome 
    and Edge use [Boomerang](https://microsoftedge.microsoft.com/addons/detail/boomerang-soap-rest-c/bhmdjpobkcdcompmlhiigoidknlgghfo?hl=en-US). 
    In Boomerang you can create individual web requests, but also load the open api specification 
    document and interact with any of the advertised endpoints. 

The OpenAPI community provides various tools, such as a validator for OAS documents or 
[generate code](https://swagger.io/tools/swagger-codegen/) as a starting point for client development.

## Content and format standards

JSON is core in pygeoapi, providing a format that is machine readable and easy to parse and handle
by client software and tools.  OGC API - Common provides uniform JSON formats for the various
endpoints it supports.  Specific OGC API standards may specify domain specific formats (for example,
GeoJSON for OGC API - Features, GeoTIFF for OGC API - Coverages) depending on the data type(s).

# pygeoapi specific conventions

pygeoapi provides some conventions that are not put forth by OGC API standards, however facilitate
some features and capabilities.

## the `f` parameter

The `f` parameter can be used with any pygeoapi endpoint to specify an output format for a given
  API request.  Examples are `f=html`, `f=json`, etc.

!!! question "Using a web browser to access OGC API"

    Use your web browser to navigate to [demo.pygeoapi.io](https://demo.pygeoapi.io/master). A browser by default opens 
    any OGC API in HTML (as a webpage) due to the [HTTP Accept header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) 
    sent by the browser (`text/html`). On the right top corner you will notice a JSON link. The link 
    adds the parameter to the url: `f=json`, which is a mechanism of pygeoapi to override the HTTP Accept
    header sent by the web browser.

!!! note 

    When calling an OGC API from javascript, and the aim is to receive JSON, you can use the `?f=json` pygeoapi convention, or the content 
    negotiation as provided by the standard; include an HTTP header `Accept: "application/json"` in your request.

    In jQuery for example, this is represented by the dataType property:

    ``` {.js linenums="1"}
    $.ajax({
        method: "GET",
        url: "https://demo.pygeoapi.io/master",
        dataType: "json"
    });
    ```

    Or using the native fetch API:

    ``` {.js linenums="1"}
    const response = await fetch('https://demo.pygeoapi.io/master', {
        method: 'GET',
        headers: {
            'Accept': 'application/json'
        }
    });
    ```

## the `skipGeometry` parameter

The `skipGeometry` (`true|false`, default is `false`) parameter can be used with feature data access to facilitate
downloading vector data without geometry if desired.

# Summary

Standards are a cornerstone of pygeoapi, and will enable you to publish your data efficiently and with a low
barrier for users.  Now, let's get to the action: **Publishing data**!
