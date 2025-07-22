# FHIR specifications XML

FHIR, pronounced "fire," stands for Fast Healthcare Interoperability Resources.
FHIR is standard for exchanging healthcare information between different
systems, designed to be flexible and easy to implement. It uses modern web
technologies like RESTful APIs and JSON, XML, or RDF for data representation.

<https://www.hl7.org/>

FHIR provides multiple releases. The current release as of 2024 is release 5
which is known as "R5".

<https://www.hl7.org/R5/>

This repository contains the worldwide-compatible FHIR R5 specifications files
using XML, and explains how to create this repository for yourself if you wish.

On the FHIR R5 downloads page, the most important file is the definitions file.
This is the master set of worldwide-compatible definitions that should be the
first choice whenever generating any implementation artifacts.

<https://www.hl7.org/fhir/R5/downloads.html>

If you're specifically interested in HL7 FHIR for GIG Cymru NHS Wales, then see this:

<https://simplifier.net/guide/fhir-standards-wales-implementation-guide/Home>

## Do it yourself

Here's how you can create this repository from scratch:

```sh
mkdir fhir-specifications && cd $_
```

### FHIR R5 XML downloads

Download files:

- **`definitions.xml.zip`**: This is the master set of definitions.

- **`examples.zip`**: All the example resources in JSON format. Note the link
  doesn't use the word "xml".

- **`fhir-all-xsd.zip`**: XML Schema Definition (XSD) validation schemas
  (includes support schemas, resource schemas, modular & combined schemas, and
  Schematrons)

Run:

```sh
mkdir -p r5/xml/definitions &&
curl -sSLO https://www.hl7.org/fhir/R5/definitions.xml.zip &&
unzip -d r5/xml/definitions definitions.xml.zip && rm $_

mkdir -p r5/xml/examples &&
curl -sSSO https://www.hl7.org/fhir/R5/examples.zip
unzip -d r5/xml/examples examples.zip && rm $_

mkdir -p r5/xml/xsd &&
curl -sSSO https://www.hl7.org/fhir/R5/fhir-all-xsd.zip &&
unzip -d r5/xml/xsd fhir-all-xsd.zip && rm $_
```

For more about these see subdirectory [r5/xml](r5/xml).
