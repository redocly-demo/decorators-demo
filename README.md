## Demo of decorators to override descriptions

- `info-description-override`
- `operation-description-override`
- `tag-description-override`

## Result

Original: https://without-decorators.redoc.ly/
With decorators: https://preview.redoc.ly/without-decorators/decorators-demo/

### `info-description-override`
<img width="1005" alt="2021-11-03_18-23-53" src="https://user-images.githubusercontent.com/1161871/140232772-502fe663-8af7-4da6-a345-21b8067129bc.png">

### `tag-description-override`

<img width="783" alt="2021-11-03_18-30-53" src="https://user-images.githubusercontent.com/1161871/140233049-e36a1bcc-4267-41b8-b646-6159a282d54a.png">

### `operation-description-override`

<img width="996" alt="2021-11-03_18-32-43" src="https://user-images.githubusercontent.com/1161871/140233186-50d4cf13-46bc-4414-8231-35f87179825e.png">


## Problem

These built-in decorators solve the age-old problem of not being able to modify the OpenAPI definition at the source. This typically happens for code-generated OpenAPI definitions. Developers can use code annotations to describe the APIs, and then run a command that pulls together an OpenAPI file. 

One of the drawbacks is that any edits made to that file will be overwritten the next time the file is generated again. 

Technical writers, and other non-developer contributors, don't have access to the source code (or sometimes the code annotations library itself is limited).

## Solution

Use decorators to decorate the OpenAPI file. When the original OpenAPI file changes, the decorators run when bundling and update it accordingly.

`bundle` command + decorator + original OpenAPI file = new OpenAPI file

1. Add Markdown files with the new descriptions for operations, info, and tags. 
2. Adjust the configuration file (`redocly.yaml`) (or [create one](https://redocly.com/docs/cli/configuration/)) -- it should have the decorators object. See the [`redocly.yaml` configuration file](./redocly.yaml) in this repository for an example.
3. Run the [bundle command](https://redocly.com/docs/cli/commands/bundle/): `redocly bundle decorators@v1`.

<!-- NTD: confirm use case

When a team autogenerates an OpenAPI file, they can push it straight into Redocly's API registry, instead of committing the artifact to a Git repository. The other team can use it as the root source in the file repository using the corresponding registry OpenAPI link:

```yaml
apis:
  decorators@v2:
    root: https://api.redocly.com/registry/bundle/testing_acme/demo%20decorators/v1/openapi.yaml?branch=main
    lint:
      decorators:
          # ...
```

Every time that API is updated by developers, the corresponding usage will be automatically updated as well. -->
