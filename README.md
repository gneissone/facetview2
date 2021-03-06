# FacetView2 - Connect UNAVCO

a pure javascript frontend for ElasticSearch search indices.

It has been developed as a jQuery plugin and lets you easily embed a faceted browse front end into any web page.

FacetView2 is a major re-write of the original FacetView application.  See https://github.com/okfn/facetview for the previous version.

## Customizations

This fork has been developed for implementation as part of [Connect UNAVCO](http://connect.unavco.org). Some customizations may be of interest:

* Replacement of popup dialogs with links or dropdown menus
* Ability to specify multiple fields to search ('fields' instead of 'default_field' in Elasticsearch)
* Sort by 'relevance' is no longer written directly into the bootstrap template  and can be sorted by a secondary field (e.g. search_sortby: [{"display":"Relevance","field":["_score","name.sort"]}])
* Specify a min_score for results - especially useful when searching ngram or other tokenized fields
* CSV export feature (requires [a plugin](https://github.com/jprante/elasticsearch-csv) which in turn requires Java 8)

## Using FacetView2

Add the following code to your web page:

    <script type="text/javascript" src="vendor/jquery/1.7.1/jquery-1.7.1.min.js"></script>
    <link rel="stylesheet" href="vendor/bootstrap/css/bootstrap.min.css">
    <script type="text/javascript" src="vendor/bootstrap/js/bootstrap.min.js"></script>  
    <link rel="stylesheet" href="vendor/jquery-ui-1.8.18.custom/jquery-ui-1.8.18.custom.css">
    <script type="text/javascript" src="vendor/jquery-ui-1.8.18.custom/jquery-ui-1.8.18.custom.min.js"></script>
    
    <script type="text/javascript" src="es.js"></script>
    <script type="text/javascript" src="bootstrap2.facetview.theme.js"></script>
    <script type="text/javascript" src="jquery.facetview2.js"></script>
    <link rel="stylesheet" href="css/facetview.css">

Then add a script somewhere to your page that actually calls and sets up the facetview on a particular page element:

    <script type="text/javascript">
    jQuery(document).ready(function($) {
      $('.facet-view-simple').facetview({
        search_url: 'http://localhost:9200/myindex/type/_search',
        facets: [
            {'field': 'publisher.exact', 'size': 100, 'order':'term', 'display': 'Publisher'},
            {'field': 'author.name.exact', 'display': 'author'},
            {'field': 'year.exact', 'display': 'year'}
        ],
      });
    });
    </script>


## Customisation

FacetView2 has been written to allow extensive customisation within a flexible but constrained page framework.

There will be more documentation here on how to do that, but in the mean time, take a look at the source of jquery.facetview.js for the config options and templates that can be replaced for custom display.


Copyright and License
=====================

Copyright 2017 Benjamin Gross.
Original FacetView2 frontend Copyright 2014 Cottage Labs

Licensed under the MIT Licence

twitter bootstrap: http://twitter.github.com/bootstrap/
MIT License: http://www.opensource.org/licenses/mit-license.php

