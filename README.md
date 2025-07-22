# FHIR specifications XML

FHIR, pronounced "fire," stands for Fast Healthcare Interoperability Resources. FHIR is standard for exchanging healthcare information between different systems, designed to be flexible and easy to implement. It uses modern web technologies like RESTful APIs and JSON, XML, or RDF for data representation.

<https://www.hl7.org/>

This repository contains the worldwide-compatible FHIR specifications files
using JSON, and explains how to create this for yourself if you wish.

<https://www.hl7.org/fhir/downloads.html>

This is the master set of worldwide-compatible definitions that should be the
first choice whenever generating any implementation artifacts that you want to
work as a baseline across all worldwide HL7 FHIR implementations, extensions,
derivations, and the like.

If you're specifically interested in HL7 FHIR for GIG Cymru NHS Wales, then see this:

<https://simplifier.net/guide/fhir-standards-wales-implementation-guide/Home>

## Do it yourself

Here's how you can create this repository from scratch:

```sh
mkdir fhir-specifications-xml && cd $_
```

Download the HL7 FHIR XML definitions, examples, and validations:

```sh
curl -sSLO https://www.hl7.org/fhir/definitions.xml.zip &&
unzip -d xml-definitions definitions.xml.zip && rm $_

curl -sSLO https://www.hl7.org/fhir/examples.zip &&
unzip -d xml-examples examples.zip && rm $_

curl -sSLO https://www.hl7.org/fhir/fhir-all-xsd.zip
unzip -d xml-validation fhir-all-xsd.zip && rm $_
```

## FHIR specification XML files

Explain these FHIR specifications XML files:

- conceptmaps.xml
- dataelements.xml
- fhir-all-xsd.zip
- profiles-others.xml
- profiles-resources.xml
- profiles-types.xml
- search-parameters.xml
- valuesets.xml
- version.info

These XML files collectively define a FHIR Implementation Guide or specification package.

These XML files contain the same FHIR specification content as their JSON counterparts. FHIR supports both XML and JSON representations equally.

**Use XML when:**

- Integrating with legacy systems
- Need schema validation
- Working with systems requiring XML signatures
- Need namespace support

**Use JSON when:**

- Building modern REST APIs
- Working with JavaScript/web applications
- Need smaller payload sizes
- Want simpler parsing

Both formats are equally valid in FHIR and contain identical information, just structured differently.

### conceptmaps.xml

**Purpose**: XML representation of code system mappings

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <type value="collection"/>
  <entry>
    <resource>
      <ConceptMap>
        <id value="gender-to-v2"/>
        <url value="http://hl7.org/fhir/ConceptMap/gender-to-v2"/>
        <source value="http://hl7.org/fhir/ValueSet/administrative-gender"/>
        <target value="http://terminology.hl7.org/ValueSet/v2-0001"/>
        <group>
          <source value="http://hl7.org/fhir/administrative-gender"/>
          <target value="http://terminology.hl7.org/CodeSystem/v2-0001"/>
          <element>
            <code value="male"/>
            <display value="Male"/>
            <target>
              <code value="M"/>
              <display value="Male"/>
              <equivalence value="equivalent"/>
            </target>
          </element>
          <element>
            <code value="female"/>
            <display value="Female"/>
            <target>
              <code value="F"/>
              <display value="Female"/>
              <equivalence value="equivalent"/>
            </target>
          </element>
        </group>
      </ConceptMap>
    </resource>
  </entry>
</Bundle>
```

### **dataelements.xml**

**Purpose**: XML data dictionary definitions

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <entry>
    <resource>
      <DataElement>
        <id value="blood-pressure-systolic"/>
        <url value="http://example.org/DataElement/bp-systolic"/>
        <identifier>
          <system value="http://example.org/dataelements"/>
          <value value="DE0001"/>
        </identifier>
        <name value="SystolicBloodPressure"/>
        <status value="active"/>
        <element>
          <path value="systolic"/>
          <label value="Systolic Blood Pressure"/>
          <definition value="Peak arterial pressure during heart contraction"/>
          <type>
            <code value="Quantity"/>
          </type>
          <minValueQuantity>
            <value value="0"/>
            <unit value="mmHg"/>
            <system value="http://unitsofmeasure.org"/>
            <code value="mm[Hg]"/>
          </minValueQuantity>
          <maxValueQuantity>
            <value value="300"/>
            <unit value="mmHg"/>
            <system value="http://unitsofmeasure.org"/>
            <code value="mm[Hg]"/>
          </maxValueQuantity>
        </element>
      </DataElement>
    </resource>
  </entry>
</Bundle>
```

