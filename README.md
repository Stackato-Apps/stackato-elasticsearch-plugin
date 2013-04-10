# ElasticSearch plugin for Stackato

This is an application that you can deploy to your local Stackato instance
to make REST API calls using ElasticSearch. Read more about ElasticSearch
at http://www.elasticsearch.org/.

## Deploying to Stackato

To deploy to Stackato, clone this repository and run:

    stackato target api.stackato-xxxx.local
    stackato login
    cd stackato-elasticsearch-plugin/
    stackato push -n

The stackato.yml file will handle the rest.
