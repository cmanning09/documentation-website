---
layout: default
title: Compatibility
nav_order: 1
has_children: false
redirect_from:
  - /clients/
---

# OpenSearch client compatibility

OpenSearch provides clients for several popular programming languages, with more coming. In general, clients are compatible with clusters running the same major version of OpenSearch (`major.minor.patch`).

For example, a 1.0.0 client works with an OpenSearch 1.1.0 cluster, but might not support any non-breaking API changes in OpenSearch 1.1.0. A 1.2.0 client works with the same cluster, but might allow you to pass unsupported options in certain functions. We recommend using the same version for both, but if your tests pass after a cluster upgrade, you don't necessarily need to upgrade your clients immediately.

{% comment %}
* [OpenSearch Java client]({{site.url}}{{site.baseurl}}/clients/java/)
{% endcomment %}
* [OpenSearch Python client]({{site.url}}{{site.baseurl}}/clients/python/)
* [OpenSearch JavaScript (Node.js) client]({{site.url}}{{site.baseurl}}/clients/javascript/)
* [OpenSearch Go client]({{site.url}}{{site.baseurl}}/clients/go/)


## Legacy clients

Most clients that work with Elasticsearch OSS 7.10.2 *should* work with OpenSearch, but the latest versions of those clients might include license or version checks that artificially break compatibility. This page includes recommendations around which versions of those clients to use for best compatibility with OpenSearch.

Client | Recommended version
:--- | :---
[Java low-level REST client](https://search.maven.org/artifact/org.elasticsearch.client/elasticsearch-rest-client/7.13.4/jar) | 7.13.4
[Java high-level REST client](https://search.maven.org/artifact/org.elasticsearch.client/elasticsearch-rest-high-level-client/7.13.4/jar) | 7.13.4
[Python Elasticsearch client](https://pypi.org/project/elasticsearch/7.13.4/) | 7.13.4
[Elasticsearch Node.js client](https://www.npmjs.com/package/@elastic/elasticsearch/v/7.13.0) | 7.13.0
[Ruby Elasticsearch client](https://rubygems.org/gems/elasticsearch/versions/7.13.0) | 7.13.0

If you test a legacy client and verify that it works, please [submit a PR](https://github.com/opensearch-project/documentation-website/pulls) and add it to this table.


{% comment %}
## Python 3 test code

This code indexes a single document and is equivalent to `PUT /python-test-index1/_doc/1`.

```python
from elasticsearch import Elasticsearch

host = 'localhost'
port = 9200
# For testing only. Do not store credentials in code.
auth = ('admin', 'admin')

es = Elasticsearch(
  hosts = [{'host': host, 'port': port}],
  http_auth = auth,
  use_ssl = True,
  verify_certs = False
)

document = {
  "title": "Moneyball",
  "director": "Bennett Miller",
  "year": "2011"
}

response = es.index(index='python-test-index1', id='1', body=document, refresh=True)

print(response)
```


## Node.js test code

This code is equivalent to `GET /`.

```js
const { Client } = require('@elastic/elasticsearch')
const client = new Client({
  node: 'https://localhost:9200',
  auth: {
    // For testing only. Don't store credentials in code.
    username: 'admin',
    password: 'admin'
  },
  ssl: {
    // ca: fs.readFileSync('./cacert.pem'),
    rejectUnauthorized: false
  }
})

async function run () {
  const { body } = await client.info();
  console.log(body);
}

run().catch(console.log)
```
{% endcomment %}
