---
title: "My Splunkbase apps"
date: 2024-10-27
draft: false
ShowToc: true
---

Over the years I have created a number of Splunk-related applications. This post exists to summarise the applications I have created, along with why they might be useful within your environment.

## [Alerts For Splunk Admins](https://splunkbase.splunk.com/app/3796)
[GitHub link](https://github.com/gjanders/SplunkAdmins)

First published in 2017, this application was created after previous Splunk conf presentations would demonstrate an interesting platform-focussed dashboard, and then, they would not provide any source code or example searches to build the dashboard. I decided to create a presentation catered to Splunk administrators with all searches and dashboards available after the presentation.

The initial attempt to inline the searches within the presentation became too hard to read, I moved to github, and later Splunkbase.

Splunk has evolved since 2017, while some of the older alerts remain relevant, they may feel somewhat outdated. The application has evolved as my roles have changed over the years, resulting in newer alerts and dashboards designed to handle multiple search head, indexer, and forwarder layers.

Within the README you will find sections such as "Which alerts are best suited to automation?" to advise which are best used to send results to admins or customers, I use [sendresults](https://splunkbase.splunk.com/app/1794) for this.

The README section "Which alerts and reports have been tested on the newer Splunk versions such as 8.2 or 9.0?" includes all reports and alerts created in version 3.0 and above, along with updated alerts that are still in use in my current environment.

## [TA-Alerts for SplunkAdmins](https://splunkbase.splunk.com/app/6518)
[GitHub Link](https://github.com/gjanders/TA-SplunkAdmins)

Due to challenges with Splunk's packaging of the python SDK, I had a a few online messages where the alerts for Splunk Admins application was called out as "breaking" another Splunk application. Due to these issues, I separated the custom search functions used in 2 reports and the lookup modular input into a separate application.

## [VersionControl For Splunk](https://splunkbase.splunk.com/app/4355)
[GitHub link](https://github.com/gjanders/SplunkVersionControl)

In 2019, and as of the publication date in 2024, Splunk has no built-in version control. While this is likely a feature that will appear in the future, this application was created after the frustration of having 1 typo wipe out an entire configuration file.

In a search head cluster the conf.log may have entries related to config changes, additionally in modern Splunk enterprise versions there is the _configtracker index for limited config files. However, this is not as comprehensive as backing up all knowledge objects.

This application can backup all knowledge objects to git on a schedule, it allows non-admin users the ability to restore the objects without an admin.

The application itself is based on the [Transfer Splunk Knowledge Objects script](https://github.com/gjanders/Splunk/blob/master/bin/transfersplunkknowledgeobjects.py), this script was written to help with SHC to SHC migration via REST API. The Version Control application evolved from this script to backup to git instead of transferring to another SHC immediately. The README of the application additionally links to alternative backup options if you would like a more straightforward solution.

## [VersionControl For SplunkCloud](https://splunkbase.splunk.com/app/5061)
[GitHub link](https://github.com/gjanders/SplunkVersionControlCloud)

There were questions around "Can you backup SplunkCloud with the Version Control application?". After assistance of a fellow SplunkTrust member, I was provided a cloud stack and this application was created to simplify getting the backups of a Splunk cloud instance working with the Version Control application.

## [DECRYPT2](https://splunkbase.splunk.com/app/5565)
[GitHub link](https://github.com/gjanders/decrypt2)

DECRYPT2 is a fork of the now archived [DECRYPT](https://splunkbase.splunk.com/app/2655) application on Splunkbase. This application can decode Base32, Base64, XOR, ROTX, RC4, ROL/ROR, hex, ascii, substr, decode (python codec), escape, unescape, htmlescape, htmlunescape, tr, rev, find, substr, slice, zlib_inflate, Base32 reverse endian, Base64 reverse endian, Base58 routines.

I forked the initial version to ensure I had a base64 decoder easily available in Splunk and contributions on github have added additional features.

## [SearchHeadStatus](https://splunkbase.splunk.com/app/7315)
[GitHub link](https://github.com/gjanders/SearchHeadStatus)

This application was built to provide a status message on a Splunk instances REST endpoint, this allows a load balancer to determine if a search head cluster member is in a state to take traffic.
Splunk introduced the new REST endpoint `/shcluster/member/ready` in version 9.1 which offers a similar function, prior to this you required an authenticated call to determine the search head member status.

This application makes it easy for a load balancer to determine if a member is ready to accept traffic on both the REST and UI ports.

## [ReportDisabler](https://splunkbase.splunk.com/app/7314)
[GitHub link](https://github.com/gjanders/ReportDisabler)

The heuristics report packaged in Splunk 9.1.3 caused production issues in my environment, the report was configured on all Splunk enterprise instances. I built this application to utilize the REST API to disable any report on request.

## [AppDisabler](https://splunkbase.splunk.com/app/7319)
[GitHub link](https://github.com/gjanders/AppDisabler)

Since I found a problematic report was causing issues, I decided to utilise the REST endpoint to disable Splunk applications. This application allows the REST endpoint to be utilised to disable the application as requested.

## [Automatic Data Rebalance](https://splunkbase.splunk.com/app/7969)
[GitHub link](https://github.com/gjanders/auto_data_rebalance)

This technical addon exists to automate the data rebalance process on indexer clusters by creating a new modular input. This allows a scheduled rebalance to occur on the indexer cluster(s) as required.
