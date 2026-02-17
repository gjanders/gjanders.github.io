---
title: "GitHub repositories"
date: 2024-11-17
draft: false
ShowToc: true
---

In addition to the [Splunkbase apps](/posts/splunkbase-apps/), I have written various automation components related to Splunk.
Each repository has a unique purpose as described in the following sections.

## [Splunk](https://github.com/gjanders/Splunk)
This repository contains various scripts that I have built over the years, the most popular would be the `transfersplunkknowledgeobjects.py` script.

This first script is documented in the README.md of the repository and exists to assist in search head to search head (or search head cluster to search head cluster) migrations using the REST API. Note that POST'ing too many searches to the savedsearches REST API can be very disruptive to the Splunk scheduler and this works best for small migrations.

The script itself was written prior to the concept of deployer ["push modes"](https://docs.splunk.com/Documentation/Splunk/latest/DistSearch/PropagateSHCconfigurationchanges#Choose_a_deployer_push_mode). In more recent migrations I've used the deployer push modes to migrate to a new search head cluster. This script is also the pre-cursor to the [Version Control Splunkbase app](https://splunkbase.splunk.com/app/4355).

Additionally, I have added a lookup transfer mechanism, `download_lookups_from_splunk.py` and `upload_lookups_to_splunk.py` exist to transfer lookups from one SHC to another using the Splunk App for Lookup File Editing (previously known as the lookup editor).

## [SplunkK8s](https://github.com/gjanders/SplunkK8s)

This repository hosts K8s related scripts, the files purposes are quite simple:

### trigger_roll_and_resync.sh 
`trigger_roll_and_resync.sh` and the related files, `roll_and_resync_buckets_v2.sh/py` relate to rolling buckets not meeting the replication factor within a K8s indexer cluster(s).

This script exists because we are using local storage, if the bucket is not meeting replication factor there is a risk of data loss if the data is not uploaded to S3. This automation handles the rolling across multiple indexer clusters located with K8s.

### k8s_healthcheck.sh
`k8s_healthcheck.sh` exists for a specific purpose...originally we had local (non-replicated) storage under the cluster manager. If the node failed, we could delete the PVC to force the CM to re-locate the cluster manager to a healthy K8s node in a node loss scenario.

However, the issue was that the appframework did not re-deploy the cluster manager apps to the members, therefore the bundle push was an empty bundle when the CM restarted.

The workaround used was to delete & re-create the cluster manager CR (custom resource), this forces the appframework to re-deploy all previous applicationsi.

This setup was later replaced by Pireaus Datastore, the [post here](/posts/kubernetes-storage) describes the details of this replicated storage option.


### k8s_offline.service
`k8s_offline.service` is a systemd unit file that can be combined with `k8s_node_offlinev2.sh` and `offline_remove_pod.sh` or the simpler `k8s_node_offline.sh`

While K8s 1.24 was documented to handle graceful shutdown, I found that when the Splunk pods in the tested version received the shutdown signal, as tested on Splunk version 9.0.3 and 9.1.3, the pods did not always shutdown Splunk. In many cases the Splunk instance abruptly terminated resulting in bucket corruption on startup.

To resolve this, the custom Systemd unit file ensures a Splunk offline command is run prior to the node going offline, the online service simply removes the cordon from the node.

This may not be required if you can see your Splunk instances shutting down cleanly with OS shutdown.

## [SplunkOther](https://github.com/gjanders/SplunkOther)

This is the only Splunk application I have created that is not published on Splunkbase. This app includes a dashboard to help users change the TTL, or time to live of any savedsearch. Additionally the appadmins dashboard allows team members without write access to a Splunk application to clone/change ownership of various knowledge objects within the application.

This particular use-case was related to the concept of having those who have read-only access within an application but may need to share a dashboard or report under some circumstances with the approval of an "app admin".

## [etc_backup](https://github.com/gjanders/etc_backup)

A simple Splunk application to backup the directories under /opt/splunk/etc that would be required to restore an SHC member, excluding various files that come from the deployer.

## [kvstore_backup](https://github.com/gjanders/kvstore_backup)

A simple Splunk application to backup the kvstore using a modular input.

## [kvstore_checker](https://github.com/gjanders/kvstore_checker)

A simple Splunk application to record the status of the kvstore via a scripted input. Useful for detecting when the kvstore has stopped working without watching for the mongod.log to stop updating.

