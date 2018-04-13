# TREC OpenSearch Data set

This repository contains the TREC OpenSearch data set which contains raw queries, documents to be ranked and clicks that were measured during the run of the TREC OpenSearch competition.

The data set contains several json files:
    
    trecos.tar.gz
    ├── 2016
    │   ├── citeseerx
    │   │   ├── docs.json
    │   │   ├── queries.json
    │   │   ├── round1_test.json
    │   │   ├── round1_train.json
    │   │   ├── round2_test.json
    │   │   ├── round2_train.json
    │   │   ├── round3_test.json
    │   │   └── round3_train.json
    │   └── ssoar
    │       ├── docs.json
    │       ├── queries.json
    │       ├── round1_test.json
    │       ├── round1_train.json
    │       ├── round2_test.json
    │       ├── round2_train.json
    │       ├── round3_test.json
    │       └── round3_train.json
    └── 2017
        └── ssoar
            ├── docs.json
            ├── queries.json
            ├── round1_test.json
            ├── round1_train.json
            ├── round2_test.json
            └── round2_train.json

Each file contains line-separated json entries representing different things:

## Documents

The `docs.json` files contain on each line a json object representing a document, which look like:

    {
      "docid": "ssoar-d1",
      "content": {
        "available": "2012-12-18T12:45:29Z",
        "publisher": "DEU",
        "description": "Published Version",
        "language": "de",
        "author": "Z\u00e4hle, Tanja",
        "issued": "2005",
        "abstract": "\"Longitudinal observations reveal that households with ...",
        "identifier": "urn:nbn:de:0168-ssoar-324292",
        "type": "journal article",
        "subject": "quantitative empirical"
      }
    }
    
Where the docid is the document identifier and the content is a json object representing the content of the document. The internal structure of the contents is dependent on the metadata available and different for SSOAR and CiteSeerX.

## Queries

The `queries.json` files contain on each line a json object representing a query, which look like:

    {
      "qid": "ssoar-q1",
      "qstr": "krause",
      "doclist": [
        "ssoar-d1",
        "ssoar-d2",
        "ssoar-d3",
        ...
      ]
    }
    
Where the qid is the query identifier, qstr is the raw query string and doclist is a list of docids for the candidate documents to be ranked.

## Clicks

The click feedback is stored per round for the train and test sets. An example of the contents of `round1_train.json` for SSOAR is as follows:

    {
      "sid": "ssoar-s33127",
      "qid": "ssoar-q588",
      "time": "2017-08-02T00:23:53.348+0200",
      "ranking": [
        {"docid": "ssoar-d23667", "clicked": true, "team": "site"},
        {"docid": "ssoar-d23664", "clicked": false, "team": "participant"},
        {"docid": "ssoar-d7941", "clicked": false, "team": "site"},
        {"docid": "ssoar-d22395", "clicked": false, "team": "participant"},
        {"docid": "ssoar-d23669", "clicked": false, "team": "site"},
        ...
      ]
    }
    
Here, the `sid` is a unique session identifier for the request. The `qid` field represents the query that was issued for this session and `time` the time it was issued. The `ranking` field contains the interleaved ranked list that was shown to the user, where each entry states which document was shown (`docid`), whether it was clicked (`clicked`) and whether the click should be attributed to the site or participant (`team`).

