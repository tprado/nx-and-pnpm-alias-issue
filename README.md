# nx and pnpm aliases issue

When a dependency is declared using [pnpm's aliases](https://pnpm.io/aliases) notation:

```json
{
  "dependencies": {
    "shared-lib": "workspace:*",
    "another-shared-lib-alias": "workspace:another-shared-lib@*"
  }
}
```

`nx` does not recognize it, leaving it out of the dependency tree.

Here's the output of the graph command.

```
$ pnpm exec nx graph
```

![image](https://github.com/user-attachments/assets/f2d98227-67b5-40b1-9df2-3a55d66cfdba)

And here how the dependency is available at runtime.

```
$ pnpm list -r

Legend: production dependency, optional only, dev only

/nx-and-pnpm-alias-issue

devDependencies:
nx 19.5.3

my-app /nx-and-pnpm-alias-issue/apps/my-app

dependencies:
another-shared-lib-alias link:../../libs/another-shared-lib
shared-lib link:../../libs/shared-lib
```




## Workaround

It is necessary to add it in the list of `implicitDependencies` of the consumer package.

```json
{
  "implicitDependencies": [
      "another-shared-lib"
  ]
}
```
