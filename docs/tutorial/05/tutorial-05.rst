==========================================
Ferrules, wire bundles, custom wire colors
==========================================

* Ferrules
  * Simpler than connectors
  * Compact graphical representation
  * Only one pin, only one connection, no designator
  * Define once, auto-generate where needed
* Wire bundles
  * Internally treated as cables
  * Different treatment in BOM: Each wire is listed individually
  * Represented with dashed outline
* Custom wire colors
  * Wirecount can be implicit in color list

.. literalinclude:: tutorial-05.yml
   :language: yaml

`Source <tutorial-05.yml>`__ - `Bill Of Materials <tutorial-05.bom.tsv>`__
