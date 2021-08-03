# CockroachDB Deep Dive for Hackathon

Supporting code, links, docs

## Install and Run CockroachDB

### Install Homebrew
```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Use Homebrew to install CockroachDB
```
$ brew install cockroachdb/tap/cockroach
```

[Other installation options](https://www.cockroachlabs.com/docs/stable/install-cockroachdb-mac.html)

### Start a 3 node CockroachDB cluster

```
cockroach start --insecure --listen-addr=localhost:26257 --join=localhost:26257,localhost:26258,localhost:26259 \
  --http-addr=localhost:8080 --store=cockroach-data-1 --background

cockroach start --insecure --listen-addr=localhost:26258 --join=localhost:26257,localhost:26258,localhost:26259 \
  --http-addr=localhost:8081 --store=cockroach-data-2 --background

cockroach start --insecure --listen-addr=localhost:26259 --join=localhost:26257,localhost:26258,localhost:26259 \
  --http-addr=localhost:8082 --store=cockroach-data-3 --background
  
cockroach init --host localhost:26258 --insecure
```

[DB Console](http://localhost:8080) is the admin UI.

### Connect using SQL CLI

```
cockroach sql --insecure
```

**NOTE:** This assumes `cockroach` is on your `PATH`.

### Add a fourth node to scale the cluster out

```
cockroach start --insecure --listen-addr=localhost:26260 \
  --join=localhost:26257,localhost:26258,localhost:26259 \
  --http-addr=localhost:8083 --store=cockroach-data-4 --background
```

