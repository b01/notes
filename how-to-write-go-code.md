# How to Write Go Code 

[link](https://golang.org/doc/code.html)

## Code Organization

### Facts

* Go programs are organized into packages, see __packages__ in [Terms](#terms) section.
* Functions, types, variables, and constants defined in one source file are visible to all other source files within the same package.
* A repository contains one or more modules.
* A file named `go.mod`, at the root of a package, declares the module path: the import path prefix for all packages within the module, and as an indicator where to download the package.

## Your First Program

### Facts

* The first statement in a Go source file must be package name. Executable commands must always use package main.
* The install directory is controlled by the GOPATH and GOBIN environment variables. If GOBIN is set, binaries are installed to that directory. If GOPATH is set, binaries are installed to the bin subdirectory of the first directory in the GOPATH list. Otherwise, binaries are installed to the bin subdirectory of the default GOPATH ($HOME/go or %USERPROFILE%\go).
* Commands like go install apply within the context of the module containing the current working directory. If the working directory is not within the example.com/user/hello module, go install may fail.
* The `go` command locates the repository containing a given module path by requesting a corresponding HTTPS URL and reading metadata embedded in the HTML response. The easiest way to make your module available for others to use is usually to make its module path match the URL for the repository.
* Functions beggining with an upper-case letter, are exported, and can be used in other packages.

* `go build` won't produce an output file. Instead it saves the compiled package in the local build cache.
* Module dependencies are automatically downloaded to the `$GOPATH/pkg/mod`. Thay are marked read-only as the contents for a given version are shared among all other modules that require them.

## Testing

* Go has a lightweight test framework composed of the `go test` command and the `testing` package.
* You write a test by creating a file with a name ending in `_test.go` that contains functions named `TestXXX` with signature `func (t *testing.T)`. The test framework runs each such function; if the function calls a failure function such as `t.Error` or `t.Fail`, the test is considered to have failed. 
*  Run the test with `go test`.

## Terms

* package is a collection of source files in the same directory that are compiled together.
* An import path is a string used to import a package. A package's import path is its module path joined with its subdirectory within the module.