### fhir-all-xsd.zip

**Purpose**: XML Schema Definition files for FHIR validation

This ZIP file contains:
```
fhir-all-xsd.zip/
├── fhir-base.xsd          # Base FHIR types and resources
├── fhir-single.xsd        # All-in-one schema file
├── xml.xsd                # XML namespace definitions
├── tombstone.xsd          # Deleted resource definitions
└── [resource-name].xsd    # Individual resource schemas
    ├── patient.xsd
    ├── observation.xsd
    ├── medication.xsd
    └── ... (all other resources)
```

Example from `patient.xsd`:

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" 
           xmlns="http://hl7.org/fhir"
           targetNamespace="http://hl7.org/fhir">
  
  <xs:complexType name="Patient">
    <xs:annotation>
      <xs:documentation>Demographics and administrative information about a patient</xs:documentation>
    </xs:annotation>
    <xs:complexContent>
      <xs:extension base="DomainResource">
        <xs:sequence>
          <xs:element name="identifier" type="Identifier" minOccurs="0" maxOccurs="unbounded"/>
          <xs:element name="active" type="boolean" minOccurs="0"/>
          <xs:element name="name" type="HumanName" minOccurs="0" maxOccurs="unbounded"/>
          <xs:element name="telecom" type="ContactPoint" minOccurs="0" maxOccurs="unbounded"/>
          <xs:element name="gender" type="AdministrativeGender" minOccurs="0"/>
          <xs:element name="birthDate" type="date" minOccurs="0"/>
          <xs:element name="deceased" type="Element" minOccurs="0"/>
          <xs:element name="address" type="Address" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
</xs:schema>
```

### profiles-others.xml

**Purpose**: Extensions, operations, and other non-resource definitions

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <entry>
    <resource>
      <StructureDefinition>
        <id value="us-core-race"/>
        <url value="http://hl7.org/fhir/us/core/StructureDefinition/us-core-race"/>
        <name value="USCoreRaceExtension"/>
        <status value="active"/>
        <kind value="complex-type"/>
        <abstract value="false"/>
        <type value="Extension"/>
        <context>
          <type value="element"/>
          <expression value="Patient"/>
        </context>
        <differential>
          <element id="Extension">
            <path value="Extension"/>
            <short value="US Core Race Extension"/>
            <definition value="Concepts classifying the person into a named category of humans sharing common history, traits, geographical origin or nationality"/>
          </element>
          <element id="Extension.extension:ombCategory">
            <path value="Extension.extension"/>
            <sliceName value="ombCategory"/>
            <min value="0"/>
            <max value="5"/>
            <type>
              <code value="Extension"/>
            </type>
          </element>
        </differential>
      </StructureDefinition>
    </resource>
  </entry>
  
  <entry>
    <resource>
      <OperationDefinition>
        <id value="patient-everything"/>
        <url value="http://hl7.org/fhir/OperationDefinition/Patient-everything"/>
        <name value="Everything"/>
        <status value="active"/>
        <kind value="operation"/>
        <code value="everything"/>
        <resource value="Patient"/>
        <system value="false"/>
        <type value="false"/>
        <instance value="true"/>
        <parameter>
          <name value="start"/>
          <use value="in"/>
          <min value="0"/>
          <max value="1"/>
          <type value="date"/>
        </parameter>
      </OperationDefinition>
    </resource>
  </entry>
</Bundle>
```

### profiles-resources.xml

**Purpose**: Resource profiles with constraints

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <entry>
    <resource>
      <StructureDefinition>
        <id value="us-core-patient"/>
        <url value="http://hl7.org/fhir/us/core/StructureDefinition/us-core-patient"/>
        <name value="USCorePatientProfile"/>
        <status value="active"/>
        <kind value="resource"/>
        <abstract value="false"/>
        <type value="Patient"/>
        <baseDefinition value="http://hl7.org/fhir/StructureDefinition/Patient"/>
        <derivation value="constraint"/>
        <differential>
          <element id="Patient">
            <path value="Patient"/>
            <mustSupport value="false"/>
          </element>
          <element id="Patient.identifier">
            <path value="Patient.identifier"/>
            <min value="1"/>
            <mustSupport value="true"/>
          </element>
          <element id="Patient.identifier.system">
            <path value="Patient.identifier.system"/>
            <min value="1"/>
            <mustSupport value="true"/>
          </element>
          <element id="Patient.name">
            <path value="Patient.name"/>
            <min value="1"/>
            <mustSupport value="true"/>
          </element>
        </differential>
      </StructureDefinition>
    </resource>
  </entry>
