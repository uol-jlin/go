# Embed Directive

Package embed provides access to files embedded in the running Go program.

Go source files that import "embed" can use the `//go:embed` **compiler directive**.
* The directive initialize a variable of type **string, []byte, or FS** with the contents of files read from the package directory or subdirectories at **compile time**.

Three ways to embed a file named `hello.txt `and then print its contents at run time.

## Embedding one file into a string:

```go
import _ "embed"

//go:embed hello.txt
var s string
print(s)
```

## Embedding one file into a slice of bytes:

```go
import _ "embed"

//go:embed hello.txt
var b []byte
print(string(b))
```

## Embedded multiple files or even folders with wildcards:

This uses a variable of the `embed.FS` type, which implements a simple **virtual file system**.

```go
//go:embed folder/single_file.txt
//go:embed folder/*.hash
var folder embed.FS
```

Retrieve some files from the embedded folder.

```go
content1, _ := folder.ReadFile("folder/file1.hash")
print(string(content1))
content2, _ := folder.ReadFile("folder/file2.hash")
print(string(content2))
```
