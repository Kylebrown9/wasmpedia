[Module]: ./
[Host]: ../general/host.md
[Guest]: ../general/guest.md
[identifier]: ./
[external kind]: ./
[index space]: ../general/index-space.md

[Function]: ./function.md
[Table]: ./table.md
[Memory]: ./memory.md
[Global]: ./global.md


# Import (Module)

An import represents some resource that a [Module] needs to be supplied in order to work.

| Field Name      | Type                 | Description                              |
| --------------- | -------------------- | ---------------------------------------- |
| `module_name`   | [identifier]         | the name of the module to import from    |
| `export_name`   | [identifier]         | the name of the export in that module    |
| `kind`          | [external kind]      | the kind of import                       |

Instantiating a Module requires the embedding to bind items of the correct type to each import,
which is called [parametric linking](../general/parametric-linking.md).

Functionally, imports take an externally-defined item and bring it into the corresponding [index space] for that items type.

## Import Types

* [Function]
    * A function import specifies the signature type for the function.
    * The function supplied for an import must have the specified type.
* [Table]
    * The table supplied for an import can't have a smaller minimum than requested by the module.
    * If a table import has a specified maximum, the supplied table must have an import and it must be at least as large.
* [Memory]
    * The memory supplied for an import can't have a smaller minimum than requested by the module.
    * If a memory import has a specified maximum, the supplied memory must have an import and it must be at least as large.
* [Global]
    * Imported globals must be immutible.

## Import Binding

When a [Module] is instantiated, its imports can be satisfied by either the [Host] or another [Guest] Module.