# Overview

The HDMF specification language defines formal structures for describing the organization of complex data using basic
concepts, e.g., Groups, Datasets, Attributes, and Links. See the
[documentation](http://hdmf-schema-language.readthedocs.io/) for more information and release notes.

The HDMF specification language is used by the
[Hierarchical Data Modeling Framework (HDMF)](https://github.com/hdmf-dev/hdmf).

## Customizing the language for specific applications

Certain keys of the hdmf-schema-language may be customized for a particular scientific domain or use case. For example,
the `data_types` key in the namespace may be customized to be `neurodata_types` and the
`data_type_def` and `data_type_inc` keys in the schema may be customized to be `neurodata_type_def`
and `neurodata_type_inc` for use in a neuroscience-specific application of the hdmf-schema-language. This can be
easily done by forking the [hdmf-schema-language repo](https://github.com/hdmf-dev/hdmf-schema-language)
and updating `source/namespace_map.yml` with the appropriate customizations. The `source/hdmf.schema.json` and any
references to HDMF in the documentation should also be modified appropriately. See the [NWB schema language repo](https://github.com/NeurodataWithoutBorders/nwb-schema-language) for an example of customizing the HDMF schema language
for use as the NWB schema language.

## For maintainers

The HDMF specification documentation is generated using [Sphinx](http://www.sphinx-doc.org/en/stable/index.html)

### Building the documentation

Install the latest version of [Sphinx](http://www.sphinx-doc.org/en/stable/index.html):
```
python -m pip install sphinx
```

To build the documentation, enter:
```
make <doctype>
```
where `<doctype>` is, e.g., `html`, `latexpdf`.

For a complete list of supported doc-types, enter:
```
make help
```

To remove previously generated documentation, enter:
```
make clean
```

### Making a release

1. Update the release notes in `source/release_notes.rst`.
2. Update the version in `source/namespace_map.yml`, `source/hdmf.schema.json`, and `source/conf.py`
