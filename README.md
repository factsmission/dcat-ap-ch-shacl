[![Build Status](https://travis-ci.com/factsmission/dcat-ap-ch-shacl.svg?branch=master)](https://travis-ci.com/factsmission/dcat-ap-ch-shacl)

# SHACL Shapes for the DCAT Application Profile for Data Portals in Switzerland

This project provides [SHACL](https://www.w3.org/TR/shacl/) to validate metadata against the [eCH-0200 Standard](https://www.ech.ch/vechweb/page?p=dossier&documentNumber=eCH-0200&documentVersion=1.0).

## Status

This project is work in progress. The functionality described in this README might not yet be implemented or not yet work as described.

## Files

 * `ech-0200.shacl.ttl` : This file models the constraints defined in eCH-200 with the SHACL vocabulary
 * `examples/` : This directory contains RDF Turtle files that can be used to test `ech-0200.shacl.ttl`. The conventions is that files ending with `.valid.ttl` will validate and files einding with `.fail.ttl`do not validate.

## Usage

To use the Shapes to validate data you need a SHACL validator such as [TopBraid SHACL API](https://github.com/TopQuadrant/shacl). With this validator you can validate RDF Turtle files as follows:

    shaclvalidate -shapesfile ech-0200.shacl.ttl -datafile data.ttl

For example (from this directory):

    shaclvalidate -shapesfile ech-0200.shacl.ttl -datafile .\examples\minimal.valid.ttl

## References

This project is similar an partially based on the [EU DCAT-AP SHACL constraint definitions](https://github.com/SEMICeu/dcat-ap_shacl).

## Note on language

While the eCH-0200 Specification is available in German and French the SHACL Shapes are documented in English to better allign with other Shape files and tools that are likely used together.

## License

As prospective part of an [eCH](https://www.ech.ch/) standard the code and documentations in this repository can be used, distributed and further developed without any restriction by patents or licenses.
