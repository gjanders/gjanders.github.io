---
title: "Splunk, systemd, and a clean shutdown"
date: 2026-01-17
draft: false
ShowToc: true
---
The pstack and eu-stack utilities do not exist inside the Splunk container, and therefore if your using the Splunk operator for Kubernetes it can be difficult to gather stacks for support purposes. This article demonstrates how to build a container that includes eu-stack's for debugging purposes and a script you can use to obtain stacks when working with Splunk support. Stacks are useful for any situation where performance of the instance is an issue.

The full post is available on medium, [Splunk, systemd, and a clean shutdown](https://medium.com/@gjanders03/splunk-systemd-and-a-clean-shutdown-dbdda318cab6). A Splunk lantern version is pending.