</Bundle>
```

### profiles-types.xml

**Purpose**: Data type profiles and constraints

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <entry>
    <resource>
      <StructureDefinition>
        <id value="us-core-direct-email"/>
        <url value="http://hl7.org/fhir/us/core/StructureDefinition/us-core-direct-email"/>
        <name value="USCoreDirectEmailAddress"/>
        <status value="active"/>
        <kind value="primitive-type"/>
        <abstract value="false"/>
        <type value="string"/>
        <baseDefinition value="http://hl7.org/fhir/StructureDefinition/string"/>
        <derivation value="constraint"/>
        <differential>
          <element id="string">
            <path value="string"/>
            <constraint>
              <key value="us-core-1"/>
              <severity value="error"/>
              <human value="Must be a valid Direct email address"/>
              <expression value="matches('^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[direct|Direct|DIRECT]$')"/>
            </constraint>
          </element>
        </differential>
      </StructureDefinition>
    </resource>
  </entry>
</Bundle>
```

### search-parameters.xml

**Purpose**: Search parameter definitions in XML

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <entry>
    <resource>
      <SearchParameter>
        <id value="patient-birthdate"/>
        <url value="http://hl7.org/fhir/SearchParameter/Patient-birthdate"/>
        <name value="birthdate"/>
        <status value="active"/>
        <description value="The patient's date of birth"/>
        <code value="birthdate"/>
        <base value="Patient"/>
        <type value="date"/>
        <expression value="Patient.birthDate"/>
        <xpath value="f:Patient/f:birthDate"/>
        <xpathUsage value="normal"/>
        <comparator value="eq"/>
        <comparator value="ne"/>
        <comparator value="gt"/>
        <comparator value="lt"/>
        <comparator value="ge"/>
        <comparator value="le"/>
        <comparator value="sa"/>
        <comparator value="eb"/>
        <comparator value="ap"/>
      </SearchParameter>
    </resource>
  </entry>
</Bundle>
```

### valuesets.xml

**Purpose**: Value set definitions in XML format

```xml
<Bundle xmlns="http://hl7.org/fhir">
  <entry>
    <resource>
      <ValueSet>
        <id value="marital-status"/>
        <url value="http://hl7.org/fhir/ValueSet/marital-status"/>
        <name value="MaritalStatus"/>
        <status value="active"/>
        <description value="The domestic partnership status of a person"/>
        <compose>
          <include>
            <system value="http://terminology.hl7.org/CodeSystem/v3-MaritalStatus"/>
            <concept>
              <code value="A"/>
              <display value="Annulled"/>
            </concept>
            <concept>
              <code value="D"/>
              <display value="Divorced"/>
            </concept>
            <concept>
              <code value="I"/>
              <display value="Interlocutory"/>
            </concept>
            <concept>
              <code value="L"/>
              <display value="Legally Separated"/>
            </concept>
            <concept>
              <code value="M"/>
              <display value="Married"/>
            </concept>
            <concept>
              <code value="S"/>
              <display value="Never Married"/>
            </concept>
            <concept>
              <code value="W"/>
              <display value="Widowed"/>
            </concept>
          </include>
        </compose>
      </ValueSet>
    </resource>
  </entry>
</Bundle>
```

## Key Differences: XML vs JSON

### Attribute Handling

XML uses attributes and elements:

```xml
<identifier>
  <system value="http://hospital.org/mrn"/>
  <value value="12345"/>
</identifier>
```

JSON uses properties:

```json
{
  "system": "http://hospital.org/mrn",
  "value": "12345"
}
```

### Arrays

XML repeats elements:

```xml
<name>
  <family value="Smith"/>
</name>
<name>
  <family value="Jones"/>
</name>
```

JSON uses arrays:

```json
"name": [
  {"family": "Smith"},
  {"family": "Jones"}
]
```

### Namespaces

XML supports namespaces:

```xml
<Patient xmlns="http://hl7.org/fhir" 
         xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <text>
    <xhtml:div>Patient narrative here</xhtml:div>
  </text>
</Patient>
```

### Schema Validation

XML has XSD for strict validation:

```xml
<xs:element name="birthDate" type="date" minOccurs="0"/>
```
