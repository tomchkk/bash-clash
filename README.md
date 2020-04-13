Bash Clash!
===========

A powerful bash argument parser.

## Usage

_source_ this file in your bash script, passing in your arguments, and they
will be parsed into `bash_clash_switches` and `bash_clash_positionals`;
bash arrays containing the values of the parsed arguments.

Both arrays – and optionally, using the `--declare` flag – all of the
arguments parsed as `bash_clash_switches` - will be available within the
context of your calling shell process.

```
source "$bash_clash" "$@"

source "$bash_clash" --declare "$@"
```

## Examples

TODO: example input and output
