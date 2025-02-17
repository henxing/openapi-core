Extensions
==========

x-model
-------

By default, objects are unmarshalled to dictionaries. You can use dynamically created dataclasses by providing ``x-model-path`` property inside schema definition with name of the model.

.. code-block:: yaml
  :emphasize-lines: 5

    ...
    components:
     schemas:
       Coordinates:
         x-model: Coordinates
         type: object
         required:
           - lat
           - lon
         properties:
           lat:
             type: number
           lon:
             type: number

As a result of unmarshalling process, you will get ``Coordinates`` class instance with ``lat`` and ``lon`` attributes.


x-model-path
------------

You can use your own dataclasses, pydantic models or models generated by third party generators (i.e. `datamodel-code-generator <https://github.com/koxudaxi/datamodel-code-generator>`__) by providing ``x-model-path`` property inside schema definition with location of your class.

.. code-block:: yaml
  :emphasize-lines: 5

    ...
    components:
     schemas:
       Coordinates:
         x-model-path: foo.bar.Coordinates
         type: object
         required:
           - lat
           - lon
         properties:
           lat:
             type: number
           lon:
             type: number

.. code-block:: python

    # foo/bar.py
    from dataclasses import dataclass

    @dataclass
    class Coordinates:
       lat: float
       lon: float

As a result of unmarshalling process, you will get instance of your own dataclasses or model.
