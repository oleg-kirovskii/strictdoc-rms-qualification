# Tool definition
The tool we discuss in this document is a **requiments management system (RMS)** ```strictdoc```.

RMS is normally used to complete the following tasks:
* Requirements documentation, incl.:
  * Documentation of requirements as text,
  * Documentation of supporting materials, e.g. pictures,
  * Documentation of models (e.g. UML)
* Requirements analysis, including setting custom attributes and tags,
* Requirements linkage, incl.:
  * Parent <> child linkage,
  * Linkage to tests,
  * Linkage to resources, i.e. files,
  * Linkage to code

# Tool confidence method selection
## Classification
* Tool impact: **TI2**, as a corruption of requirements databased **is expected to** cause additional risk to the system
* Tool detection: **TD2**, as the corruption of requirements database may be noticed (especially if the items become unavailable or visibly corrupted), or it may be missed (especially if a full specification or its section is lost, and no procedure is in place to control for it).

TCL = **TCL2**.

## Qualification
### method selection
**Tool validation** will allow use of a TCL2 tool in the context of up to ASIL D (max. safety integrity level)

### Requirements for the method
Requirements on qualification method "Validation of the software tool" are specified by ISO 26262-11.4.9.2:

1. The validation measures shall provide evidence that the software tool complies with specified requirements to its purpose as specified in the classification
1. the malfunctions and their corresponding erroneous outputs of the software tool occurring during validation shall be analysed together with information on their possible consequences and with measures to avoid or detect them; and
1. the reaction of the software tool to anomalous operating conditions shall be examined