When writing schema using the HDMF Schema Language, including extensions, the HDMF development team provides a few best
practices to ensure correct behavior from the HDMF reference API and other APIs that we are aware of (e.g., MatNWB).

1. Do not create schema that the HDMF reference API does not yet support. See `hdmf_support`_ for details.

2. Define new data types (``data_type_def``) at the root of the schema rather than nested within another data type
definition. Nested type definitions may in some cases lead to errors in HDMF. See `hdmf#511`_ and `hdmf#73`_.

3. Use the ``quantity`` key not in the data type definition but in the group/dataset spec where the type is included.
When the data type is included within another data type via ``data_type_inc``, if the ``quantity`` key is omitted, the
default value of 1 would be used. This makes the ``quantity`` defined in the data type definition meaningless
and confusing.

4. Use the ``name`` key not in the data type definition but in the group/dataset spec where the type is included,
unless you really want to require that all instances of the data type have that name. Mismatch between the name
defined on the data type definition and where it is included can lead to unexpected behavior in the APIs.

5. Create a new data type when adding attributes/datasets/groups/links to an existing data type. See
`hdmf-schema-language#13`_ for details. Adding attributes/datasets/groups/links to an existing data type using
``data_type_inc`` is partially supported by the APIs, particularly the validator, so this is discouraged until
full, tested support is added.

6. Modifying the dtype, shape, or quantity of a data type when using ``data_type_inc`` should only restrict the values
from their original definitions. This ensures that the data types follow the object-oriented programming principle of
inheritance. For example, if type A has ``dtype: text`` and type B extends type A
(``data_type_def: B, data_type_inc: A``), then type B should not redefine ``dtype`` to be ``int``
which is incompatible with the ``dtype`` of type A. The same idea holds if type A is included in another type
and a new type is not defined (just ``data_type_inc: A``).
In other words, all children types should be valid against the parent type. See `hdmf#321`_.

7. Non-scalar values for the ``value`` and ``default_value`` keys are not fully supported in the official APIs,
so these are discouraged until support is added.

8. Do not put spaces in the names of data types or objects. This can lead to unexpected behavior in the APIs.
See `pynwb#1421`_ for an example.


.. _hdmf#511: https://github.com/hdmf-dev/hdmf/issues/511
.. _hdmf#73: https://github.com/hdmf-dev/hdmf/issues/73
.. _hdmf-schema-language#13: https://github.com/hdmf-dev/hdmf-schema-language/issues/13
.. _hdmf#321: https://github.com/hdmf-dev/hdmf/issues/321
.. _pynwb#1421: https://github.com/NeurodataWithoutBorders/pynwb/issues/1421
.. _hdmf_support: https://hdmf.readthedocs.io/en/stable/spec_language_support.html
