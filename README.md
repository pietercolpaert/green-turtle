# RDFa Processor
[![npm version](https://badge.fury.io/js/rdfa-processor.svg)](https://badge.fury.io/js/rdfa-processor)

A Fork of Green Turtle, an RDFa 1.1 implementation in JavaScript for browsers and NodeJS. This repository only keeping the core RDFa tasks and using the RDFJS triple/quad representation.

Install: `npm install rdfa-processor`

Usage:
```javascript
var doc = window.document; //you can also use jsdom to get this, or use DOMParser to parse a string
var parser = new (require('rdfa-processor').RDFaProcessor)();
parser.onTriple = function (triple) {
  console.log(triple);
};
parser.process(doc);
```

See the `example` folder for more examples

## Conformance Information from the original repository

Green Turtle passes all the tests for XML, XHTML1, XHTML5, HTML4, and HTML5 as provided by the [RDFa WG](http://rdfa.info/test-suite/) except for the following notable issues:

 * [XML Test 0332](http://rdfa.info/test-suite/test-cases/rdfa1.1/xml/0332.xml) uses a bare `lang` attribute instead of an `xml:lang` attribute.  I believe this is a bug in the test.  Green Turtle does the right thing with respect to `xml:lang` attributes in XML and `lang` attributes in HTML.  A `lang` attribute in arbitrary XML has no special meaning.
 * [XHTML1 Test 0198](http://rdfa.info/test-suite/test-cases/rdfa1.1/xhtml1/0198.xhtml) and [XHTML5 Test 0198](http://rdfa.info/test-suite/test-cases/rdfa1.1/xhtml5/0198.xhtml) both have extra namespaces serialized in the XMLLiteral as expected output.  The input for the test cases does not have XML namespace attributes.  Instead, they use a `prefix` attribute to declare the prefixes used in the RDFa annotations.  Meanwhile, when the literal is serialized, they are not in the in-scope namespaces.  The RDFa specification says nothing about doing any kind of merging of prefixes and in-scope namespaces.  I believe these test cases are incorrect.  The correct serialization will not contain the `rdf:` and `foaf:` namespace declarations as they are not present in the source document.

## License

The original repository is licensed MIT, this derived work as well.
