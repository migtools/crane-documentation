---
title: "Export"
date: 2021-11-16T12:37:12-05:00
draft: false
---

First step of the migration is to export resource from a source cluster. This `export` command provides means of extracting resources from any namespace desired. This is a required step of the process and has to be the first step of the process as input of subsequent commands depends on the output of `export`.

#### Examples

```
crane export -n foo -e export --context demo
```

```
cat << EOF >> conf.yaml
namespace: foo
export-dir: export
context: demo
EOF

crane export -c conf.yaml
```

```
cat << EOF >> conf.yaml
namespace: foo
export-dir: export
context: testing
EOF

crane export -c conf.yaml --context demo

# Note the difference is we are overriding "context" here with flag
```

All the above command will export contents of `foo` namespace in to local dir `export` with the context `demo` defined in `KUBECONFIG`.

It is also possible to restrict the export of resources with a label selector:
```
crane export -l "app=mariadb-2,service=mariadb"
```

<b>Note: </b> there are few ways to provide input to a command, precedence of which is `input from flags > input from config file > env variables > default values` (not all the flags can have corresponding env variable). And this behavior persist across all the commands of crane cli.
