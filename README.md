Bash Clash!
===========

A powerful bash argument parser.

Use Bash Clash to interpret arguments to your shell scripts - e.g.:

```
$script --switch value --flag -- positional-argument
```

Bash Clash will parse:
  - _switches_ with or without the _=_ assignment operator and with space-separated values
  - _flags_ without a value as `true` (can be explicitly overridden)
  - _positionals_ in any position in the argument list when indicated by the `--` separator

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

```
source "$bash_clash" --foo bar
# bash_clash_switches=(
    foo=bar
)

source "$bash_clash" --foo=bar
# $bash_clash_switches(
    foo=bar
)

source "$bash_clash" --foo bar --bar
# bash_clash_switches=(
    foo=bar
    bar=true
)

source "$bash_clash" --foo bar --bar=false
# bash_clash_switches=(
    foo=bar
    bar=false
)


source "$bash_clash" --foo bar space-separated values --bar
# bash_clash_switches=(
    foo=bar space-separated values
    bar=true
)

source "$bash_clash" --foo bar space-separated values -- positional-argument --bar
# bash_clash_switches=(
    foo=bar space-separated values
    bar=true
)
# bash_clash_positionals=(
    positional-argument
)
```
