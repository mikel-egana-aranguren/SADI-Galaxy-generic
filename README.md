SADI-Galaxy-generic
===================

About
-----

SADI-Galaxy-generic is a Galaxy tool that can execute any [SADI](http://sadiframework.org/) service, i.e. a generic SADI client for Galaxy. The inputs for the tool are the service URL and an RDF file with the actual data for the service to consume. SADI-Galaxy-generic applies automated reasoning to infer whether the RDF can be consumed by the service, that is, whether the RDF has instances that are inferred to be members of the service's OWL input class. If the input RDF can be consumed by the service, it invokes the service (more technically, it POSTs the RDF to the service), producing the output RDF (RDF/XML). Two extra Galaxy tools are provided to deal with the output RDF: RDF Syntax Converter and Merge RDF Graphs. RDF Syntax Converter converts any RDF/XML file to N3, N-Triple, or, (more importantly for Galaxy) a tab delimited, three column file (Subject-Predicate-Object); Merge RDF Graphs is able to merge together any number of RDF graphs, (hopefully) integrating information through common URIs.

Dependencies
------------

SADI-Galaxy-generic and RDF Syntax Converter depend on Java (tested with 1.7). Merge RDF Graphs depends on Python (Tested tested with 2.7.3) and [RDFLib](https://github.com/RDFLib/rdflib) (Tested with 4.1.1).

Installation
------------

1. Stop Galaxy.

2. Download or clone with Mercurial from the Galaxy tool shed (`hg clone http://mikel-egana-aranguren@toolshed.g2.bx.psu.edu/repos/mikel-egana-aranguren/sadi_generic`).

3. Copy everything under `galaxy-dist/` to your server's `galaxy-dist/` (i.e. recreate the `tools/`, `tool-data/` and `test-data/` directories in your server).

4. Add the following lines to your server's `/galaxy-dist/tool_conf.xml`:

```
  <section name="SADI services" id="SADI">
    <tool file="SADI/sadi_generic.xml"/>
    <tool file="SADI/RDFSyntaxConverter.xml"/>
    <tool file="SADI/mergeRDFgraphs.xml"/>
  </section>
```
  
5. Start Galaxy.

Testing SADI services
---------------------

In the case of SADI-Galaxy-generic, Galaxy tests (see `<tests></tests>` in `sadi_generic.xml`) can be used to execute different services that are usually up and running and respond promptly. Since the RDF output from the services is not deterministic (Syntactically and functionally) there is no way of generating an RDF file in order to do some detailed comparison, only general criteria like containing URIs and XML validity are used. The tests make more sense as examples to execute SADI services with the adequate RDF inputs (Most of the SADI services included in the main [registry](http://sadiframework.org/registry) only include the OWL input class, not the RDF input). One of the services is a mockup [SADI Python](http://code.google.com/p/sadi/wiki/BuildingServicesInPython) service you can run at localhost: if you want to use it, install SADI Python (`easy_install sadi` or `pip install sadi`) and then run `python galaxy-dist/test-data/localhost_SADI.py`. You can then proceed with the tests: 

`./run_functional_tests.sh -id sadi_generic`

Contact
-------

Please send any comment to mikel.egana.aranguren@gmail.com, or use GitHub to fork/pull request or add issues. This GitHub repository is for development, the Galaxy tool-shed Mercurial repository is for official releases.

Acknowledgements
----------------

This work is funded by the Marie Curie Cofund program of the EU, FP7, and the Genomic Resources group of the UPV-EHU.

 