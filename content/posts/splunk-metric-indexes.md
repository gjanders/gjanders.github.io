---
title: "Splunk indexers — metrics data — HEC fields vs INDEXED_EXTRACTIONS changes the bucket"
date: 2025-02-22
draft: false
ShowToc: true
---
A discussion around Splunk metrics indexes and how using different ingestion methods changes the bucket. In our production environment, we encountered challenges with high cardinality metrics indexes, specifically those receiving metric data with a large number of unique dimension values.

The full post is available on medium, [Splunk indexers — metrics data — HEC fields vs INDEXED_EXTRACTIONS changes the bucket](https://medium.com/@gjanders03/splunk-indexers-metrics-data-hec-fields-vs-indexed-extractions-changes-the-bucket-ed4fba8b2674), and a lantern version with title [Preventing premature bucket rolling in metrics indexes](https://lantern.splunk.com/Splunk_Platform/Product_Tips/Data_Management/Preventing_premature_bucket_rolling_in_metrics_indexes).
