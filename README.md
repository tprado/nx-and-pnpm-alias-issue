# nx and pnpm aliases issue

When a dependency is declared using [pnpm's aliases](https://pnpm.io/aliases) feature:


```json
{
  "dependencies": {
    "shared-lib": "workspace:*",
    "another-shared-lib-alias": "workspace:another-shared-lib@*"
  }
}
```

`nx` does not recognize it, leaving it out of the dependency tree.

## Workaround

It is necessary to add it in the list of `implicitDependencies` of the consumer package.

```json
{
  "implicitDependencies": [
      "another-shared-lib"
  ]
}
```
