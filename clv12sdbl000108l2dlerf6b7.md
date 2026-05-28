---
title: "Track Calendly Meeting on Google Ads"
seoTitle: "How to Track Calendly Meetings in Google Ads Easily"
seoDescription: "Learn the easiest way to track Calendly meetings in Google Ads using GA4. Step-by-step guide to set up conversion tracking and measure your bookings"
datePublished: 2024-04-15T14:54:07.474Z
cuid: clv12sdbl000108l2dlerf6b7
slug: track-calendly-meeting-on-google-ads
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1756367398184/ce4671eb-c443-4e6b-b074-b5afad11ef5d.png
tags: google-ads, calendly

---

I know why you're here. Most likely, you visited a website where the integration of Calendly with Google Analytics too confusing. You've come to the right place.

In this article, I will cover the easiest way to track Calendly or Tally events on Meta and Google Ads.

**We're not using a thank you page because many users leave it before it fully loads.**

I'm going to get straight to the point and list all the steps over here.

## **Prerequisites**

* Calendly **Standard**, **Teams**, or **Enterprise** plan (Google Analytics integration required)
    
* Active **Google Analytics 4 (GA4)** property
    
* Active **Google Ads** account
    
* Admin access to all three platforms (Calendly, GA4, and Google Ads)
    

## Setting up Calendly with Google Analytics

### Step 1: Setup Calendly with Google Analytics

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713183038839/5d0c167b-99c4-4b8c-9461-7d623aef143b.png align="center")

Go To Calendly &gt; Integrations &gt; Google Analytics and when you're here, you need to enter your Google Tag ID, which you'll obtain from your Google Analytics dashboard.

### Step 2: Verify Calendly is linked to Google Analytics

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713183554487/caf3fcc9-6c2c-48bf-be87-5fef11a1b236.png align="center")

Go to Google Analytics &gt; Admin &gt; Data Collection and Modification &gt; Data Streams and ensure it indicates '***Data collection is active in the past 48 hours***.'

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Need help? I’ll set this up for you for $199 — <a target="_self" rel="noopener noreferrer nofollow" href="https://nikhil.pro/paid" style="pointer-events: none">Book a Setup Session</a></div>
</div>

### Step 3: Verify Calendly Events on Google Analytics

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713183843898/a818b5b8-12db-4c51-82ba-d77123cc2261.png align="center")

Now, go to Google Analytics &gt; Admin &gt; Data Display &gt; Events.

Calendly has five important events that we need to focus on, and you have to ensure that the following events appear on the events page.

* **invitee\_event\_type\_page**
    
* **invitee\_meeting\_scheduled**
    
* **invitee\_scheduling\_page**
    
* **invitee\_select\_day**
    
* **invitee\_select\_time**
    

Don't worry if they don't show up immediately, as it takes some time for the events to appear. Just **make sure that you trigger the events by scheduling a meeting after setting up Google Analytics.**

We have to focus on the **invitee\_meeting\_scheduled** as this is the last page which also means that the meeting has been scheduled, and we only want to track the scheduled meetings.

### Step 4: Set Calendly Event as 'Conversion' on Google Analytics

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713184393271/89b7fc52-4ba3-44b8-9ca9-3567b9e79eba.png align="center")

Once you see the Calendly events in Google Analytics, you need to set "**invitee\_meeting\_scheduled**" as a conversion by checking the checkbox next to it.

That's it for Google Analytics.

Now, let's move on to Google Ads and connect Google Analytics with Google Ads.

## Importing Calendly events into Google Ads

### Step 1: Connect Google Analytics 4 to Google Ads

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713190316490/311423fe-2d38-4044-8cb6-0cc69fa76397.png align="center")

Go to **Google Ads &gt; Tools &gt; Data Manager &gt; Connect a Product** and connect your Google Analytics 4 with Google Ads, this has your invitee\_meeting\_scheduled that we will need later on.

### Step 2: Import Calendly Events to Google Ads

To Import Calendly events to Google Ads, go to Google Ads &gt; Goals &gt; Summary

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713191167782/790f5625-dfd8-403b-ac30-ef3320ebf83d.png align="center")

Click on '**New conversion action**,' then click on 'Import' to import data from Google Analytics or other sources. Select Google Analytics 4 properties, then 'web'.

Here, you will see the Google Analytics event called invitee\_meeting\_scheduled that we marked on Step 3.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713191435546/cee2d265-520a-4920-86de-5d8fcf62d3ca.png align="center")

**Click on Import and continue.**

### Step 3: Verify Calendly Event on Google Ads

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713191698464/dd7f15ca-ed1a-4631-9cb4-04614d1c94cf.png align="center")

To verify Calendly event on Google Ads, just go to Google Ads &gt; Goals &gt; Summary and you will see the imported invitee\_meeting\_scheduled event and the status will be active.

This means your Calendly event is setup and ready to track calendar meetings.

---

### Can you track Cal.com meetings on GA-4 or Google Ads using this method?

Unlike Calendly, Cal.com [does not support](https://cal.com/help/bookings/analytics) automatic event tracking for third-party analytics tools. To track [Cal.com](http://Cal.com) meetings in GA4 or Google Ads, you’ll need to configure it through Google Tag Manager. While about 90% of the setup process is the same, there’s one additional step - setting up GTM to handle the tracking. I can help you with linking Google Ads / Google Analytics to Cal.com

---

## Calendly/Cal.com to Google Ads Booking Tracking Service

I have helped 100+ businesses track Calendly bookings on Google Ads, book your consultation today and track your bookings easily

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1758713054235/91c0a72f-8b5c-41c2-96bd-60c44a3a3ada.png align="center")](https://nikhil.pro/paid)

That's it. Now you can run ads and track the Calendly conversions (meetings) on your Google Ads.

The setup is simple, but if you’d like me to do it for you, you can [book a paid consultation session](https://nikhil.pro/paid) for **$199**.