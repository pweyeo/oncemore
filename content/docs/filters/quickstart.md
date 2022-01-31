---
title: "Filters Quickstart"
description: "Learn how to write AdBlock Plus filters."
lead: "Get up and running with your first custom filter rule."
draft: false
images: []
menu:
  docs:
    parent: "filters"
weight: 100
toc: true
---

## Writing Filters

This tutorial explains how to write custom filter rules, or just **filters**, that [Adblock Plus](https://adblockplus.org/) can use to filter and block ads.

No prior programming experience is required, though some knowledge of HTML and the [document object model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) (DOM) will be useful.

By the end of this tutorial, you'll know how to write and add blocking filters to Adblock Plus. First, though, you'll learn some basic filter concepts.

## Filter Basics

A filter is a rule that a browser uses to block elements on a web page. A collection of filters is a **filter list**.

Adblock Plus (**ABP**) uses filter lists to block and filter web content. ABP uses three pre-installed filter lists:

- [Acceptable Ads](https://acceptableads.com/)
- [EasyList](https://easylist.to/)
- [ABP Anti-Circumvention](https://github.com/abp-filters/abp-filters-anti-cv)

You can create your own filter rules, though, and add them to your instance of Adblock Plus.

## Your first filter

Writing a new blocking filter for Adblock Plus requires three steps:

1. **Identify the web request address you want to block.**
2. **If necessary, use characters to turn the request address into a filter.**
3. **Add the new address, or filter, to Adblock Plus.**

Below, you'll use a practical example to learn each of these steps.

### Identifying the request address

Most internet ads are web resources found at a URL. Suppose you come across ad content at the following URL:

```html
http://example.com/ads/banner123.gif
```

This URL contains two key components:

- A domain name, in this case `example.com`
- A path, in this case, `/ads/banner123.gif`

The path itself contains two components:

- A directory, or folder, in this case `/ads`
- A file inside that folder, in this case, `banner123.gif`

Next, you'll learn how to convert this URL into a filter.

### Turning the request into a filter rule

If you only wanted to block the file `banner123.gif`, you could instruct the browser to block the entire, unchanged URL. However, the file's parent folder, `/ads`, probably contains other ads that you could block as well. By making small changes to the URL, you can create a comprehensive filter rule that blocks `banner123.gif` and content similar to it, as well.

#### Changing requests with special characters

For example, if you see a file named `banner123.gif`, you might conclude that the folder contains other files with similar names, like `banner456.gif` or `banner789.gif`. Instead of writing filter rules for each potential file, you could use the wildcard character `*` and replace the numbers following `banner`, like in the following example:

```html
http://example.com/ads/banner*.gif
```

This `*` character serves as a placeholder for any other characters that may follow, including numbers. This filter rule, then, would block all `.gif` files in the `/ads` folder that begin with the string `banner`.

#### Altering paths to target directories




### Adding your filter rule to Adblock Plus

{{< alert icon="👉" text="For this step, make sure you have Adblock Plus installed on your device." />}}

Use the following instructions to complete the final step, adding your filter to Adblock Plus:

1. Copy the filter rule you created in the previous step.
2. In your browser, open Adblock Plus, then select the **Advanced** tab.
3. Scroll down to the **My Filter List** section.
4. Paste the filter rule from Step 1 into the **Search or add filter(s)** field.
5. Click the **+Add** button to confirm.

You've just added a custom filter rule to Adblock Plus.

## What next?

In this guide, you learned how to write a custom blocking filter.    [API Docs →](#)


## Help

Need help?  Reach out to our team for support. [Support →]({{< relref "#" >}})
