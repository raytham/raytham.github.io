# Workspaces

$GOPATH/ | Description
----------|------------
src/ | This contains your source code.
bin/ | Compiled executables go here.
pkg/ | Compiled packages go here.

## Source Code Organization
Within ``$GOPATH/src` are subdirectories that represent your packages. A package may contain multiple source code files, or just a single one. The top level directories are usually the code repositories that version control the packages.

```
$GOPATH/src/
  myrepo/
    .git/
    mypackage/
      mycode.go
```

When you compile your code with the `go` tool, you specify your package by passing the to it in relation to `$GOPATH/src/`.

```
go install myrepo/mypackage
```
