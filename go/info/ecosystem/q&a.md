<!-- TOC -->
* [Q&A](#qa)
  * [Questions](#questions)
  * [Answers](#answers)
<!-- TOC -->

# Q&A
## Questions

1. How does Golang manage its dependencies?
2. What native Golang tools do you know? (get, build, format, test, etc)
3. How to host third-party library locally (for debug or development purpose)?
4. What types of imports do you know?
5. Which go static analysis tools do you know? What are the differences between them?
6. What build flags do you know?
7. What are profiling and tracing used for? In case of pprof explain, how do you work with it?
8. Describe project structure you would use for library/service/application? Describe pros/cons.
9. What are GOPROXY, GOPRIVATE and GOSUMDB used for?

## Answers
1. Go manages its dependencies using the `go.mod` file. This file defines the module’s module path and its dependency requirements.
2. Native Go tools include `go get` for fetching and installing packages, `go build` for compiling Go sources, `go test` for running tests, and many more.
3. To host a third-party library locally, you can clone the repository and use `replace` directive in the `go.mod` file to redirect to your local copy.
4. Go has two types of imports: standard library imports and third-party imports.
5. Go static analysis tools include `golint` for style checks, `go vet` for examining code for common mistakes, and `staticcheck` for detecting bugs and performance issues.
6. Build flags in Go include `-o` for specifying the output file name, `-i` for installing packages, `-v` for verbose output, and many more.
7. Profiling and tracing are used for performance tuning in Go. The `pprof` package provides tools for profiling and tracing Go programs.
8. A typical Go project structure includes directories for `cmd`, `pkg`, `api`, `web`, `scripts`, etc. This structure helps in separating concerns, making the project easier to navigate and maintain.
9. `GOPROXY` is used to specify a Go proxy service, `GOPRIVATE` is used to bypass the proxy for private modules, and `GOSUMDB` is used to specify a checksum database.
