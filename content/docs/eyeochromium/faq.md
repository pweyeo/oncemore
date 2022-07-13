---
title: "ADRs & FAQs"
description: "Read the eyeo Chromium ADR."
lead: "Learn about the thinking behind eyeo Chromium."
draft: false
images: []
menu:
  docs:
    parent: "eyeochromium"
weight: 103
toc: true
---

## Overview

This page contains eyeo Chromium's architectural decision records **(ADRs)**, which summarize the most important software design choices made during the development of the eyeo Chromium SDK.

These decisions address functional and non-functional requirements that eyeo finds architecturally significant.

## Transitioning from minified to full filter lists

The main reason for using minified filter lists in previous implementations of our ad-filtering core was to reduce memory consumption for mobile users. On the other hand, more recent implementations achieved this reduction by adopting [FlatButters as a filter list](#storing-filter-lists-in-flatbuffer-format) file format and by moving from V8 to a native implementation.

We can now use full filter lists, which allow for more filter rules. This improves user experience and blocks a greater number of intrusive ads. As a result, more acceptable ads are allowed, which increases for publishers who participate in the [Acceptable Ads scheme](https://acceptableads.com/).

## Moving user counting to a dedicated service

Coupling the user counting service with filter lists gives us insight into SDK usage across Chromium, OS, and platform versions. As a dedicated service, it also allows us to monitor Acceptable Ads opt-out rate while preventing partners from serving and monetizing filter lists from their own servers.

## Implementing ad-filtering from scratch

Chromium contains some ad-blocking functionality in the form of the [subresource filter](https://chromium.googlesource.com/chromium/src.git/+/main/components/subresource_filter/README.md). The Chromium subresource filter, however, doesn't support CSS element-hiding, JavaScript element hiding emaulation, or snippets.

Patching these limitations requires significant tradeoffs, some of which include the following:

- More conflicts to solve after Chromium updates
- Less flexibility to introduce new features and optimizations
- Irreconcilably different objectives between eyeo and Chrome's authors

Chromium authors ultimately control subresource filter development. As a result, they may have different (ad-related) business objectives that could take subresource filtering in a direction that doesn't fit with eyeo's vision.

<!-- https://gitlab.com/eyeo/adblockplus/abpchromium/-/blob/eyeo-103-dev/components/adblock/docs/adr/not-extending-subresource-filter.md -->

For these reasons, the eyeo team chose not to build on top of the subresource filter, opting for an implementation with ad-filtering capabilities built from scratch.

## Storing filter lists in FlatBuffer format

Filter lists aren't consumed in plain text format right after download. Instead, they are converted from plain text into the FlatBuffers format, which offers the following advantages:

- Reduced memory consumption, down to approximately 15 MB
- Reduced startup time, from seconds down to milliseconds
- No negative impact on page load time, except for sites with long URLs
- Facilities for multi-threading and synchronous popup blocking
- No required deserialization, because FlatBuffers is already in a binary format
- FlatBuffers can be memory-mapped and accessed as memory directly from disk
- Accessing data in a flatbuffer is as fast as deferencing pointers to memory

A FlatBuffers file contains only one filter list, for the following reasons:

- Filter lists updated at different times can be downloaded independently.
- Less time consumed in conversion than if all selected filter lists are combined in one file
- For long-term distribution of FlatBuffers files, having to provide a file containing all selected filter lists would cause an explosion of combinations

## Questions?

Do you have questions about other architectural decisions made during the development of eyeo Chromium? Contact eyeo's team for answers. [Support →]({{< relref "#" >}})
