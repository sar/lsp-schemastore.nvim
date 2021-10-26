# SchemaStore.nvim [![Version](https://img.shields.io/github/v/tag/b0o/schemastore.nvim?style=flat&color=yellow&label=version&sort=semver)](https://github.com/b0o/schemastore.nvim/releases) [![License: Apache 2.0](https://img.shields.io/github/license/b0o/schemastore.nvim?style=flat&color=green)](https://www.apache.org/licenses/LICENSE-2.0) [![Test Status](https://img.shields.io/github/workflow/status/b0o/schemastore.nvim/test?label=tests)](https://github.com/b0o/schemastore.nvim/actions/workflows/test.yaml) [![Build Status](https://img.shields.io/github/workflow/status/b0o/schemastore.nvim/generate)](https://github.com/b0o/schemastore.nvim/actions/workflows/generate.yaml)

A Neovim Lua plugin providing access to the [SchemaStore](https://github.com/SchemaStore/schemastore) catalog.

## Install

[Packer](https://github.com/wbthomason/packer.nvim):

```lua
use "b0o/schemastore.nvim"
```

## Usage

To use SchemaStore.nvim with [lspconfig](https://github.com/neovim/nvim-lspconfig/blob/master/CONFIG.md#jsonls) + [jsonls](https://github.com/hrsh7th/vscode-langservers-extracted):

```lua
require'lspconfig'.jsonls.setup {
  settings = {
    json = {
      schemas = require'schemastore'.json.schemas(),
    },
  },
}
```

To use a subset of the catalog, you can select schemas by name (see [the catalog](https://github.com/SchemaStore/schemastore/blob/master/src/api/json/catalog.json) for a full list):

```lua
require'lspconfig'.jsonls.setup {
  settings = {
    json = {
      schemas = require'schemastore'.json.schemas {
        select = {
          '.eslintrc',
          'package.json',
        },
      },
    },
  },
}
```

If you want to use your own schemas in addition to schemas from SchemaStore, you can merge them:

```lua
require'lspconfig'.jsonls.setup {
  settings = {
    json = {
      schemas = vim.tbl_extend('force', {
        {
           description = "My Custom JSON schema",
           fileMatch = { "foobar.json", ".foobar.json" },
           name = "foobar.json",
           url = "https://example.com/schema/foobar.json"
         },
      }, require'schemastore'.json.schemas {
        select = {
          '.eslintrc',
          'package.json',
        },
      },
    },
  },
}
```

## Changelog

```
15 Oct 2021                                                             v0.0.1
  Initial Release
```

## License

&copy; 2021 Maddison Hellstrom

Released under the Apache 2.0 License.
