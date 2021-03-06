This example shows how to use type customization to parse and serialize
a specific attribute that is matched by a wildcard (anyAttribute). The
example achieves this by customizing the type to include the data
members and accessors/modifiers that represent the attribute as well as
the parsing constructor and serialization operator where the attribute
value is extracted from and inserted back to DOM, respectively. For
more information on the C++/Tree mapping customization see the C++/Tree
Mapping Customization Guide[1].

[1] http://wiki.codesynthesis.com/Tree/Customization_guide

The example consists of the following files:

wildcard.xsd
  XML Schema definition for simple data type and element.

wildcard.xml
  Sample XML instance document.

wildcard.hxx
wildcard.ixx
wildcard.cxx
  C++ types that represent the given vocabulary, a set of parsing
  functions that convert XML instance documents to a tree-like in-memory
  object model, and a set of serialization functions that convert the
  object model back to XML. These are generated by XSD from wildcard.xsd
  with the --custom-type option in order to customize the data type.

wildcard-custom.hxx
  Header file which defines our own data class by inheriting from the
  generated data_base. It is included at the end of wildcard.hxx using
  the --hxx-epilogue option.

wildcard-custom.cxx
  Source file which contains the implementation of our data class.

driver.cxx
  Driver for the example. It first calls one of the parsing functions
  that constructs the object model from the input file. It then prints
  the data to STDERR, including the extra attribute. Finally, the driver
  serializes the object model back to XML.

To run the example on the sample XML instance document simply execute:

$ ./driver wildcard.xml
