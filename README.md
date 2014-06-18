# ElasticSearch plugin for Stackato

This is an application that you can deploy to your local Stackato instance
to make REST API calls using ElasticSearch. Read more about ElasticSearch
at http://www.elasticsearch.org/.

This plugin was made as a standalone application, following the
[example on cloudfoundry-examples](https://github.com/cloudfoundry-samples/rails-elastic-search/blob/master/README.md),
with a few more tweaks. In this application, we have provisioned a
[FileSystem service](http://docs.stackato.com/deploy/services/filesystem.html)
that will allow the indices created by REST API calls to ElasticSearch to
be preserved, given that the FileSystem service is not deleted when you
uninstall the application from Stackato. This allows the user to safely
stop, restart, and uninstall the application, and the indices will
be preserved, ready for when another application binds to this
service.

## Deploying to Stackato

To deploy to Stackato, clone this repository to your local machine,
ensure you have installed the [Stackato CLI](http://www.activestate.com/stackato/download_client) and run:

    stackato target api.stackato-xxxx.local
    stackato login
    cd stackato-elasticsearch-plugin/
    stackato push -n

After the app is deployed, run:

    stackato map elasticsearch elasticsearch.stackato-xxxx.local

## Testing ElasticSearch

Let’s make sure we can index some
data. We will go with the most simple example.

    curl -XPUT 'http://elasticsearch.stackato-xxxx.local/twitter/tweet/1' -d '{
      "user": "bacongobbler",
      "post_date" : "2013-04-10",
      "message" : "Hello, World!"
    }'

Try running this curl request from your local
computer. You can use a [Rest client](http://code.google.com/p/rest-client/) if
you don’t have curl, and there is a cool
[Chrome extension](https://chrome.google.com/webstore/detail/cokgbflfommojglbmbpenpphppikmonn?hc=search&amp;hcp=main)
to do this as well. If all went well, you should see a successful response:

    {"ok":true,"_index":"twitter","_type":"tweet","_id":"1","_version":1}



