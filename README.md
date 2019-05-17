This adds a data transform plugin system to Paragraphs Sets by wrapping that module's data_alter hooks.

The annotated plugins operate kinda sorta like migration process plugins. Currently include plugins: 

- `simple`: an identity plugin
- `create_entity`: construct nested entities for an entity reference field

For example, in a paragraphs set, we want a paragraph that references custom entities to prepopulate (i.e., create) the entities:

```
...
-
    type: fast_facts
    data:
      field_heading: 'Why Choose This Degree?'
      field_collection_items:
        plugin: create_entity
        reuse_template_if_unmodified: true
        data:
          -
            bundle: fast_fact
            field_heading: 'Test fact 1'
            field_body: 'Lorem ipsum'
          -
            bundle: fast_fact
            field_heading: 'Test fact 2'
            field_body: 'Lorem ipsum'
...
```

The `field_collection_items` field gets populated using the `create_entity` plugin, while `field_heading` gets populated as before using the paragraphs_sets builtin field value setter.
