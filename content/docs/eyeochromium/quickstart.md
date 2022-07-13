---
title: "Quickstart Guide"
description: "Get up and running with the eyeo Chromium SDK."
lead: "Get up and running with the eyeo Chromium SDK."
draft: false
images: []
menu:
  docs:
    parent: "eyeochromium"
weight: 101
toc: true
---

## About the eyeo Chromium SDK

eyeo Chromium is a software development kit (**SDK**) that you can use to integrate eyeo's ad-filtering technology into Chromium-based browsers.

Built from a fork of the [Chromium project](https://adblockplus.org/), eyeo Chromium leverages eyeo's ad-blocking functionality and filter lists to serve as the basis for developing your own browser.

You can get started with the eyeo Chromium SDK in just two stages:

1. Verify your Chromium dependencies.
2. Fork eyeo Chromium from eyeo's GitLab repository.

By the end of this quickstart guide, you'll have cloned the eyeo Chromium project and laid the ground work for the development of your own Chromium-based ad-filtering browser.

{{< alert icon="👉" text="This guide assumes familiarity with both Git and the command line." />}}

## Verify Chromium dependencies

Because eyeo Chromium is built from a Chromium fork, integrating eyeo Chromium into your browser requires several Chromium dependencies.

You'll find the necessary dependencies within the `components` directory in the [eyeo Chromium SDK repository](https://gitlab.com/eyeo/adblockplus/abpchromium). A successful integration requires the following dependencies:

- [KeyedService](https://gitlab.com/eyeo/adblockplus/abpchromium/-/blob/eyeo-104-dev/components/keyed_service/core/keyed_service.h)
- [Network Service](https://gitlab.com/eyeo/adblockplus/abpchromium/-/tree/eyeo-104-dev/services/network)
- [PrefService](https://gitlab.com/eyeo/adblockplus/abpchromium/-/blob/eyeo-104-dev/components/prefs/pref_service.h)
- [Profile](https://gitlab.com/eyeo/adblockplus/abpchromium/-/blob/eyeo-104-dev/chrome/browser/profiles/profile.h)
- [Resources](https://gitlab.com/eyeo/adblockplus/abpchromium/-/tree/eyeo-104-dev/components/resources)
- [Version Information](https://gitlab.com/eyeo/adblockplus/abpchromium/-/tree/eyeo-104-dev/components/version_info)

If you're unable to incorporate these (or any other) Chromium dependencies into your browser, the SDK might not perform as expected.

For questions about your implementation or advice on strategies that best fit your use case, reach out to your eyeo distribution partner.

## Clone the eyeo Chromium fork

You'll build your eyeo Chromium project on top of eyeo's current fork. Follow these steps to clone the eyeo Chromium GitLab repository:

1. **Copy the following URL:**

```html
https://gitlab.com/eyeo/adblockplus/abpchromium
```

2. **Clone the repository using the URL you just copied, then move in to the new eyeo Chromium directory:**

```bash
git clone https://gitlab.com/eyeo/adblockplus/abpchromium
cd abpchromium
```

3. **Set ABP as the upstream repository, and set your repository as its origin:**

```bash
git remote rename origin upstream
git remote add origin your-repository-path
```

4. **Create your development branch from the latest ABP Chromium release tag**:

```
git checkout -b my-branch eyeo-abp-release-101.0.4951.41-2.0
```

You can now develop and commit your project's changes to the branch you just created.

## Next up

In this quickstart guide, you cloned the eyeo Chromium fork to your own development project.

While you could begin working on your own browser immediately, using the SDK to accomplish basic ad-filtering tasks will take your project to the next level. Check out the [eyeo Chromium features documentation]() to learn how eyeo Chromium handles common ad-filtering use cases.

## Help

Need support?  Contact eyeo's team for questions or advice on implementing the eyeo Chromium SDK into your project. [Support →]({{< relref "#" >}})
