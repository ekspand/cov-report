# cov-report

_Generates aggregate go code coverage results._

`go test` can generate code coverage results and an overall coverage percentage, however it can
only do this one package at at time, also there are no mechanisms to exclude certain source
files from the calculation (e.g. you may want to exclude code generated files).

This tool will take one or more cover profiles generated by GO test and generate a summary
of the aggregate coverage across the set of cover profiles results. In addition you can
provide a regex to exclude files from the calculation, and get a summary of the files with
the least coverage.

## Build

If you want to manually build from source, clone the repo, and build with the standard go build tools.
You'll also need the dependency from golang.org/x/tools/cover [or the internal mirror]

`go install .`

## Usage

`cov-report [-fmt txt|json|xml] [-o results.file] [-u <num top uncovered files>] [-ex source file name exclusion regex] [-cc combined output filename] <coverprofileFile> ...`

e.g.

```.sh
./cov-report -ex "query_console|.*.pb.go" ~/code/ekspand/cov-report/cpt.out ~/code/ekspand/cov-report/cp.out
Statements
total:     203
covered:   182
uncovered: 21
excluded:
result:    89.7%

Top uncovered source files [name, uncovered count, total uncovered %]
 github.com/go-phorce/cov-report/cmd/cov-report/main.go     19    9.4%
 github.com/go-phorce/cov-report/version/versioninfo.go      1    0.5%
 github.com/go-phorce/cov-report/version/current.go          1    0.5%

```
