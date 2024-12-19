# DappsterOS-CLI

[![Go Reference](https://pkg.go.dev/badge/github.com/dappsteros-io/DappsterOS-CLI.svg)](https://pkg.go.dev/github.com/dappsteros-io/DappsterOS-CLI) [![Go Report Card](https://goreportcard.com/badge/github.com/dappsteros-io/DappsterOS-CLI)](https://goreportcard.com/report/github.com/dappsteros-io/DappsterOS-CLI) [![goreleaser](https://github.com/dappsteros-io/DappsterOS-CLI/actions/workflows/release.yml/badge.svg)](https://github.com/dappsteros-io/DappsterOS-CLI/actions/workflows/release.yml) [![codecov](https://codecov.io/github/dappsteros-io/DappsterOS-CLI/branch/main/graph/badge.svg?token=XHM6PM8C0K)](https://codecov.io/github/dappsteros-io/DappsterOS-CLI)

A command-line tool to interact with DappsterOS for testing and diagnosing purpose

## Usage

```text
A command line interface for DappsterOS

Usage:
  dappsteros-cli [command]

Services
  app-management All compose app management and store related commands
  local-storage  All local storage related commands
  message-bus    All message bus related commands

Additional Commands:
  completion     Generate the autocompletion script for the specified shell
  help           Help about any command
  version        Show version

Flags:
  -h, --help              help for dappsteros-cli
  -u, --root-url string   root url of DappsterOS API (default "localhost:80")

Additional help topics:
  dappsteros-cli gateway        All gateway related commands
  dappsteros-cli user           All user related commands

Use "dappsteros-cli [command] --help" for more information about a command.
```

## Contributing

Use <https://github.com/spf13/cobra-cli> to add any new command.

Follow example steps below to add commands like `dappsteros-cli message-bus list event-types`

1. create command scaffold with `cobra-cli add`:

    ```shell
    go run github.com/spf13/cobra-cli@latest add messageBus --config .cobra.yaml
    go run github.com/spf13/cobra-cli@latest add messageBusList -p messageBusCmd --config .cobra.yaml
    go run github.com/spf13/cobra-cli@latest add messageBusListEventTypes -p messageBusListCmd --config .cobra.yaml
    ```

    > It is important to include `--config .cobra.yaml` to attribute the scaffold code with correct license header.

2. update each `messageBus*.go` file with correct command format:

    ```go
    // messageBus.go
    Use:   "messageBus",
    // messageBusList.go
    Use:   "messageBusList",
    // messageBusListEventTypes.go
    Use:   "messageBusListEventTypes",
    ```

    becomes

    ```go
    // messageBus.go
    Use:   "message-bus",
    // messageBusList.go
    Use:   "list",
    // messageBusListEventTypes.go
    Use:   "event-types",
    ```

3. update short and long description for each command, and implement the logics

4. to verify the commands are created correctly, run

    ```shell
    $ go run main.go message-bus list event-types --help
    list event types

    Usage:
    DappsterOS-CLI message-bus list event-types [flags]

    Flags:
    -h, --help   help for event-types
    ```

> Run `go run github.com/spf13/cobra-cli@latest --help` to see additional help message.

