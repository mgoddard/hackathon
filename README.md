# CockroachDB Deep Dive for Hackathon

Supporting code, links, docs

[Slide deck (PDF)](./Hackathon_Build_with_CockroachDB.pdf)

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

## CockroachDB Geo Tourist demo

[Link to GitHub repo](https://github.com/cockroachlabs-field/crdb-geo-tourist#cockroachdb-geo-tourist)

## Serializable Isolation

[Hands on demo](https://www.cockroachlabs.com/docs/stable/demo-serializable.html)

[StackOverflow discussion](https://stackoverflow.com/questions/60339223/node-js-transaction-coflicts-in-postgresql-optimistic-concurrency-control-and) of adding support for retries

## TypeORM

[Installation and Quick Start](https://typeorm.io/#/)

## Ideas for Next Steps

* Continue with the “Step-by-Step Guide” section of the [TypeORM guide](https://typeorm.io/#/)
* Review the [`AS OF SYSTEM TIME` clause](https://www.cockroachlabs.com/docs/stable/as-of-system-time.html)
* Add AOST to TypeORM -- see [this GitHub issue](https://github.com/typeorm/typeorm/issues/4646)
* Explore multi-region capabilities with the help of [this demo](https://github.com/chriscasano/multi-region-dad-jokes)
* Explore any of several interesting topics available at [this jumping off point](https://github.com/cockroachlabs/workshop_labs)
* Make the [_Geo Tourist_ demo](https://github.com/cockroachlabs-field/crdb-geo-tourist) more interesting

