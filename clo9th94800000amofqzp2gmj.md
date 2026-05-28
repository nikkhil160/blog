---
title: "Facebook (Meta) Ads Not Recording Add-To-Cart or Purchases?"
seoTitle: "Meta Ads (formerly Facebook) not recording add-to-cart or purchases"
seoDescription: "This article outlines the steps to fix Meta Ads not recording add-to-cart or purchases. There are multiple troubleshooting steps to fix the Meta Integration"
datePublished: 2023-10-28T09:05:31.496Z
cuid: clo9th94800000amofqzp2gmj
slug: meta-ads-not-recording-add-to-cart-or-purchases
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706866600939/6377bd2c-c256-40b5-8781-cb896df119fa.png
tags: facebook, meta, facebookads, metapixel

---

Meta has upgraded their ad algorithm to [Meta Lattice](https://nikhil.pro/meta-ads-unstable-after-july-2023-all-you-should-know) after that several users have been facing several issues including ads being unstable and Meta Ads not recording add-to-cart or purchases (sales), remember it's not you! It's just happening with everyone and we will try to fix the issue.

### Check if the Meta Pixel is connected properly

**Troubleshooting Step 1:** You have to verify if the Facebook Pixel (now Meta Pixel) is connected properly to your store. You can do it by going to Facebook Business Manager &gt; Events Manager and you will see your Pixel on the website.

**Troubleshooting Step 2:** Install the Meta Pixel Helper Chrome extension on your Google Chrome browser by using [this link](https://chrome.google.com/webstore/detail/meta-pixel-helper/fdgfkebogiimcoedlicjlajpkdmockpc) and go to your website, select the Meta Pixel Helper extension and see if that finds the pixel. Make sure your ad blocker is disabled.

![Screenshot of Meta Pixel Helper extension to troubleshoot Facebook Pixel Issues](https://cdn.hashnode.com/res/hashnode/image/upload/v1698482278372/e8e4a458-0817-47f8-93f6-eb63495f423b.png align="center")

### **Check Event** Prioritisation **in Meta Business Manager**

Make sure your events are prioritized for iOS 14 and your website's domain must be linked to your pixel and verified using an HTML code. You can check the prioritization settings in the events manager.

![Meta (Facebook) pixel event name with event descriptions](https://community.shopify.com/c/image/serverpage/image-id/60699iB25A80B530DC63B8/image-size/large?v=v2&px=999 align="left")

If you are running an e-commerce store then follow this pattern for pixel prioritization (from high to low) Purchase &gt; Initiate Checkout &gt; Add to Cart &gt; View Content. Purchase events should be on high priority.

### **Check Event Match Quality in Meta Business Manager**

![Check Event Match Quality in Meta Business Manager](https://cdn.hashnode.com/res/hashnode/image/upload/v1698482410354/f9acc080-6339-440c-a461-6454f3a18a0f.png align="center")

Go to your Facebook Business Manager then head over to Events Manager, click on your pixel and you will see multiple columns like

Connection method, Event match the quality and total events, you have to focus on Event Match Quality and should be either Great or OK, if that's poor then you should follow the troubleshooting steps by Meta.

### **Test Your Events using the Meta Events Testing Tool**

Head over to your Meta Events manager and select your pixel, click on test events. Enter your domain (website URL) in the test browser events page and click on Open Website

![Test Facebook Pixel Events using the Meta Events Testing Tool](https://cdn.hashnode.com/res/hashnode/image/upload/v1698483165353/11a1cf11-6863-41be-aec5-988bf193b1de.png align="center")

![Test Facebook Pixel Events using the Meta Events Testing Tool](https://cdn.hashnode.com/res/hashnode/image/upload/v1698483263125/8dba14d6-d887-45aa-a044-535853b5df1e.png align="center")

After that open some pages on your website and go back to the Facebook tab and you will see the events processed. Make sure your ad blocker is disabled.

If the events don't show up then check your website for the Meta Tag.

### **Configure Meta's Server Side Conversation API**

Because Apple or other Operating Platforms block the trackers which makes Facebook hard to pinpoint the purchases make sure you are sending both browser-side events as well as server-side events to Meta (Facebook) so that Facebook can get data from the user as well as from the backend of your website. Shopify and almost all major platforms allow conversation API by Meta now.

### Hire A Professional

Do you need professional help? I can help you with Meta Pixel-related issues. I have experience connecting hundreds of Meta Pixels and have recently solved the issue of iOS14 not tracking purchases. You can schedule a call with [Nikhil Sharma](https://nikhil.pro/meeting)