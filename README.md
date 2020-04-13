Bash Clash!
===========

A powerful bash argument parser
-------------------------------

Use Bash Clash to interpret arguments to your shell scripts - e.g.:

```
$script --switch value --flag -- positional-argument
```

Bash Clash will parse:
  - _switches_ (named value arguments):
    - with short or long _handles_ (_-s_|_--switch_)
    - with or without an assignment operator (_-s=value_|_--s value_)
    - with space-separated values (_-s with values_)
  - _flags_ (named boolean arguments):
    - without a value as `true` (can be explicitly overridden)
  - _positionals_ (unnamed value arguments):
    - in any position in the argument list when preceded by the `--` separator

Bash Clash can handle all orders and variations of the above and will optionally declare all named arguments, so they're available within the context of your calling shell process.

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

### Switches

```
source "$bash_clash" --foo bar --bar=foo
# bash_clash_switches=(
    foo=bar
    bar=foo
)
```
```
source "$bash_clash" --foo bar space-separated value --bar="f o o"
# bash_clash_switches=(
    foo=bar space-separated value
    bar=f o o
)
```

### Flags

```
source "$bash_clash" --bar
# bash_clash_switches=(
    bar=true
)
```
```
source "$bash_clash" --bar=false
# bash_clash_switches=(
    bar=false
)
```



### Positionals

```
source "$bash_clash" --foo bar -- positional-arg1 positional-arg2 --bar=foo
# bash_clash_switches=(
    foo=bar
    bar=foo
)
# bash_clash_positionals=(
    positional-arg1
    positional-arg2
)
```
