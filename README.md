# ifc-reeper

This archive holds the output of running the [reeper](https://sourceforge.net/projects/reeper/) processing engine against the [Industry Foundation Class](https://www.buildingsmart.org/standards/bsi-standards/industry-foundation-classes/) EXPRESS schema. The hope is that the converted data models - output as SysML, UML2, and OWL - can serve as a springboard for integrating IFC with the broader STEP and MOF ecosystems.

# Workflow
Every IFC release is given it own top-level directly. Each reeper output format for the corresponding IFC schema has its own subdirectory (i.e., sysml/, uml2/, owl/). 

Reeper expects an XML encoding of the EXPRESS schemas as input. This XML encoding is distinct from ISO 10303-28 and is used to avoid the need for an EXPRESS parser. EuroStep's (now retired) eep parser can perform the conversion, although I had success using Craig Lanning's [ExpressEngine](http://exp-engine.sourceforge.net/). 

At the time of writing, reeper is a command line tool without a standard install procedure or gemfile. Apart from Ruby 2.x, you'll need to `gem install` [uuid](https://rubygems.org/gems/uuid/versions/2.3.9) and [nokogiri](https://nokogiri.org/tutorials/installing_nokogiri.html). I also had to update the `map_from_express` method signatures inside each mapping_*.rb files to take a second argument, *passedArgs*.

From here, the workflow is automatic. To map IFC4x2 to SysML, for example:
`$ ruby reeper.rb expxml=IFC4x2.xml map=./mapping_sysml.rb`

Omitted translations (like EXPRESS WHERE rules) will be echoed on stdout.

# Next Steps

Encoding the IFC schema in an [MOF](https://en.wikipedia.org/wiki/Meta-Object_Facility)-based format opens up a lot of possibilities: 
* Importing into a CASE or MDA framework for visualization and analysis
* Increasing IFC's modularity by leveraging MOF's packaging system
* Experimenting with [MMT](https://en.wikipedia.org/wiki/MMT_(Eclipse)) for cross-domain schema interoperability
* Developing open, extensible industry "workbench" tools based on [EMF](https://en.wikipedia.org/wiki/Eclipse_Modeling_Framework) and [OSGi](https://en.wikipedia.org/wiki/Equinox_(OSGi))

To learn more about the mapping strategies reeper uses, review the header comments of each mapping_*.rb file in the [reeper project repository](https://sourceforge.net/p/reeper/code/ci/master/tree/). 
