SADI-Galaxy-generic
===================

About
-----

SADI Generic is a Galaxy tool that can execute any [SADI](http://sadiframework.org/) service. The inputs for the tool are the service URL and an RDF file. SADI Generic infers whether the RDF can be consumed by the service, and if so it invokes the service, producing the result RDF (RDF/XML). Another tool, RDF Syntax Converter, is included to process the result: it converts any RDF/XML file to N3, N-Triple, or, (more importantly for Galaxy) a tab delimited, three column file (Subject-Predicate-Object). 

Installation
------------

1. Stop Galaxy.

2. Download or clone with mercurial (`hg clone hg clone http://mikel-egana-aranguren@toolshed.g2.bx.psu.edu/repos/mikel-egana-aranguren/sadi_generic`).

3. Copy everything under galaxy-dist/ to your server's galaxy-dist/ (i.e. recreate the tools/, tool-data/ and test-data/ directories in your server).

4. Add the following lines to your server's /galaxy-dist/tool_conf.xml:

```
  <section name="SADI services" id="SADI">
    <tool file="SADI/sadi_generic.xml"/>
    <tool file="SADI/RDFSyntaxConverter.xml"/>
  </section>
```
  
5. Start Galaxy.

Tests
-----

The RDF Syntax Converter can be tested as follows:

`./run_functional_tests.sh -id RDFSyntaxConverter`

In the case of SADI generic, rather than testing the tool itself, the tests execute different services that are usually up and running (Also, the RDF serialisation is not deterministic so there is no way of generating an RDF file in order to do some detailed comparison, only vague criteria like containing URIs, XML validity, ...). They also work as examples you can use to execute SADI services with the adequate RDF inputs (Many SADI services only include the OWL input class, not the RDF input). One of the services is a mockup [SADI Python](http://code.google.com/p/sadi/wiki/BuildingServicesInPython) service you can run at localhost: if you want to use it, install Python SADI (`easy_install sadi` or `pip install sadi`) and then run `python galaxy-dist/test-data/localhost_SADI.py`. You can then proceed with the tests: 

`./run_functional_tests.sh -id sadi_generic`

Contact
-------

Please send any comment to mikel.egana.aranguren@gmail.com, or use GitHub to pull request or add issues. 


Acknowledgements
----------------

This work is funded by the Marie Curie Cofund program of the EU, FP7, and the Genomic Resources group of the UPV-EHU.

 