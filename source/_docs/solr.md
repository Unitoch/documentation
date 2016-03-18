---
title: Apache Solr on Pantheon
description: Detailed information on using Apache Solr on the Pantheon Website Management Platform.
categories: [developing]
tags: [code]
keywords: apche, apache solr, index, indexing, searching, index and search, indexing and searching, solr, how to enable solr, enable solr, solr api, indexserver solr, solr indexserver, solr api, enable solr search, apachesolr, apache solor search module, solr modules, configure solr,
---
Apache Solr is a system for indexing and searching site content. Pantheon provides Apache Solr v3.6 as a service for most plans including the free sandbox. No permission or action is required from Pantheon to use Solr.  

## Which Plans Can Use Solr?

Currently, all plans except for a Personal plan can use Solr. Solr is available to Sandbox plans for developmental purposes, but Solr will not be available going live on a Personal plan.

| Plans        | Supported
| ------------- |:-------------:|
| Sandbox      | **Yes** |
| Personal      | No      |
| Professional | **Yes**      |
| Business | **Yes**      |
| Elite | **Yes**      |


## Using Solr with WordPress or Drupal

For installation instructions and additional details, see [Enabling Solr for WordPress](/docs/solr) or [Enabling Solr with Drupal](/docs/solr).

## Known Limitations of Pantheon's Solr Service

- Anything that takes more than 5 seconds to send to the Solr server to be indexed will timeout, which will block indexing. For example, large documents attached to Drupal nodes. In these cases, the developer must work with the content or code to exempt the nodes and/or files from being indexed.
- If you have a very large number of facets, the URLs generated by CURL may exceed length limits (may be fixed in search\_api).
-  Partial search, stopwords.txt, synonyms.txt, etc. are not supported.
- Non-English letters and characters will not be recognized because the Solr database is not UTF-8 encoded.  Therefore, multi-lingual search is not supported.

## Alternatives to Pantheon's Solr Service

While Pantheon provides a stable, reliable, and basic Solr service, your individual site needs may require something more robust and customizable. In those cases, a dedicated hosted Solr service may be a better solution for your needs. Given that Solr can tolerate higher latency (one query per request vs hundreds of database queries), Solr servers do not need to be in the same data center to provide fast and responsive results.

Some customers have reported success using external Solr service providers for their Solr indexing:  

 - [IndexDepot](https://www.indexdepot.com/en/). For more information, see [Using IndexDepot With Pantheon Sites](/docs/indexdepot/).
 - [OpenSolr](https://opensolr.com/)
 - [WebSolr](https://websolr.com/)

## Apache Solr Vocabulary

<dl>
	<dt>bias</dt>
	<dd>Allows certain parts of indexed items to influence the importance of search results. The higher the bias, the greater the influence; the range is 0.1 to 21.0.</dd>
	<dt>core</dt>
	<dd>A core is a separate configuration and index using a single Solr instance. A core is created when the schema is posted. For more information, see <a href="http://wiki.apache.org/solr/CoreAdmin">http://wiki.apache.org/solr/CoreAdmin</a>.
</dd>
	<dt>document</dt>
	<dd>A document is similar to a database row, containing the contents of what is to be searched and whatever fields are associated with it, like title.</dd>
	<dt>facet</dt>
	<dd>Search facets allow search results to be filtered; examples include seeing a list of potential filters and the count of matches for each filter on the left, like Amazon product searches.</dd>
	<dt>index</dt>
	<dd>structure containing extracted keywords from a document for rapid search and retrieval, similar to a database table.</dd>
	<dt>score</dt>
	<dd>calculated relevance of matches influenced by bias, represented as a float.</dd>
	<dt>schema.xml</dt>
	<dd>Contains details about the fields that documents can contain, and how those fields are handled when adding documents to the index or querying those fields. Must be posted using the pantheon_apachesolr module before indexing and searching will work. For more information, see <a href="http://wiki.apache.org/solr/SchemaXml">http://wiki.apache.org/solr/SchemaXml</a>.
</dd>
</dl>
#### Check Index and Batch Sizes

Are you only indexing only 50 items at a time and wondering why hundreds of new content nodes generated in the last hour aren't being indexed? Numbers are important here. If you need to increase the number of items being indexed with each Solr indexing run, feel free to do so. However, don't get ridiculous here: setting 1000 items to be indexed per run could cause a page timeout. If a specific request times out, that could be because it's trying to POST too much data at once; try reducing the quantity of items being indexed per batch and see if that allows the items to be indexed.

### Apache Spatial Search on Pantheon

Pantheon's Solr configuration does not support geospatial indexing and searching and there are currently no plans to add it.  
As an alternative, there are several external Solr service providers that do support spatial searching. Pantheon doesn’t do any blocking/filtering, so you’re welcome to use an externally hosted solr index – and in a case where you’re looking for a more complex configuration, that might be optimal.