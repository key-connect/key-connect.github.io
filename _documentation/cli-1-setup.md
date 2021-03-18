---
# Page settings
title: Setting up the CLI # Define a title of your page
description: How to setup Key Connect CLI # Define a description of your page
keywords: keyconnect cli blockchain eth xrp # Define keywords for search engines
order: 4 # Define order of this page in list of all documentation documents
comments: false # Set to "true" in order to enable comments on this page. Make sure you properly setup "disqus_forum_shortname" variable in "_config.yml"

# Hero section
hero:
    title: Setting up the CLI
---

Download latest CLI jar from the [mvnrepository](https://mvnrepository.com/artifact/app.keyconnect/keyconnect-cli) site.

```shell
wget -O kc.jar https://repo1.maven.org/maven2/app/keyconnect/keyconnect-cli/1.1.0/keyconnect-cli-1.1.0.jar
```

You will need at least JRE 11 installed on your system to run the CLI.

**Help needed** in turning this into a native executable, see github issue [#31](https://github.com/key-connect/services/issues/31).

For now you could use system aliases or functions to make the CLI easily accessible.

```shell
# linux and macos
alias kc="java -jar path/to/kc.jar"
```

From here on we will refer to `java -jar path/to/kc.jar` as `kc` command.

Test that CLI is able to run by running the status command:

```shell
$ kc status
class AvailableBlockchains {
    blockchains: [class BlockchainStatus {
        chainId: eth
        networks: [class BlockchainNetwork {
            group: mainnet
            servers: [class BlockchainNetworkServerStatus {
                host: mainnet.infura.io
                status: healthy
                lastCheck: 2021-03-18T08:13:14.449966049Z
            }]
        }, class BlockchainNetwork {
            group: ropsten
            servers: [class BlockchainNetworkServerStatus {
                host: ropsten.infura.io
                status: healthy
                lastCheck: 2021-03-18T08:13:15.007920146Z
            }]
        }]
    }, class BlockchainStatus {
        chainId: xrp
        networks: [class BlockchainNetwork {
            group: testnet
            servers: [class BlockchainNetworkServerStatus {
                host: s.altnet.rippletest.net
                status: healthy
                lastCheck: 2021-03-18T08:13:15.234040799Z
            }]
        }, class BlockchainNetwork {
            group: devnet
            servers: [class BlockchainNetworkServerStatus {
                host: s.devnet.rippletest.net
                status: healthy
                lastCheck: 2021-03-18T08:13:15.664170027Z
            }]
        }, class BlockchainNetwork {
            group: mainnet
            servers: [class BlockchainNetworkServerStatus {
                host: s2.ripple.com
                status: healthy
                lastCheck: 2021-03-18T08:13:16.099504840Z
            }, class BlockchainNetworkServerStatus {
                host: s1.ripple.com
                status: healthy
                lastCheck: 2021-03-18T08:13:16.702404379Z
            }]
        }]
    }]
}
```

#### Output Formats

The Key Connect CLI supports three output formats
1. Default output format
2. JSON
3. YAML

The default format is what you see above. You can switch between json or yaml formats by providing the flags `--json` or `--yaml` respectively. 

#### Debugging

In case you are having issues, you can use the `--api-debug` flag to enable debug output which could help you in diagnosing the issue.

#### Usage

To view available commands, use the `-h` option directly:

```shell
$ kc -h
Usage: kc [-hV] [COMMAND]
Key Connect command line interface
  -h, --help      Show this help message and exit.
  -V, --version   Print version information and exit.
Commands:
  server-status, server, srv               Print server status
  status, s                                Print high-level status of supported
                                             block chains
  accounts, a                              Print information for a given
                                             account / wallet address
  account-transactions, transactions, txs  Print transactions for a given
                                             account / wallet address
  transaction, tx, txn, hash               Print details of a given transaction
                                             ID (hash)
  fees                                     Print fees for a given blockchain
  rate                                     Currency conversion rates
  fund, f                                  Funds a given account in test
  init                                     Initialize local wallet
  new                                      Creates a new wallet
  wallets                                  View information about local wallets
  export                                   Export the local wallet mnemonic and
                                             seed passphrase
  rename, rename-wallet                    Rename a given local wallet
  pay                                      Make a payment
Exit codes:
  10            Generic non-api related error, mostly an issue with the CLI or
                  the environment
  20            Network or connection related error
  [HTTP Code]   Exit code is the HTTP status code returned by the server
```

You can view usage information for a specific command by providing the `-h` option on that specific command. For example:

```shell
$ kc accounts -h
Missing required option: '--chainid=<chainId>'
Usage: kc accounts [--api-debug] [--json] [--yaml] [-a=<accountAddress>]
                   -c=<chainId> [-f=<fiat>] [-n=<network>]
                   [--name=<walletName>] [-s=<baseUri>]
Print information for a given account / wallet address
  -a, --account=<accountAddress>
                             Account address (not required if --name is
                               specified)
      --api-debug            Debug API request/responses
  -c, --chainid=<chainId>    ID of the blockchain
  -f, --fiat=<fiat>          Fiat currency to convert value in
      --json, --print-json   Print output in JSON format
  -n, --network=<network>    Blockchain network, if other than server-side
                               default
      --name=<walletName>    Local wallet name (not required if --account is
                               specified)
  -s, --server=<baseUri>     Base URI of the server, if other than production
                               https://api.keyconnect.app
      --yaml, --print-yaml   Print output in YAML format
```
