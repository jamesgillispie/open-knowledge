---
type: reference
title: RudderStack CDP Tutorial for Newbies — Video Transcript
description: Timestamped transcript of the 'RudderStack CDP Tutorial for Newbies | Marketing Data Platform Demo' video by How to Hippo, walking through RudderStack sources, destinations, collect, transform, activate, govern, monitor, and settings.
tags:
  - analytics
  - area17
channel: How to Hippo
source_url: https://www.youtube.com/watch?v=fax1DcagzCE
duration: 09:02
published: 2025-07-17
transcribed_on: 2026-04-30
---
# RudderStack CDP Tutorial for Newbies — Video Transcript

- **Title:** RudderStack CDP Tutorial for Newbies | Marketing Data Platform Demo
- **Channel:** How to Hippo
- **URL:** https://www.youtube.com/watch?v=fax1DcagzCE
- **Duration:** 09:02
- **Published:** 2025-07-17
- **Transcribed on:** 2026-04-30

---

[00:00:00 → 00:00:39]

Hey everyone and welcome back to our channel, your go-to place for tech tools and software walkthroughs made simple. In today's video, we are diving into Rother Stack, the powerful marketing data platform designed to help you collect, unify, and activate your customer data across all your tools. Whether you're a marketer trying to build smarter campaigns, a developer looking for event streaming solutions, or a data team needing reliable pipelines, Ruther Stack brings it all together with a privacy first approach.

[00:00:37 → 00:01:26]

So, if you are ready to take control of your customer data and supercharge your analytics stack, hit the like button, subscribe, and let's begin. Now the first thing that you need to do visit the official website of Rudderstack. On the top corner you have the option to log in using your credentials. But of course we all know that the better option is to click the try for free. If you do you will be forwarded to a new page. It's very simple. You just have to provide all the information needed and click the sign up button. And to make the account creation faster and easier, you can also sign up using your Google account. Once you have successfully created your account here in RotterStack, you will be forwarded to

[00:01:23 → 00:02:12]

this specific page. It's very important to add a source so that rudderstack can track and collect data from different apps and platforms by adding them as a source. Okay. So, you need to choose a source, name the source and configure the source. I want you to click that blue button and you will be forwarded here. Okay, so you can use the popular sources such as Android, of course, JavaScript, web hook, source, node, python, snowflake, iOS, and http. Now, you can also choose from any of the following.net and a lot more. So, at this point, if you're not familiar yet with the um the source, you might want to skip that, okay? But we're going to discuss all

[00:02:10 → 00:02:58]

some of the features that you can use here in Ruddertock which is going to be now the directory is going to be your central hub for all data sources and destinations. So think of it as going to be your integrations library. All right, this is where you can connect tools like these PHP node Monday source and a lot more. So when you find your sources, that's going to be your data coming in. And of course, the destinations is going to be where you would like to send your data. Similar to the sources, you can use the popular destinations such as um Amazon S3, Amplitude, BigQuery, HubSpot, Snowflake, and a lot more. Red Shift. So you might want to click that as well.

[00:02:55 → 00:03:29]

Now again if you are not familiar with the um data sources you might want to ask your client or your guard stationation to provide the information needed here and of course the access but for now we're going to go to the collect se um collect section that focuses on the uh data ingestion and again before you can move forward you need to add some resources because that is the only way you can manage how you collect the first data from websites.

[00:03:25 → 00:04:10]

of course the mobile apps or cloud apps. It shows any event tracking like like um SDK setup schema validation and real-time data flows. It's going to be the foundation of customer event data gathering. If you want to create a transformation, you can do that as well. It's very easy. All I have to do is create a custom transformation and you need to choose from the transformation templates. All right. So you have the um allow list, deny list, jolocation enrichment, replace a pill, parse user agent, hash pill, and a lot more. If you want to create a timestamp conversion, you might want to do that. But make sure that you choose on the drop-own menu.

[00:04:08 → 00:04:46]

It's is it going to be like a JavaScript or a Python depending on your preferences. And of course, you have the ability to run the uh chest payload if you want. Click the run test. want to make sure that any events here you can edit. And of course, you can use the difference. It's up to you. All right. And if you want to save that transformation, I want you to click the blue button right here once you have finalized all the data. But you want to make sure that all the codes are correct and all the parameters are in check. And then after that is going to be the activate section wherein this is where you put your collected data to work.

[00:04:45 → 00:05:18]

There's going to be a new model here wherein you can help to sync data with a downstream tools for marketing analytics or personalization. There's going to be a search button here to search applicable sources. And since we are using a free trial, we only have like um 10 limited section for that. Of course, you just have to follow the five steps here like select a source, setup source name and source type and configure source review and create.

[00:05:16 → 00:05:59]

Okay, now I'm going to click the cancel because if you don't have any access to the reverse ETL here like BigQuery, data bricks, snowflake and trreno all these data sources, you're going to be not going to be able to move forward. Okay, so I'm going to go to the govern section because the govern section is where you can track the data quality, privacy and schema enforcement. If you want to create an event so that you can track schema drift, manage identity resolution and apply data governance rules, you can do that. Okay. So for example, let's say in this instance, we're going to be naming this as how to use rudders tag.

[00:05:57 → 00:06:41]

You need to put some sample description and select the category. Is it going to be like conversion, general, marketing or onboarding. I find this very useful useful for compliance and keeping your data pipelines trustworthy and clean. It helps maintain data integration. Let's say general and observability. Click the save button and we have that already covered. Just like that. And of course, the tracking plan is going to be an option for you to ensure data qualifies and validate your expected events against the live events that are delivered to runners tag. If you want to create a tracking plan, it's going to be easy because you just need to pull from source. But I want you to click the use template.

[00:06:40 → 00:07:29]

Now, is it going to be like um e-commerce? If you do that, you need to uh you need to name the tracking plan, map properties to events, and of course connect to source and configure. I'm going to cancel that for now. Yes, I'm going to leave that. I'm going to go to the monitor which provides the real time logs and metrics to help you track system health. Here you can see the event delivery success failures and throughout which is kind of really great for debugging and ensuring your pipelines are running smoothly. Of course, the syncs option is going to be if you want to refresh, you have like five tabs here at the top corner. Here you have the created, succeeded, failed and aborted. And if you want to re refresh and retry aborted, you can do that as well. The settings is going to

[00:07:28 → 00:08:18]

be your workspace and system configuration area. You can manage teams here. API keys, token, permissions, and preferences. And of course, you can set up roles, billing, and global options for your water stack workspace. And if you wanted to chat with the specialist, if you have like more questions, you can do that as well without getting problems. And these are going to be some of the features and updates if you wanted to know more about Rudderto like um updates and release notes. Okay. And with that being said, and that's a wrap on our walkthrough of Roersto. So if you are looking for a developer friendly platform that gives you full control of your event data, Rudderstack is a powerful alternative to traditional CDPs. It's a scalable privacy conscious

[00:08:16 → 00:09:03]

and integrates with most modern data stocks. So whether you're in marketing, analytics, or engineering, it bridges the gap between data collection and action. From setting up your sources and of course destinations to activating customer data and ensuring governance, runners tank makes it very easy to unify and use your customer data across tools and teams. If you found this video helpful, do not forget to give it a thumbs up, subscribe for more tech walkthroughs, and hit the bell icon so you never miss an update. If you have any questions about Rudderto or if you have any experiences using it, drop them in the comments below. Would love to hear from you. And as always, thank you so much for watching and we will see you again in the next one.
