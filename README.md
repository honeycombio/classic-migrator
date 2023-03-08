# Honeycomb Classic-Migrator

The Honeycomb Classic Migrator is a tool designed to streamline the process of migrating your features and configurations (boards, derived columns, triggers, etc) from [Honeycomb Classic](https://docs.honeycomb.io/honeycomb-classic/) to our modern [Environments & Services](https://changelog.honeycomb.io/preview-new-environments-and-services-functionality-in-honeycomb!-227356) data model.

Classic Migrator is distributed as a single binary (built by Go), which serves a web interface to the user, guiding them through all the necessary migration steps. It fetches all needed depencies and places them in the working dir (specified on the command line as `--working-dir`).

## Running the Classic-Migrator

### Building it:
```
cd <this repo>
go build -o classic-migrator .
strip classic-migrator
```
### Standard run:
```
$ classic-migrator --listen-on localhost:8000 --working-dir /tmp/foo
Welcome to the Honeycomb Classic Migrator! version: dev

Using working directory: /tmp/foo (override with --working-dir)
To get started, visit http://localhost:8000 in your browser.
```

### Dev mode:
```
cd <this repo>
export ENV=development
go run . --working-dir /tmp/foo
```
