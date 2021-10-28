# Using the Koinos CLI

The Koinos Command Line Interface (CLI) is a comprehensive command line tool for interacting with the Koinos Blockchain.

## Installing and starting the CLI

The latest release can be downloaded from [GitHub](https://github.com/koinos/koinos-cli).

Start the CLI with the binary included in the archive.

## Basic usage

When running the wallet, it will start in interactive mode. Press tab or type `list` to see a list of possible commands.

`help <command-name>` will show a help message for the given command.

Some commands require a node RPC endpoint. This can be specified either when starting the CLI with `--rpc` command line switch, or with the `connect` command from within the CLI. Both take an endpoint url.

There is a public RPC server that may be used for testing at this address: `http://192.241.131.189:8080`

If there is a red symbol to the left of the prompt, it indicates that you are not connected to an RPC endpoint.

`exit` or `quit` will quit the wallet.

## Wallet creation & management

The lock symbol to the left of the prompt indicates whether or not you have a wallet open. Some commands require an open wallet.

To create a new wallet, use the command `create <filename> <password>`. The new wallet will then be created in the given file, and automatically opened.

To open a previously created wallet, use the command `open <filename> <password>`.

To import an existing Wallet Import Format (WIF) private key, use the commands `import <wif> <filename> <password>`.

To close an open wallet, simply use the `close` command.

Any of the commands which take a password may be called with it omitted. In this case it will use the value in the `WALLET_PASS` environment variable / .env file.

## Other useful commands

To check the balance of a given public address, use the command `balance <address>`.

To transfer tKOIN from the currently open wallet, use the command `transfer <amount> <address>`.

## Smart contract management

Note: Smart contract management will change in the future to be much easier to work with.

To upload a smart contract, use the command `upload <filename>`. The file given should be a compiled wasm smart contract. The contract id will be the public address of the currently open wallet.

To read from a smart contract, use the command `read <contract-id> <entry-point> <arguments>`. Entry-point should be a hex value such as 0x0D, as defined in the contract. Arguments should be a base64 string representing the binary arguments the entry-point requires.

To call a smart contract, use the command `call <contract-id> <entry-point> <arguments>`. The parameters here are given the same way as in the read command described above.

## Transaction sessions

Sometimes it is important to ensure multiple operations are included in the same block in a specific order. To accomplish this with the CLI, you use a session.

To begin a session, use the command `session begin`. A paper icon will appear to the left of the prompt while a session is active.

Any command that interacts with the chain will now be added to the current session.

To view the current session, use `session view`.

To cancel the current session, use `session cancel`.

When you are done adding commands to the session, `session submit` will send the attached commands as a single transaction to the blockchain.

## Non-interactive mode

Commands can be executed without using interactive mode. The `--execute` command-line parameter takes a semicolon separated list of commands, executes them, then returns to the terminal.
