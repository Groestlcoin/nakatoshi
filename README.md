# nakatoshi

[![](https://github.com/Groestlcoin/nakatoshi/workflows/Rust/badge.svg)](https://github.com/groestlcoin/nakatoshi/actions?query=workflow%3ARust)

A [Groestlcoin Vanity Address](https://github.com/bitcoinbook/bitcoinbook/blob/develop/ch04.asciidoc#vanity-addresses) generator.

nakatoshi accepts as input a prefix string (Or a file with multiple prefixes) to search for and produce
a Groestlcoin address and private / public keys. The amount of time required to find a given pattern depends
on how long the string is, the speed of your computer, and whether you get lucky.

## CLI

```
USAGE:
    nakatoshi [FLAGS] [OPTIONS] <prefix> --input-file <input-file>

FLAGS:
    -b, --bech32            Use Bech32 addresses. Starting with grs1q (Lowercase address)
    -c, --case-sensitive    Use case sensitive comparison to match addresses
    -h, --help              Prints help information
    -u, --uncompressed      Use uncompressed private an public keys
    -V, --version           Prints version information

OPTIONS:
    -i, --input-file <input-file>    File with prefixes to match addresses with
    -t, --threads <threads>          Number of threads to be used [default: The number of CPUs available on the current
                                     system]

ARGS:
    <prefix>    Prefix used to match addresses
```


## Examples:

#### Generate a vanity address

```shell
nakatoshi FKids
```

#### Generate a vanity address and parse JSON response

```shell
nakatoshi FBitc | jq
```

#### Use a file with multiple prefixes

A file with one address prefix on each newline can be used to search for a vanity
address. This reduces the time to find a result.

Example:

```shell
nakatoshi --input-file input.txt
```

The contents of the `input.txt` file looks like this:
```
FKids
FLove
```

#### Bech32 addresses

```shell
nakatoshi -b grs1qki
```

Note: There is no need to search with the `case-sensitive` flag because `grs1q` addresses are
always lowercase.

## Development

```shell
# Build
$ cargo build

# Help
$ cargo run -- -help
```

Note: `Cargo run` creates an unoptimized executable with debug info. When testing
the speed/throughput of the application, make sure to use `cargo run --release`.
