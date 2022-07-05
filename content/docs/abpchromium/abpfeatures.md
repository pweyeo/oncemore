---
title: "SDK Features"
description: "Use ABP Chromium to filter ads."
lead: "Learn how the SDK helps you filter content."
draft: false
images: []
menu:
  docs:
    parent: "abpchromium"
weight: 102
toc: true
---

## ABP Chromium Features

This page contains information you'll find useful as you configure the ABP Chromium SDK for your own project. If you've not yet installed the SDK, start with the [ABP Chromium quickstart guide](/docs/abpchromium/quickstart).

{{< alert icon="👉" text="Some knowledge of Java and C++ will benefit you as you implement the practices on this page." />}}

## Supported ad-filtering techniques

ABP Chromium supports the following ad-filtering techniques:

- [Request filtering](#), which blocks network resources from downloading
- [Element hiding](#), which hides content that request-blocking couldn't hide
- [Snippets](#); custom code snippets that deal with complex cases, like video ads

Because ad content can be served at various stages while a web page loads, ABP consults Adblock Plus filter rules to determine which requests to block and which to hide.

## How ABP Chromium uses filter lists

To determine which requests to block and which elements to hide, ABP Chromium refers to filter lists, collections of rules that instruct a browser to block certain elements on a web page.

Filter lists are hosted online in plain text. ABP Chromium downloads these lists, converts them into the [FlatBuffer format](https://google.github.io/flatbuffers/), and stores them. ABP Chromium implements all ad-filtering techniques, then, and deploys the right technique depending on the nature of the ad content it detects.

### Default filter lists

A basic ABP Chromium installation contains the following filter lists:

- [**EasyList**](https://easylist.to/); the standard for filtering ad content online. ABP Chromium also includes language-specific rules that depend on the user's system region
- **Acceptable Ads**; an allowlist of ad content that the [Acceptable Ads Committee](https://acceptableads.com/) has compiled
- **ABP Anti-Circumvention**; custom filter lists, including the ABP anti-circumvention filter list

{{< alert icon="👉" text="The Acceptable Ads and ABP Filters lists are both maintained by eyeo." />}}

## Recipes for common ad-filtering integration tasks

Depending on your implementation of ABP Chromium, you'll likely find some of the following strategies useful for configuring the SDK within your project.

{{< alert icon="👉" text="The following strategies are only supported for Android." />}}


### Disable ad-filtering on a specific domain

In some cases, you may want to disable ad-filtering on certain domains. To do so, call the [AdblockController](https://gitlab.com/eyeo/adblockplus/abpchromium/-/blob/eyeo-103-dev/chrome/android/java/src/org/chromium/chrome/browser/adblock/AdblockController.java)'s `addAllowedDomain()` method.

The following example, in Java, instructs ABP Chromium to stop filtering ads on the specified domain:

```java
import org.chromium.components.adblock.AdblockController;

String domain = "example.com";
AdblockController.getInstance().addAllowedDomain(domain);
```

To resume ad-filtering on the same domain, use the `removeAllowedDomain()` method:

```java
import org.chromium.components.adblock.AdblockController;

String domain = "example.com";
AdblockController.getInstance().removeAllowedDomain(domain);
```

You must pass the targeted domain as an argument, like `example.com`, not as a URL.

### Add or remove subscriptions to a filter list

You may have custom filter lists that you want to add to your ABP Chromium instance. To add such lists, call [AdblockController](https://gitlab.com/eyeo/adblockplus/abpchromium/-/blob/eyeo-103-dev/chrome/android/java/src/org/chromium/chrome/browser/adblock/AdblockController.java)'s `addCustomSubscription()` method.

The following example, in Java, instructs ABP Chromium to download, parse, and install a filter list:

```java
import org.chromium.components.adblock.AdblockController;

URL myFilterList = new URL("http://example.com/my_list.txt");
AdblockController.getInstance().addCustomSubscription(myFilterList);
```

To remove a custom filter list you've added, call the `removeCustomSubscription` method:

```java
import org.chromium.components.adblock.AdblockController;

URL myFilterList = new URL("http://example.com/my_list.txt");
AdblockController.getInstance().removeCustomSubscription(myFilterList);
```

### Change default filter lists

By default, ABP Chromium includes EasyList, Acceptable Ads, and the ABP Anti-Circumvention filter list.

If you want to change the default filter lists in your ABP Chromium project, modify `config::GetKnownSubscriptions` in `components/adblock/core/subscription_config.cc`.

The following shows a sample configuration for designating a new filter list as default:

```cpp
static std::vector<SubscriptionInfo> recommendations = {
    ...
     {"https://domain.com/subscription.txt",        // URL
      "My custom filters",                          // Display name for settings
      {},                                           // Supported languages list, considered for
                                                    // SubscriptionFirstRunBehavior::SubscribeIfLocaleMatch
      SubscriptionUiVisibility::Visible,            // Should the app show a subscription in the settings
      SubscriptionFirstRunBehavior::Subscribe       // Should the app subscribe on first run
      SubscriptionPrivilegedFilterStatus::Forbidden // Allow snippets and header filters or not
     },
```

### Set build arguments for user counting

With ABP Chromium, you can count the number of users your product has. The ABP Chromium SDK requires the following `gn` arguments to count active users:

* `abp_telemetry_client_id`
* `abp_telemetry_activeping_auth_token`

eyeo provides the argument values. To set the arguments, generate project build files like the following:

```sh
gn gen --args='abp_telemetry_client_id="mycompany" abp_telemetry_activeping_auth_token="peyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9" ...' ...
```

If you don't set these arguments, eyeo may be not correctly attribute users to your product.

{{< alert icon="👉" text="Keep your auth token secure. Never embed it in open-source repositories or documents. If your auth token is revealed, reach out to eyeo as soon as possible to receive a new token." />}}

User counting doesn't transfer any PII or other identifiable data to eyeo, nor does it allow tracking or profiling of users by eyeo.

## Next up

Now that you've learned standard how to accomplish standard tasks with your ABP Chromium integration, view our [ABP Chromium settings documentation] to learn more about the ABP Chromium APIs, and interfaces you can use to control the SDK.

## Help

Need support?  Contact eyeo's team for questions or advice on implementing the ABP Chromium SDK into your project. [Support →]({{< relref "#" >}})
