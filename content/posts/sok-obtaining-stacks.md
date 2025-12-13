---
title: "Splunk Operator for Kubernetes (SOK) — Obtaining stacks from an instance"
date: 2025-10-03
draft: false
ShowToc: true
---
The pstack and eu-stack utilities do not exist inside the Splunk container, and therefore if your using the Splunk operator for Kubernetes it can be difficult to gather stacks for support purposes. This article demonstrates how to build a container that includes eu-stack's for debugging purposes and a script you can use to obtain stacks when working with Splunk support. Stacks are useful for any situation where performance of the instance is an issue.

The full post is available on medium, [Splunk Operator for Kubernetes (SOK) — Obtaining stacks from an instance](https://medium.com/aws-in-plain-english/splunk-operator-for-kubernetes-sok-obtaining-stacks-from-an-instance-1d7a97ffa083). And on Splunk lantern as [Obtaining stacks from a Kubernetes instance](https://lantern.splunk.com/Manage_Performance_and_Health/Obtaining_stacks_from_a_Kubernetes_instance).
