## Annotation Usage

### How to Use Annotations in Markdown Files

To annotate the content with domain terminology, wrap the text in annotation blocks using the following format:

```
<!-- BEGIN-ANNOTATION: ontology_id -->
The text goes here.
<!-- END-ANNOTATION: ontology_id -->
```

This annotation functionality automatically identifies and enriches domain-specific terminology with semantic hyperlinks.

### Available Ontologies

The following ontology IDs are supported:

- `oeo`
- `brick`
- `sms`
- `fmi`
- `dogont`
- `s4grid`
- `sargon`
- `s4ener`
- `bont`
- `openadr`
- `dices`

### Example

```
<!-- BEGIN-ANNOTATION: oeo -->
electrical energy is a form of energy derived from the potential or kinetic energy of charged particles.
<!-- END-ANNOTATION: oeo -->

<!-- BEGIN-ANNOTATION: brick -->
Building automation systems monitor temperature sensors.
<!-- END-ANNOTATION: brick -->
```