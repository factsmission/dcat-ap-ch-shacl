[![Build Status](https://travis-ci.org/factsmission/dcat-ap-ch-shacl.svg?branch=master)](https://travis-ci.org/factsmission/dcat-ap-ch-shacl)

# SHACL Shapes for the DCAT Application Profile for Data Portals in Switzerland

This project provides [SHACL shapes](https://www.w3.org/TR/shacl/) to validate metadata against the [eCH-0200 Standard](https://www.ech.ch/vechweb/page?p=dossier&documentNumber=eCH-0200&documentVersion=1.0).

## Files

 * `ech-0200.shacl.ttl` : This file models the constraints defined in eCH-200 with the SHACL vocabulary
 * `examples/` : This directory contains RDF Turtle files that can be used to test `ech-0200.shacl.ttl`. The convention is that files ending with `.valid.ttl` will validate, while files ending with `.fail.ttl` will not validate.

## Usage

To use the shapes to validate data you need a SHACL validator such as [TopBraid SHACL API](https://github.com/TopQuadrant/shacl). With this validator you can validate RDF Turtle files as follows:

```BASH
$ shaclvalidate -shapesfile ech-0200.shacl.ttl -datafile data.ttl
```

For example (from this directory):

```BASH
$ shaclvalidate -shapesfile ech-0200.shacl.ttl -datafile .\examples\minimal.valid.ttl
```

The example isn't strictly minimal, as omitting `dcat:themeTaxonomy` would only result in a warning.

### Validating non Turtle Files

In order to work with RDF/XML files you need to convert the file in turtle format.

First you need Apache Jena. You can download and extract it with these commands:

```BASH
$ wget https://www-eu.apache.org/dist/jena/binaries/apache-jena-3.9.0.tar.gz
$ tar xvzf apache-jena-3.9.0.tar.gz
```

This creates a folder named `apache-jena-3.9.0`. To convert your `RDF/XML` file (eg. `file.rdf`) you can use this command:

```BASH
$ ./apache-jena-3.9.0/bin/riot --output=turtle rdfxml file.rdf > file.ttl
```

And you will find the converted result in `file.ttl`.

Jena supports these RDF formats: `turtle`, `ntriples`, `nquads`, `trig` and `rdfxml`.


## References

This project is similar and partially based on the [EU DCAT-AP SHACL constraint definitions](https://github.com/SEMICeu/dcat-ap_shacl).

## Note on Language

While the eCH-0200 Specification is available in German and French the SHACL shapes are documented in English to better allign with other shape files and tools that are likely used simultaneously.

## Comments on the Interpretation of the Specification

 * The specification mandates the use of `schema:url`v as class. This seems a mistake and we assume that `schema:URL` is what is meant.
 * The SHACL file also supports `xsd:dateTime` where the spec mandates `xsd:date`.
 * Inference: The specification isn't explicit if and what inference should be allowed. We assume that where `vcard:Kind` is allowed its subclasses (Individual, Organization, Group, Location) should be allowed to. SHACL only allows specifying ontological statements in the data and not in the shape graph, so currently using a subclass is only accepted if the respective `rdfs:subClassOf` statement is also present in the data. We could of course explicitly allow some named subclassed in the shape file but this doesn't seem to be wanted by the spec.
 * The type (`foaf:Document`) does not need to be explicitely specified for a document to validate; the type can be inferred from the `rdfs:range` of `foaf:Document`.

 ## Other Points to Discuss
 * Shouldn't we require a dataset to be named (using standard IRI) rather than requiring a proprietary `dct:identifier`?
 * Also, shouldn't the `dct:publisher` be named, rather than being an instance of `foaf:Agent`? Analogous questions can be asked for `dcat:themeTaxonomy` and `foaf:homepage`.
 * Should `xsd:dateTime` be supported as well where `xsd:date` is required?
 * It seems inconsistent to forbid `adms:status` on distributions while generally allowing arbitrary properties.

## License

As prospective part of an [eCH](https://www.ech.ch/) standard the code and documentations in this repository can be used, distributed and further developed without any restriction by patents or licenses.
