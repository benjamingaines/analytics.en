---
title: Download link
description: The name of the download link.
---

# Download link

The 'Download link' dimension reports the names of download links implemented on your site. This dimension is valuable when you want to learn more about visitor behavior around download links, such as:

* Determine the files that are downloaded most frequently from your site.
* Understand if certain files are downloaded more often during specific time periods.
* Validate that visitors download different filetypes if offered.

## Populate this dimension with data

This dimension collects data from the [`pev2` query string](/help/implement/validate/query-parameters.md) in image requests for hits that also have the `pe` query string with the value of `lnk_d`. If the `pe` query string has a different value in the hit, this dimension does not collect data.

If you want to send data to this dimension using AppMeasurement:

* Populate the [`linkName`](/help/implement/vars/config-vars/linkname.md) variable with the desired value.
* Set the [`linkType`](/help/implement/vars/config-vars/linktype.md) variable to `"d"`.
* Send a [`tl()`](/help/implement/vars/functions/tl-method.md) image request.

## Dimension items

Since this variable is based on a custom string in your implementation, your organization determines what the dimension items are. Adobe recommends that you group links into meaningful categories based on your reporting needs.