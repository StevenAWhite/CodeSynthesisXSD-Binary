This example shows how to handle XML vocabularies with multiple
root elements using the C++/Tree mapping.

See also the messaging example for an alternative approach that
uses the element type and element map features of the C++/Tree
mapping.

The example consists of the following files:

protocol.xsd
  XML Schema which defines a simple bank account protocol with
  requests such as withdraw and deposit.

balance.xml
withdraw.xml
deposit.xml
  Sample XML instances for the protocol requests.

protocol.hxx
protocol.cxx
  C++ types that represent the given vocabulary and a set of
  parsing functions that convert XML documents to a tree-like
  in-memory object model. These are generated by XSD from
  protocol.xsd.

dom-parse.hxx
dom-parse.cxx
  Definition and implementation of the parse() function that
  parses an XML document to a DOM document.

driver.cxx
  Driver for the example. It first calls the above parse() function
  to parse the input file to a DOM document. It then determines the
  type of request being handled and calls the corresponding parsing
  function that constructs the object model from this DOM document.
  Finally, it prints the content of this object model to STDERR.
  This example intentionally does not support the deposit request
  to show how to handle unknown documents.

To run the example on the sample XML request documents simply
execute:

$ ./driver balance.xml
$ ./driver withdraw.xml
$ ./driver deposit.xml
