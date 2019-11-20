---
description: Page variables directly populate a report, such as pageName, List Props, List Variables, and so on.
keywords: Analytics Implementation
solution: Analytics
subtopic: Variables
title: Page variables
topic:
uuid:
---

# eVarN

The [!UICONTROL eVar] variables are used for building custom reports.

<!-- 

eVarN.xml

 -->

When an eVar is set to a value for a visitor, the value is remembered until it expires. Any success events that a visitor encounters while the eVar value is active are counted toward the eVar value.

|  Max Size  | Debugger Parameter  | Reports Populated  | Default Value  |
|---|---|---|---|
|  255 Bytes  | V1-v75 ( [or v100 or v250](/help/implement/js-implementation/page-variables/page-variables.md))  | Custom Conversion  | ""  |

**Expiration**

`eVars` expire after a time period you specify. After the eVar expires, it no longer receives credit for success events. eVars can also be configured to expire on success events. For example, if you have an internal promotion that expires at the end of a visit, the internal promotion receives credit only for purchases or registrations that occur during the visit in which they were activated.

There are two ways to expire an eVar:

* You can set the eVar to expire after a specified time period or event.
* You can use force the expiration of an eVar, which is useful when repurposing a variable.

If an eVar is used in May to reflect internal promotions and expires after 21 days, and in June it is used to capture internal search keywords, then on June 1, you should force the expiration of, or reset, the variable. Doing so will help keep internal promotion values out of June's reports.

**Case Sensitivity**

eVars are case insensitive, but they are displayed in the capitalization of the first occurrence. For example, if the first instance of eVar1 is set to "Logged In," but all subsequent instances are passed as "logged in," reports always show "Logged In" as the value of the eVar.

**Counters**

While eVars are most often used to hold string values, they may also be configured to act as counters. eVars are useful as counters when you are trying to count the number of actions a user takes before an event. For example, you may use an eVar to capture the number of internal searches before purchase. Each time a visitor searches, the eVar should contain a value of '+1.' If a visitor searches four times before a purchase, you will see an instance for each total count: 1.00, 2.00, 3.00, and 4.00. However, only the 4.00 receives credit for the purchase event (Orders and Revenue Metrics). Only positive numbers are allowed as values of an eVar counter.

**Subrelations**

A common requirement for a Custom eVar report is the ability to break down one Custom eVar report by another. For example, if one eVar contains gender, and another contains salary, you may ask the following question: of the female visitors to my site, how much revenue was generated by women who make more than $50,000 per year. Any eVar that is fully sub-related allows this type of break down in reports. For example, if the gender eVar has full subrelations enabled, all other custom eVar reports can be broken down by gender, and gender can be broken down by all others. To see the relationship between two reports, only one of them needs full subrelations enabled. By default, Campaign, Products, and Category reports are fully sub-related (any eVar can be broken down by campaign or products).

**Syntax and Possible Values**

While eVars may be renamed, they should always be referred to in the JavaScript file by eVarX, where X is a number between 1 and 75 ( [or 100, or 250](/help/implement/js-implementation/page-variables/page-variables.md)).

```js
s.eVarX="value"
```

When not used as a counter, eVars have the same limitations as all other variables. If the eVar is a "counter," it is expected to receive numeric values like "1" or "2.5." If more than two decimal places are given, the eVar counter rounds to two decimal places. An eVar counter may not contain negative numbers.

**Examples**

```js
s.eVar1="logged in"
```

```js
s.eVar23="internal spring promo 4"
```

**Configuration Settings**

eVars can be configured in Analytics > Admin > Report Suites > Edit Settings > Conversion > Conversion Variables]. All eVars can be configured with a Name, Type, Allocation, Expire After Setting, or Reset. Each configuration setting is addressed separately.

<table id="table_5C524B71520849FA8A9A6B79A3EE77C9"> 
 <thead> 
  <tr> 
   <th class="entry"> Setting </th> 
   <th class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Name </td> 
   <td> Allows you to change the name of the eVar report within <span class="keyword"> Analytics </span>. <p>The eVar should still be referenced as s.eVarX in the JavaScript code, no matter what name is given to the report in <span class="keyword"> Analytics </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> Type </td> 
   <td> Allows you to show whether the eVar is a Text String or Counter. </td> 
  </tr> 
  <tr> 
   <td> Allocation </td> 
   <td> Used to configure which value of the eVar receives credit for success events. <p>If Allocation is set to "Most Recent (Last)," then B receives credit. </p> <p>If Allocation is set to "Original Value (First)" then A receives credit. </p> <p>If Allocation is set to "Linear", then both A and B receive credit for half the purchase value. </p> </td> 
  </tr> 
  <tr> 
   <td> Expire After </td> 
   <td> Lets you determine whether an eVar expires on a specific event, like purchase, or after a custom or predefined time period. </td> 
  </tr> 
  <tr> 
   <td> Reset </td> 
   <td> By selecting the <span class="wintitle"> Reset </span> check box for an eVar, and clicking <span class="wintitle"> Save </span> at the bottom of the page, all values of that eVar are immediately expired. After this happens, only new values of the eVar receive credit for success events. </td> 
  </tr> 
 </tbody> 
</table>

**Pitfalls, Questions, and Tips**

* Unlike [!UICONTROL prop] variables, eVar variables are not allowed to be lists of delimited values. If you populate an eVar with a list of values, for example "one,two,three," then that exact string appears in reports.
* eVar counters may not contain negative numbers.