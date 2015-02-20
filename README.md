# Flask-Cassandra

Flask-Cassandra provides an application-level connection to an Apache Cassandra database.  This connection can be used to interact with a Cassandra cluster.

Flask-Cassandra requires both Flask and the [Datastax Python Driver for Apache Cassandra](https://github.com/datastax/python-driver) to be installed.  This driver will be installed automatically when running `setup.py install`.

## Installation

Install the extension with one of the following commands:

```sh
$ python setup.py install
```

## Use

This is an example flask app that reads from a Cassandra cluster.

```python
from flask import Flask
from flask_cassandra import CassandraCluster

app = Flask(__name__)
cassandra = CassandraCluster()

app.config['CASSANDRA_NODES'] = ['cassandra-c1.terbiumlabs.com']  # can be a string or list of nodes

@app.route("/cassandra_test")
def cassandra_test():
    session = cassandra.connect()
    session.set_keyspace("monty_python")
    cql = "SELECT * FROM sketches LIMIT 1"
    r = session.execute(cql)
    return str(r[0])

if __name__ == '__main__':
    app.run()

```
