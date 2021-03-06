This example shows how to use type customization to parse and serialize
mixed content. The example achieves this by customizing the type with 
the mixed content model to include a DOM document that stores the data 
as a raw XML representation. The customized type also provides its own
parsing constructor and serialization operator where the mixed content
is extracted from and inserted back to DOM, respectively. The use of
DOM for mixed content storage is one of the options. You may find other
data structures (e.g., a string) more suitable depending on your situation.

For more information on the C++/Tree mapping customization see the C++/Tree
Mapping Customization Guide[1].

[1] http://wiki.codesynthesis.com/Tree/Customization_guide

The example consists of the following files:

people.xsd
  XML Schema definition for a simple person record vocabulary. Each
  record includes the bio element which represents arbitrary XHTML
  fragments as mixed content.

people.xml
  Sample XML instance document.

people.hxx
people.ixx
people.cxx
  C++ types that represent the given vocabulary, a set of parsing
  functions that convert XML instance documents to a tree-like in-memory
  object model, and a set of serialization functions that convert the
  object model back to XML. These are generated by XSD from people.xsd
  with the --custom-type option in order to customize the bio type.

people-custom.hxx
  Header file which defines our own bio class by inheriting from the
  generated bio_base. It is included at the end of people.hxx using
  the --hxx-epilogue option.

people-custom.cxx
  Source file which contains the implementation of our bio class.

driver.cxx
  Driver for the example. It first calls one of the parsing functions
  that constructs the object model from the input file. It then prints
  the data to STDERR, including the bio information converted to text.
  Finally, the driver serializes the object model back to XML.

To run the example on the sample XML instance document simply execute:

$ ./driver people.xml
