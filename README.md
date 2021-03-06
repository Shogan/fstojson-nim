# fstojson-nim

A simple CLI tool to traverse a target directory & output the collected 
hierarchy to JSON. This is my first attempt at writing something in the [Nim language](https://nim-lang.org/).

## Build and Install

`nimble install`

## Usage

```
fstojson

Usage:
  fstojson [-p | --pretty] [-r | --recurse] PATH

Arguments:
  PATH          The path to begin traversing

Options:
  -h --help     Show this screen.
  --version     Show version.
  -p --pretty   Pretty print JSON
  -r --recurse  Recusively traverse paths.
```

For example:

Output a target path in the filesystem (as well as it's contents) as a JSON string:

`fstojson PATH`

Output a target path in the filesystem (recursive) and all contents as a JSON string:

`fstojson -r PATH`

Add the `-p` argument to output the JSON in prettified print.

`fstojson -r -p PATH`

```json
{
  "name": "temp",
  "relativePath": "temp",
  "absolutePath": "/Users/seand/Git/sean/fstojson/temp",
  "fileSizeBytes": null,
  "nodeType": "directory",
  "children": [
    {
      "name": "temp/abc.txt",
      "relativePath": "abc.txt",
      "absolutePath": "/Users/seand/Git/sean/fstojson/temp/abc.txt",
      "fileSizeBytes": 1341,
      "nodeType": "file",
      "children": []
    },
    {
      "name": "temp/f2",
      "relativePath": "f2",
      "absolutePath": "/Users/seand/Git/sean/fstojson/temp/f2",
      "fileSizeBytes": null,
      "nodeType": "directory",
      "children": [
        {
          "name": "temp/f2/f2sub1",
          "relativePath": "f2sub1",
          "absolutePath": "/Users/seand/Git/sean/fstojson/temp/f2/f2sub1",
          "fileSizeBytes": null,
          "nodeType": "directory",
          "children": []
        },
        {
          "name": "temp/f2/f2file.log",
          "relativePath": "f2file.log",
          "absolutePath": "/Users/seand/Git/sean/fstojson/temp/f2/f2file.log",
          "fileSizeBytes": 2303,
          "nodeType": "file",
          "children": []
        }
      ]
    }
  ]
}
```

### fstojson with jq

Of course you can pass the output of fstojson to tools like jq via the pipeline:

Getting just the absolute paths of files within a particular directory:

`fstojson temp/somedir | jq '.children[].absolutePath'`

```text
/Users/seand/Git/sean/fstojson/temp/f1/f1sub1/a-file.txt
/Users/seand/Git/sean/fstojson/temp/f1/f1sub1/empty-dir
```

## Notes

- Directory content at each level may not necessarily be sorted alphabetically.
