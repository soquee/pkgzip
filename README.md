# pkgzip

The **pkgzip** command bundles assets into a Go package.
It is a fork of [statik] that changes the API of the package to not require
import side effects.

To use this tool in your Go project, add it to your `tools.go` file, and add a
[Go Generate] line (this doesn't necessarily have to be in `tools.go`) similar
to the one in the following example:

```go
//go:generate go run code.soquee.net/pkgzip -m -f -src assets -pkg assetsfs

// +build tools

package main

import (
	_ "code.soquee.net/pkgzip"
)
```

Then update your `go.mod` file with the specific version you want (use `go get
-u` to get the latest), and run `go generate tools.go` (or wherever you put the
comment) to generate your assets package.
It's probably easiest to do this from your Makefile like so:

```make
mybin: internal/assetsfs/pkgzip.go
	go build -o $@

internal/assetsfs/pkgzip.go: $(MYASSETS)
	go generate tools.go
```


## License

The package may be used under the terms of the BSD 2-Clause License a copy of
which may be found in the [`LICENSE`] file.

Unless you explicitly state otherwise, any contribution submitted for inclusion
in the work by you shall be licensed as above, without any additional terms or
conditions.

Parts of this work are copied from [statik] and used under the terms of the
Apache License Version 2.0, a copy of which can be found in the file
[`LICENSE.apache`].

[statik]: https://github.com/rakyll/statik
[`go generate`]: https://golang.org/pkg/cmd/go/#hdr-Generate_Go_files_by_processing_source
[`LICENSE`]: ./LICENSE
[`LICENSE.apache`]: ./LICENSE.apache
[Go Generate]: https://golang.org/pkg/cmd/go/#hdr-Generate_Go_files_by_processing_source
[the wiki]: https://github.com/golang/go/wiki/Modules#how-can-i-track-tool-dependencies-for-a-module
