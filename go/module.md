### Introduction

- Ability to work with Go code outside of the GOPATH workspace.
- Ability to version a dependency and identify the most compatible version to use.
- Ability to manage dependencies natively using the Go tooling.





## GOPATH

Before modules, if you wanted to use this package, you would use `go get` to clone a copy of the repo inside your GOPATH using the canonical name of the repo as its exact location on disk.The canonical name being a combination of the root of the remote repository and the name for the repo.



## go.mod

It was decided to name this special file [`go.mod`](https://golang.org/cmd/go/#hdr-The_go_mod_file) and the canonical name for the repo defined inside the file would represent this new entity called a module. These file **$GOPATH/pkg/mod/**



## Bundling and Versioning

#### before module

- You can’t use a version of the `conf` package in your own project unless you also clone all the repos for the packages that `conf` depends on. This is a problem for all of your project’s transitive dependencies.

- `go get` only knows how to clone and update the latest code from the `master` branch for each dependency. Pulling code from the `master` branch for each dependency might be fine when you write your initial code.

#### module

- there is supporting the use of different major semantic versions of the same dependency within your project incase your dependencies are importing different major versions of the same package.

#### integrated solution

The solution was to reuse the module file to maintain a list of direct and sometimes indirect dependencies by version. Then treat any given version of a repo as a single immutable bundle of code. This versioned immutable bundle is called a module.



## gopls

> To provide editors with support for modules (and for other reasons), the Go team built a service named [gopls](https://github.com/golang/tools/blob/master/gopls/doc/user.md) which implements the language server protocol ([LSP](https://microsoft.github.io/language-server-protocol/)).The idea of the protocol is to provide editors with support for language features such as auto complete, go to definition, and find all references.



## module cache

 That cache can be found at `$GOPATH/pkg`. If you don’t have a GOPATH setup, the default GOPATH is at `$HOME/go`.

clean module cache :  **go clean -modcache** 

initialize the root of your project’s source tree :**go mod init**

get transitive module,remove dependingdencies,download module :**go mod tidy**

A quick way to get the gopls internal module cache back in sync with the local module cache is to reload the VS Code editor. This will restart the gopls server and reset its internal module cache. In VS Code, there is a special command called `reload window` to do just this.





The Go tooling can follow the path of module files to get a complete picture of all the modules needed to build or test code.



## MVS (minimal version selection)









## reference

https://www.ardanlabs.com/blog/2019/10/modules-01-why-and-what.html

https://www.ardanlabs.com/blog/2019/12/modules-02-projects-dependencies-gopls.html

https://www.ardanlabs.com/blog/2019/12/modules-03-minimal-version-selection.html