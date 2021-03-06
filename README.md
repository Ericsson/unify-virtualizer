# Introduction

This module is a Virtualizer data model implementation example library in Python for the [EU-FP7-UNIFY](http://fp7-unify.eu/) project.

The Virtualizer YANG model was presented in [draft-unify-nfvrg-recursive-programming](https://tools.ietf.org/html/draft-unify-nfvrg-recursive-programming).

The main goal of the library was to provide a common interface between components from various partners, by realizing the Sl-Or UNIFY reference point according to the Virtualizer YANG model.
Further expectations on the library were:
* Realize the elements of the Yang model by Python Objects
* Parse an entire Virtualizer instance from XML
* Dump an entire Virtualizer instance to XML
* Support main Netconf abstractions
* Support workflows, like: get config, edit config, diff config
* Support working with full configurations as well as partial updates to existing configurations
* Support easy access to components of an object (e.g. flow entries of a flow table)
* Support walking in the structure (e.g. from a port of a flow entry to the NF to which the port belongs to)

The library consists of two main files:
* virtualizer3.py: contains the Virtualizer object structure. This is autogenerated from the virtualizer3.yang module.
* baseclasses.py: contains the common components for the library, like the base Yang class for generic parsing, comparison, etc.

# Usage examples
* A = Virtualizer(): init an empty virtualizer object
* B = Virtualizer.parse(xml): to parse an instance from an XML input (file or string)
* B.xml(): to dump an instance to an XML string, e.g., for netconf operation
* B.reduce(A): remove all objects from B, which exist in A (create a canonical form)
* B.bind(A): resolve lefrefs; copy missing targets from A to B if needed
* A.merge(B): update A with changes from B; netconf operations are copied without execution
* C = A.diff(B): return a diff to go from A to B
* A.patch(C): apply C on A, i.e., A.patch(A.diff(B)) == B

# Additional information

* [UNIFY Deliverables](http://fp7-unify.eu/index.php/results.html#Deliverables)
