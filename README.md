# estringer

An extended version of the [`stringer`](https://pkg.go.dev/golang.org/x/tools/cmd/stringer) tool for go.

This tool extends `stringer` by adding a `StringTo<Type>()` function, returning the value corresponding a given string.
This function is generated when using the `-string-to-type` argument.

For example, given this snippet,
```go
package painkiller

type Pill int

const (
	Placebo Pill = iota
	Aspirin
	Ibuprofen
	Paracetamol
	Acetaminophen = Paracetamol
)
```
running this command
```
estringer -type=Pill -string-to-type
```
in the same directory will create the file `pill_string.go` as for the standard `stringer`, with addition of the function
```go
func StringToPill(v string) (Pill, bool)
```
