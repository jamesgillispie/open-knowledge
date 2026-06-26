---
type: reference
title: Technical Architecture Walkthrough for AREA 17 Website Project
description: NASEM codebase walkthrough notes and full transcript covering NAPAR/Saloon integration, Pool Party taxonomy, Material Store, Binder, sync, and tech debt.
tags:
  - client
  - nasem
  - area17
meeting_title: Technical architecture walkthrough for AREA 17 website project
date: Dec 15
---
# Technical Architecture Walkthrough for AREA 17 Website Project

### NAPAR API Integration Architecture

- Uses Saloon package to standardize API requests and reduce integration complexity
- OAuth authentication with automatic token refresh to handle long-running processes
- Paginated requests for projects, events, with helper methods for chaining operations
- Each project requires multiple API calls to get complete data:
    - Base project info
    - Committee details
    - Committee supplemental
    - Award information

### Pool Party Taxonomy System

- Third-party service for managing taxonomies, implemented after development started
- Migration from internal IDs to Pool Party IDs created ongoing complexity
- High failure rate in production due to timeout issues
    - Requires job queuing for automatic retries
    - Processes schemes: topics, statuses, types, units, material types
- Relationship built through NAPAR - users connect Pool Party taxonomies in their system, not ours

### Material Store & Binder Integration

- Material Store: Internal PDF/document storage system with NAPAR API interface
- Binder: Separate digital asset management provider
- Token-based access control - each token scoped to source system (NAPAR vs Twill)
- Dual management system:
    - NAPAR can add/update materials via API
    - Twill users can manage materials internally
- Complex relationship mapping through metadata and related records tables
- 34,000+ materials requiring efficient querying strategies

### Data Synchronization Challenges

- No incremental sync capability from NAPAR - must pull all projects every time
- NAPAR aggregates data from multiple internal sources, creating delays
- Sync ID system tracks which records updated in each sync cycle
- Soft delete stale records not updated in current sync
- Publication sync uses new endpoints (added in last 5 weeks) with last-updated timestamps

### Technical Architecture Pain Points

- Awards/award cycles relationship misunderstood during initial development
    - Originally built as one-to-many, actually one-to-one
    - Created complex filtering logic that could be simplified
- Time zone handling issues:
    - Server runs UTC, events come in Eastern time
    - NAPAR provides timezone as “PT” instead of proper IANA format
    - Hard-coded Eastern time display needs localization
- Program status logic overly complex due to architectural assumptions

### Development Process & Communication

- Primary communication through shared Slack channels with NAPAR team
- Mark serves as liaison between NAPAR developers and PHP team
- Tickets often require back-and-forth with data provider
- 1,300 tickets total - largest project James has worked on
- Multiple failed/reopened tickets indicate data model misalignments

### Performance & Infrastructure

- LiveWire component for media uploads with Alpine.js conflicts resolved
- Pre-commit hooks running on entire codebase causing slow development workflow
- Horizon job queues generally stable, some timing conflicts with NAPAR releases
- Server capacity tripled during launch, may need optimization when reduced
- Swap.js causing navigation issues and SEO concerns

---

Meeting Title: Technical architecture walkthrough for AREA 17 website project
Date: Dec 15

Transcript:

Me: Hey, anthony.
Them: Hey, how's it going?
Me: Pretty good. How are you?
Them: Good.
Me: Good. Tim's going to jump on. But. If you saw this, Doc. Put this in here. We'll just go through this kind of. Just kind of question by question. Just totally informal. I mean, I feel like this is kind of a brain dump exercise. And if anything, I'm not uncovering here or thinking about. Just feel free to. I don't know if there's anything missing from this. That is important in your mind. But yeah.
Them: Okay?
Me: I don't know if the best way to do it is to look at VS code or what? I don't know what ID is, but look at the code base together or just kind of chat through. What do you think?
Them: Yeah, I think probably the code base. Is ideal.
Me: Okay?
Them: Yeah, So I can share my screen and work through that. Just going to wait.
Me: That'd be awesome.
Them: For this finish.
Me: Yeah. We have an hour to cover the whole code base. I was looking at the tickets. There's, like, 1300 tickets. That's insane.
Them: Yeah.
Me: I don't know. I want to kind of put like I want to. Capture how large this project is, because I just keep saying this is the biggest project I've ever worked on. But there's empirical truths to that. I've never worked on a website that. Had 1,300 tickets.
Them: Yeah. Okay, so I guess I'll start with Napar, because. And then we'll go to Nap. So for those integrations, we use Saloon, which kind of takes some of the edges off of integrating with different APIs.
Me: Yeah.
Them: The connectors and the requests are defined in HTTP and then integrations. So we have the ones for Aptify, Binder Camera, which were, you know, moving away from Napar and Pool Party. So the connector kind of defines how all the different requests will be created. And you can override those on, like, a per request basis. So for Napar, we specify some. How many tries in the retry interval. This is using OAuth. And then we set up the constructor to pass in the information for the API credentials. This boot method just handles the refreshing of the token. We were running into issues with like some long running processes like or the gran's kind of airing out. So we've added this into refresh the token when we need to. To find pagination, then these projects and events. So these are kind of little helper methods on this constructor, so that when you're using the, the, the client, you can kind of say like this, you know, napar connector and then projects. And then once you get this project, so you get this, this project's. Resource. And then you can call these methods off of it. So it allows kind of chaining off of like the passed in. What is it called? Connector. And then for these, this is like we use all. I think we use filtered for the most part. Then you can, you can. This one gets a specific project. This gets the award for the project committee. Committee, supplemental. And then lookups, we don't really even need this. This lookups. We, when we first started on the project. Before Pool Party was implemented, we would we like, needed to get lookups to get all the different types for the projects that.
Me: Wow. Pool party. Pool party was added on after you started development. Is that what you're saying?
Them: Yes, but it was, it was a knowing, like, it was, they were going to migrate through that. But like, we, it wasn't ready when we, when we. Yeah, when we started. And then, like, even towards the end, we were still not getting pool party IDs from the neighbor data. And so, like, that was a whole. Thing to like migrate from the IDs that they were using internal to the pool party ideas. So right now we have a cron that that runs these lookup, gets these lookups, but it's only for, I think, region. And what was the other one? There's like, there's two things that we get in that lookups cron and it they're not really things that we use. Like, I don't we have and we store region information, but I don't think we ever use it. So. Yeah, not that.
Me: Wow. It wasn't. Right. Wow, that's crazy. Oh, my God. W. Ow.
Them: Not that important.
Me: Yes.
Them: So in the sync.
Me: All right.
Them: Projects command. We go through and we get all the projects. And then we, for each project we go through, and then we, like, actually sync that project in. So the content that you get from this. Result is not like all of the project's information. It's like you get results and then you have to use, like, you get a bunch information, but it's not everything that we need. And so once you get a list of all the projects, then you need to make another request for each of those projects. To kind of get the, like, the. The. All the information that we require for. For syncing in. And then for cling. Sorry. Go on.
Me: So. No, keep going. I'll just ask my questions after you stop.
Them: And then to clean up records, we added in this, where it was like, generate a. A sync id and then we just pass it into the sync project. So every time we sync a project, we update the sync id, so then we know which projects have been updated in which, like, sync. So at the end, what we do is we just clean up stale project records and we pass it into sync IDS for. For that. So any projects that, you know, don't have this thing id we. We. I think be soft, delete them.
Me: And this is connected to the cms, too. Like the manual, I'm guessing. Is this part of that, or is that a separate. Yeah, okay.
Them: Yeah. It. It is this one. So you can sync a specific project from the project view in twill or on the sync, you can actually, like, run this. I think it. It actually triggers this. What is it called? I think it's, like, sync. Sync. Can't remember. It's like. Sync controller. That must be it. So it will call the sync projects. Yeah. So it just runs that. That command, and then that the, the command triggers out all these. All these jobs. So we run through all the projects, and then here we dispatch a new job to sync the project, and this job will. Gets the ner connector. Binder connector. And then we. This call right here gets the project from. From Napar. So that's that where we have the neighbor connector and then projects that sort of helper method. And then we run the get method off of this, which is going to call the get project request and then we pass it in. A pin and we get the DDO or or fail off of that, and then we go through and sync in the different. Yeah. The different information, this, the project requires a couple of different calls. So like here we have to get the committee and then the committee supplemental as well as when we sync in awards, we have to get the, the project award here. So when we sync in a project, we have to make a few additional calls to neighbor to get the supporting information.
Me: Got it.
Them: And then this does the same thing as before. Where. When. When this, like, this gets those sync ideas. And then at the end, in the. In the cleanup. So, like, cleanup stale project records. We. We clean up projects. We clean up award cycle, award, award cycle, awardees, award cycle, and award. So this is all based on that sync id.
Me: That record or whatever. Yeah, okay. So just for my. In the cms, like. There's, like, the individual. You can update individual projects. Right? And then that just calls on that. Okay. Okay, got it.
Them: Yeah. This calls on where would it be? It would be project info so down. Here. We call a the sync project, which is admin sync, and then we pass the pin. So that would be Project Controller.
Me: Okay?
Them: And then this just dispatch syncs. I think this does it in real time. And get the exit code, and then so we can tell if it. If it succeeded or failed.
Me: The other parent. I got it. 'll cool. And then the prawn jobs or whatever you want to call them. The, like, scheduled, the horizon type things. I don't know what the. I guess they're cron jobs, right?
Them: Yeah, yeah, yeah, yeah. Schedule the Quran, I think, runs to run the scheduler.
Me: Yeah. And those are? Got it. Got it.
Them: Yeah.
Me: And the scheduler isn't just is it using. Because I know there's a lot of, like, work on dates and time, and I think that's the part that I. I'm a little anxious about. And I don't know, I guess that's separate from the event times. Right? Am I? I'm just kind of talking, thinking out loud, but.
Them: Yeah.
Me: So the. The scheduler is just running on kind of like utc, right? It's like it doesn't. It doesn't have anything to do with, like, the time of the events or anything. Those are two separate things, right?
Them: Yeah. Yeah. So the server will be in UTC time, and so we. When we schedule that, we need to convert. Okay, well, if it's going to be in utc, then we want east coast time. The crons to run at this interval, then we have to do that conversion.
Me: Okay?
Them: And that's kind of where we were running into problems with the events or the application acceptance dates was that we were getting times in primarily, I think, east coast, whatever it is, Eastern Standard Time or. Yeah. In that time zone. And then when we're doing the comparisons, like the because the servers in utc, anything that uses like now or today or those will be all in UTC time.
Me: Yeah, yeah.
Them: And so right now, like there is, we did push an update to convert any dates that we get for projects. Into utc. Like we just saved everything is as utc so that when we're doing those comparisons in the code base that we're, we're doing everything against UTC time. And then when we need to display the, the date, we do a conversion into. Right now, I think everything's just kind of hard coded. To be displayed as east coast time. But for events that still. I'm still working on that. Like, ideally I would get the like the UTC timestamp from the NAPAR API for events because there's still a little bit of like when you're viewing event that is taking place in California. Like you should. It should be displayed in. In local time. Right? Like you should.
Me: All right.
Them: See it in local time, right? Like, because, like, on our. On the event. Modal. We have, like, the. The, you know, start and end time. For the event. Let's say it's 4:00 to 5:00 and then we're right now hard coding that as conversion into Eastern time. And then.
Me: But how does that know the location of the event? Is that part of the equation? Like you're trying to say this is.
Them: Yeah, the we do. When we get the event data from napr, we get a timestamp. We get an offset and we get a time zone. And so the time zone is the time zone of the event, but the time zone that we get from Napar doesn't. Isn't in, like, You know, Pacific Standard Time or Pacific Daily Savings Time. It's just pt, which isn't a time zone that I can use. Like, I would have to convert that into, like, the I can time zone. Like, what is it? America? New Los Angeles?
Me: Right. New york. Yeah. Got it. Yeah, yeah.
Them: Yeah. Eric. Yeah. And so there's just. There's just some weirdness in the way that I'm currently getting. Getting the. The time, because the offset.
Me: Have you. Have you talked? Yeah, well, sorry, just real quick, can they change the way that that is displayed? Like, I'm curious about that process. Like, I know you've worked with Mark a bunch. And, like, so how much control do they have, like, on their end to, like, fix, like, something like that or any other maybe example that you can think of?
Them: There there is a change in in in dev that I can post the. The thread because he did make a change. But it didn't end up. I don't think it will work out the way that I want. Here it is.
Me: So when you say he changed to Dev, what do you mean by that? Just curious.
Them: Like he changed the the payload in the dev environment for the Nabar API.
Me: The napar Dev, just so I know what you're talking about.
Them: Yeah, yeah, the nap part.
Me: Just okay.
Them: Yeah.
Me: And how much like, how much have you. Have you spent any time in nap? Like, do you know what that like, I still never seem. Like I just have. You got eyes in there like so.
Them: No, no, really. I get the occasional screenshot, but I've never seen what it looks like, and I don't know how it's built. I don't know what language. It's not, you know, PHP or anything, so I don't know what they're using for, like, on their Android. So, yeah, so, like, that thread that I just posted in chat just goes through, like, what were you saying? He posted a change. And then I'm trying to get the. The like a. I'm trying to get it so that I can get the. The utc time.
Me: Got it. So raid is like, He's. I. I granted Mark access to the repo. I'm, like, starting to wonder. I'm just imagining a scenario which, like. He could do, like, end to end. Do you think that? Could you imagine that or. No, you wouldn't let those guys. What do you think?
Them: End like. What do you mean?
Me: Well, like, imagine a scenario where he, like, updates Napar and then he goes into the code base and updates. Like, can you. Can you imagine that happening, or based on what you know?
Them: No, I don't think so. Because the people that do Napar, they're not PHP developers. And then Mark is, and so. But he would be able to kind of liaison between the two.
Me: All right. Right, but he's not gonna. He's not gonna cut.
Them: You know, the. The website or whatever. Yeah, the consuming side, but I don't think one person on their end would be able to do both.
Me: Yeah, right. Right. It Raids. Sounded very curious to get in. I'm gonna grant him access. The next day or two, but. Anyway, trying to think of these types of things where you've been so integral in working these things out with them throughout the whole thing. It's amazing that Pool Party was implemented after development and started like, I did not know that.
Them: Yeah.
Me: But, like, I mean, it just sounds like you're just in terms of the process, like. You know, a ticket comes in, I need to fix this. You look at it, you say, well, the data we're getting doesn't give us what I need. And then you slack, right? Or do you select Talia just in terms of the process? Like, how do you.
Them: I mean, we've. We've kind of done both. I think I have to, like, within that, that thread there, like, I've been trying to get an answer for a couple of days now. So I'm thinking, well, now I have to bring somebody else in or maybe email him directly and just be like, hey, can you respond to this this thread in Slack, but for the most part, yeah, like use the share channels for visibility. But I wouldn't bring in I wouldn't like at Tally out right away unless she's kind of been involved in the conversation. Then I keep her up to date on what what the developments are just so that she's, she's aware. So, like, if, if she's in an email thread, then obviously, like, I just keep everybody in the email thread as we're working out the, the solution.
Me: Yeah. Right? Right. Yeah, she's a cross. Can we go back? Sorry, I feel like I skipped over to Dayton time, but can we look at pool party and material store? It just so I feel like I'm getting a better deal. But do you. Is that okay? I feel like this makes sense to me. The Scheduler and everything. I just kind of want to not skip over the pool party. I don't. It doesn't sound like it's that complicated, but it's. Again, it's another, like, API that I've never. I don't really know where it's coming from and who updates it and how. You know, if I need to change.
Them: Yeah, yeah. Yeah. Yeah. Yeah. Pool party. Is this. This, like, actual. Where is. Like pool. Come on. Pool party biz. So, yeah, it's, it's a, it's a third party for managing taxonomies. And so we, we integrate with them. So the integration is, is pretty simple, but we do have a lot of issues with it. If you look at the, like, production horizon, the highest rate of failed jobs is this pool party. Because of timeout issues.
Me: Yeah.
Them: So we have this. The command just dispatches this job. And the reason why we have this job. Is because of the fact that it fails so often that we need it in jobs so that we can kind of track and it can automatically retry. So pool party also uses saloons. We have our pool party connector. We run this call to get the schemes, and then we run through each of the schemes. To process them. So here is where we kind of define. These are the ones that we, that we support and then how we, we process them. So we get a, you know, an array of topics, statuses, types, units and, and material types that is a little bit different. This uses the, the same thing. So, like, this ID is material, tapes. Whereas where is it? This ID is project types. So we don't have event types. Events use the same types as projects. So we get the array. So, like process topics, we get the properties from the what we get from pool party, and then we just update or recreate that, and then we process the subtopics on that. So it kind of calls itself. With the. With the. The kind of the lower level two and then level three. Topics off of. Off of that.
Me: And the. The project ideas, the unifying. Right. Is that right? It's the. The taxonomy is connected to the Project id. Am I saying that right? Is it Project ID or just id? I just say ID and then the na. Par. ID is the project. Is it project? I'm sorry. I'm like, my brain broke a while ago.
Them: The. The way the like. The FR like the pool party types are connected to. To projects through the like type relationship. So in when we sync the sync the project. Job.
Me: So it's not using the id, it's using the type. Like.
Them: So we sync in the pool party types and then when we get the the type from or the project, that's where we'll like have this type id so we get a type ID where we get the pool party ID so that we do get the pool party ID from Napar for the project and then. We get the ID of the the model?
Me: So the relationship. Yeah, okay. Just so the relationship to Napar is created.
Them: So.
Me: It's created. So pool party is connected to Napar. And in Napar. You're in a project. And you've the user connects the pool party, right? Is that how basically it works? Okay. And then you're that.
Them: Yeah. Yeah. Yeah, so.
Me: 's so you're right. Okay, so then once that relationship is made, You're can. It's already. It's already. The relationship's already connected. You don't have to construct that.
Them: Yeah. Yeah.
Me: Got it.
Them: Yeah. So in. In the data we get from Napar, we get the cool party ID for the. For the type. And we call in all the types from Pool Party. And so then we just make the connection to our kind of models there. But they, they connect the type to the pool party in, in their system.
Me: Cool. Okay, let's take a. Let's look at material and then we can. If my mind hasn't melted already, we can keep moving through our questions. But yeah, it'd be interesting looking material store and. And how that works. Basically. How is that? Materials is a binder, right? That's like a totally separate. I know the answer to this.
Them: Yeah. Yeah. Yeah. So Binder is the digital asset management provider. Material store is a. What do you call it? Like a. It's like a. I guess it's like an S3. Like, it's where they store all their. Their materials.
Me: Yeah.
Them: For this is like Nepal for internally.
Me: Like, PDF, some documents and stuff, right? Not. Yeah.
Them: So. We have.
Me: But two separate things. Separate from B, there's no overlap between binder and material. Those are completely separate, right?
Them: That's right. Yeah. Yeah, they.
Me: Yeah. Okay, good.
Them: So we, like locally, we run like we have an API that Napar connects to. Let's see here. Material. Ap. I controller. So this is kind of the. The Napar's interface into material store. Twill has its own interface so that people can update and manage materials from within Twill, but for Napar, they have this. This API for adding and making changes to the material store. Just wondering if there's, like, Just go to the documentation here is it? API docs material. There it is. So they have, like, kind of full control, but everything is scoped to a. A token. Source. So in local if you're in admin and you go to material store API tokens, when you create a token you the source system of the token. So for this one, the NAPR import token is the source system is listed as. When this token is used, they only have access to materials that list out the sources system as Napar. So in this.
Me: Good.
Them: API when you create, when you store a material. You'll have this source system, and it's using the material token that they are using to, like, authenticate against. So if you're using an APER token, this will be napar. And when you're like filtering or searching, you'll, you'll be scoped to using this, this source system. So like, they can't, like they don't have full access to everything in the material store.
Me: Good. Good.
Them: See?
Me: What is this, by the way? Like, what is this? Just, like. Is this like, Postman. What is this you're looking at?
Them: So.
Me: This is just.
Them: Yeah. It's like if you go to. There was a command to build out the. These. These docs. So it's using this? I'm not familiar. I didn't set this up, but this is. Yeah, these docs are generated. So we take the. The. The spec, which is an open API spec, and then it reads these. These docs out of. Just out of that, that spec.
Me: That. Again. Cool.
Them: So you can. Yeah, you can run that command and you can get this on your local machine. I think it's. It might be in staging as well, but it's definitely not in production like this. This endpoint doesn't exist in production. So yeah, you can create new materials, update lists out like how updates are made, how you can filter and delete filtered materials. Delete. You can use like a source system id or you can use the material material ID for.
Me: What source System id? Sorry, just. I don't.
Them: So in, in Napar, they have the concept of like a material. So let's say they have Agenda PDF, that Agenda in their system will get an ID and they can pass that idea along to the API when they're creating the material, so that they know they can use their kind of internal ID for querying. Against the, the, the system. So let's see here in. Bring local. Let's see if I can find a. Yeah. So here's some of the digital health. This One store system ID is. Yeah, 1431 81. That's what was provided. That's how Napar knows of this URL in their system is by this id and then it has. We have a uuid. So you can use this ID where you can use this ID when. When querying against. The the material store API.
Me: So that's just how it's. The relationship is made. Cool. That's good to know.
Them: Let's see here. Okay, so. Yeah, like the.
Me: Sorry. Can we go back? Sorry. Before, that command that you said that you run, is that just like. Go back to that? So you run like npm.
Them: Npm build or npm run API docs, materials, or.
Me: API docs material, and then it just fires up that little local. All right. I don't. I don't know if that's in documentation. I feel like these should be captured, and they're. Read me.
Them: Yeah, yeah. Run API docs.
Me: I'm going to do, like, I'm going to take this conversation, it's being recorded by Gemini, and then, like, I'm going to say, cross reference our readme and update these very important things.
Them: Material. Yeah.
Me: So I could just. Yeah. So we're getting rid of. Why can I not pronounce Kramera? I feel like it's just not in my lexicon.
Them: Yeah.
Me: We're going to get rid of that. We're going to get rid of a couple things, but this is great. This is. This one isn't in there. Sorry, What. What were you saying? Oh, it is in there.
Them: Oh, just. Yeah, it just. It is in the dream, right there.
Me: Okay, that's good. To know.
Them: Probably. The one for publications probably isn't, but the publications one is, like. Very, very simple.
Me: Yeah. Well, good to know that's in there. I just don't think I ever used that. So don't know.
Them: Yeah. There's a. Didn't need to. What is it? Materials. Publications. Yeah. So this is like the. The publications one. She's just that endpoint to allow Mark to update a given publication. So it's just a post endpoint. It triggers a job for updating a single publication. So that was the other API endpoint. So those are the two kind of API endpoints that we or APIs that we have. On our end. Material store is obviously the. The bigger, more fleshed out one, and this one's simple. One. Okay, so that was Material Store. Oh, I'll go through the. The front end as well. So let's see here. I don't know why when I. So materials you can up add new one filter these. In order for something to appear on the front end, it needs to be public and approved. I don't know why they couldn't just have one that, like, makes it as public, but.
Me: So they manage materials in twill, though, that's what you're saying?
Them: They can manage materials in in twill.
Me: They can do it both ways. It sounds like they can just dump stuff in there. And it'll sync.
Them: I don't. I don't know, actually, if the. I don't. I think that like anything that with N needs to come from from Napar like there there is like if they make edits here. I think it does go back to to day part, but. Yeah, I don't really. I'm not sure on how the napar integration is with with material store. But for twil, like for the twill, like when you add a new you can it'll source system twill and then you can use that within collections, for instance. So like this one right here, this data set is added to twill under the material store for a, for a collection. So if you click on this, you can even see down here appears in collections. And then it shows you that it's a. It appears in, in this collection for. For this project.
Me: That's nice. Okay? A lot of hair, man.
Them: The other thing that.
Me: But, like, we're just at the tip of the iceberg.
Them: Yeah. The, the other thing that's kind of important about the material stores this metadata. So this is metadata that we get from. Napar, for the most part, but you can. You can add in your own metadata. So, like this, this specific material was. Pulled in through a. Like a Quran or not a Quran for a script to build out these repositories. So they provide these meta, this metadata. But this is how we're doing filters on these repositories. It's. It, it's not ideal. But it's the way that we can, like, kind of generate the ability to have, like, custom filters on there, on the repositories.
Me: That's. So that script. Who wrote that? Did we write or did they write it?
Them: We wrote it. It was just for migrating data. So in the future,
Me: Beard time. The one time.
Them: Yeah. In the future, if they're going to be creating these repositories, are going to be adding the materials to the material store. Creating the repositories and then associating the materials with those repositories so the. The scripts won't be. It won't be like. It won't be an automated thing anymore. It's just. Yeah, for migrating the repositories from the Oracle cms.
Me: Got it.
Them: The other thing is we have this related records. And this is a kind of a. This. This right here should have this project. I wonder if I go in. See here? I forget what it's called. So this sync material. No materials is bound to sync. This sync materials related items. Goes through and creates. Title. Creates these relationships for these. So, like, I don't know why this one isn't there. Let's go to. What's it page? 10. Part, this one. So these related records. So it says here, control by Napar. You can't edit this. What we get from Napar is this, this pin and then that script, the sync materials related item script. Goes through all the materials and makes these connections. So that the, the way that. The reason why is because originally we had the, the pin here, and then some of them had meeting id, some of them had event id, and we would be using that on the front end. For knowing. Like, when you're looking at a project, you want to see all the materials for that project. We were using this kind of metadata to filter out which materials should appear on that project. Because there's, you know, a lot of materials. Like right now on Dev I have, or on this one, there's 34,000 to kind of do that looking in. Like, it's fast, but it was making the queries kind of complicated when. When we needed to, like, do more. Kind of complex, like child relationships. Getting the. All the. The materials for, for, like, events and projects and, and having them all appear on the, like, the same, the same page, it was kind of slowing things down. So the. The script here to sync related items, what it does is it creates those relationships in twill. In twills related items. Tables, so. Here is. So under. Where is it? Twill related. This is where all the relationships are, are stored for, for these materials. Like, we have these materials here, and so now we have all this, this data, like inside a table and all the connections. So now the. When we're doing any filters on projects and getting their materials, then we just, we're looking at, like, database. Columns, which makes it a little bit easier to. To reason about. So that's what, like, that script does, and that's why in, like, in. On some of them, you can add the related records, and then some of them, you. You can't. Because if it's a Napar, if it's an apart material, then they handle all of that. That connection they tell us. Yeah.
Me: That relationship's done on it. And is there, Is there. Are we at an inflection point? Where do you know, like, going forward, will they continue or will it just be both? Or will it just be. Do you know, like, will they be managing.
Them: Yeah.
Me: It through twill more. More. Or is it tbd?
Them: I don't think so. I think that, like, anything related to Napar will still be related to Napar. Like this, this data, the materials, the. The metadata, anything that we. That we get from Napar will. The source of truth will always be a bar.
Me: Right. But we have. They have the option to. Scale it up to, like, extend it if they want to. Right. That's, like how we built it. Yeah.
Them: Yeah. Yeah. So for, like, the any of the projects events.
Me: That's cool.
Them: Like anything that we get from from neighborhood. So all these properties here, you can't edit them, you can only add in augment with additional information. But if they.
Me: Yeah. Right. Can you go back to that material real quick? You were just at. Sorry. Just click that. So. Just so I understand, like, can you scroll down? Like that. Related records. Like, controller. Like, how is that built? Like, was that built? I guess the, like, pool party thing kind of tells me that. Like. Walk me through, like, how that was, like, just. Was that, like, organically discovered, or was that, like, specked out in the, like, technical specifications?
Them: Sure. So. Yeah. No, it was. It was. It was. Or organic. So, like, this related records was added to the material store. For a different purpose. It was, it was added to, because before, if you wanted to associate a material with a project, you would have to go in here and add in the metadata. You'd have to add in, you know, type in pin and then type in the, the, the PIN for.
Me: So they were like, can you make this easier for us?
Them: Well, they didn't. They didn't ask. But it was just like, I. You know, it's one of those things where it's like, really, we should be. Right. If you want to attach this material to a project, then you should be able to find the project and then attach it in there. Yeah. And. So.
Me: Right. Just able to choose. Yeah. That's not, like, a huge amount of work to do, but it's like, it's additional quality of life things that we just baked in because we're. We're nice people. Yeah.
Them: No. Yeah, and. Yeah. And so. Because we had that for some of the. Right. So what I was doing was I was supporting both. You could add in your related records here, or you could add it in here. It's. We still support both, but if you add in a related record here in the script, what it's. Going to do is it's going to. We don't, we don't query this for these types of, of models. So anything that you put in here that should be in here will be.
Me: Right. That's.
Them: Whatever raised up or like, you know, pulled out, it'll be kind of pulled into. Into here for. For. For. For managing.
Me: Source. The truth? Yeah. Right. Yeah. It just feels like this whole back end is kind of like. It's like a fallback on a fallback on a fallback on a fallback, you know, like. Right. I mean, that's. I think that's. I think that's the trick is, like, understanding.
Them: Yeah.
Me: There's no way to really understand it because it's so complex. And at least I'm not smart enough to, like, I'm trying to. I think there's so many of those instances where, like, it was pulled in and done this way. But then in the creation of the site, like, we realized that this is untenable, so then we created a new way to do it. That was easier. But then we wouldn't want to get rid of the old way because other things have been done that way. So there's both, and then that's like there is no real.
Them: Yeah.
Me: The hierarchy gets a little lost. And yeah. Anyway, but that's all good. I mean, I totally get it.
Them: Yeah. Yeah. Like, there's a lot of hidden stuff.
Me: Because it's. It's. It's an insanely complex project, and it requires an insanely complex. Controllers. Okay. What a time we got. We got 15 minutes.
Them: Yeah. So, like your rate, like what I've tried to do when I was doing some stuff to where like is like appears in collection that listed and then it's like when a material appears in a repository collection, it is hidden from projects, events, Right? Because these are things that like I was getting bug tickets in. And they were saying, like, oh, this is not showing up. But it was because, you know, one request was when they, when they create something that is in a, in a collection, right? Like that, that's where it should appear. It shouldn't appear any. Like, we had all this, this back and forth on making sure that. When materials appear, they should only appear in one spot.
Me: Right.
Them: And so they didn't like if, if an agenda. Right. Was associated with an event. Well, it appears in the agenda section of the events page. And so once it gets pulled out of, like, the, the bucket, it needs to, like, disappear. And so, you know, you have that kind of hidden stuff going behind the scenes. And so like, this is my attempt of, like, being like, hey, heads up. Like, the reason why this material might not be showing up where you think it is because it's. You know, somebody's been in. Somebody's included it in a collection.
Me: Explaining it. Yeah. In terms of, like, that, like, CMS management kind of stuff, or, like, do you feel like it's. Do you think that could be. I'm just thinking ahead because we have a three year contract with like, and I, I feel like we'll continue to refine and, you know, quality of life stuff, like. But do you see, like, value in that or do you see it more as, like. I don't really know what I'm trying to ask.
Them: Value in in.
Me: Like, continuing to flesh out those kind of, like, explainers or, like, is there, you know. Yeah, and obviously that's like, not a priority at this point because we're kind of still post launch and. But like. And then do you think you're in the best position to make those decisions or. I would say you or Quentin? Both of you. Which are. I don't know what your status is. I could talk about that later, but, yeah, I'm just curious in terms of your opinion on, like, what.
Them: I do? Yeah. I think so.
Me: Is if, say, like, all the tickets are resolved and everything is perfect. Like, what would you. What would you spend your time doing? Like next? If that makes sense. Like, how would you continue to, like, improve this product?
Them: Yeah, I think that. I mean, one. Like tests, I think are important because, like, in your test, you define. The way things should work. And in defining the tests, you have an opportunity to go back to the client being like, hey, this is the rules that we have for this specific thing. Like, are those rules correct? And then you write your. Your test to kind of, like, make sure that you have feedback from a client saying that, like, yes, the way you've defined it is correct, and now you have a test in place to make sure that those rules will always be correct. As you make changes to the. To the system. Because I think that, like, for instance, the. There. There was a lot of tickets on the program. Status. And, like, when stuff should show and when it shouldn't show. Ins. So there was, you know, they would. Come to us and say, okay, well, this. This tab isn't showing, and it should show or on this one. And then we'll be refining this like we would make changes. That would fix it in this specific case, but it wouldn't, it would break it in other cases. And so having like an, like a defined rules that you can then. You know, have in the, in the test as being like, okay, well, the app application status. Will, you know, given this project in this state, it will display this status bar or this tab and this tab. And if the project is in this other state, then, you know, this will be hidden. And you can kind of develop rules around that, because I think that.
Me: How would you imagine that being, like, captured?
Them: Yeah. I'm probably going through the, like, looking at the. The current code and just, like, creating a doc around. The the current state. So like for instance, the, the project or the program statuses. The. There also, I think, was confusion around building that out. Through through Napar, so. For instance. Let's see here. In. In. Let's see here. Sync. Project. So when we originally were creating this, we had. Awards. Like, there was projects and then awards, award cycles and then award cycle awardees. But then we found out that actually when they were implementing it on their end, there was a misunderstanding in that awards and award cycles. Could, could exist without each other. So a, an award could exist without cycles, and I think that a cycle can exist without a. An award and. So the way that we had, like these, these. When you look at a program, we want to figure out if the program is open to accept applications. And so we want to see if there's a, like a current award, and the award has a start date and an end date. But because the, the in the database, we have that as a. Like a one to many relationship where a program can have many awards and an award can have many cycles. It kind of made things a little bit complex on. How we like assume when, when a project or when a program is is active, but I think that it's actually not a one to many, it's a one. Like it's a one to one where a program will have one award and then that award can have many cycles. And so when we're getting these, when we're looking at the, the current project, We're like, looking through the awards table, and then we're trying to find, like, a current awards. We're like, okay, well, does the program have an award that has a start date that is in the past and an end date that is in the future, or. And then we're like, we're assuming that the program can have many awards and we're, like, filtering it, but that might not be the case. And so there's, like, this kind of, like, Misunderstandings. I think that we've developed architecture around.
Me: Yeah.
Them: Because like in. In slack.
Me: But then we, like, patched it. Yeah, we, like, patched it through Slack and. But then there's no real reconciliation, right, of those changes. It's like, it works now, but. Do you know what I'm saying, like.
Them: Yeah. Yeah. But now it's very complicated because we're. We're doing all this, like, filtering. When I think that really, like, in this specific case, like, like.
Me: And that.
Them: It would really simplify things if we can just say, like, hey, like, a program has one award or no awards, right? Like, it's not. It's. We're not filtering. We're not trying to find the open award. It's like, does the associated ward have a start date?
Me: Right? Right.
Them: And an end date that is, you know, within.
Me: Do you see any movement on there? Like, management of the content based on this work? Like, I always call it like business therapy, where we're basically like,
Them: This.
Me: Coaxing them through their inefficiencies. Because, like, when you build a system. To organize their business or whatever, and you find all those inefficiencies, you can't even identify them until you get into those, really. But, like, I guess, have you seen them update their methods or even acknowledge them that, oh, this isn't right, we should do a better job? Like, have you seen that? At all.
Them: Yeah.
Me: They're just like, this is just how it is.
Them: No. And, like, we've been on calls. Where. Yeah, where they've been kind of arguing back and forth a little bit about, like, oh, we can't do that. Right. Like, for instance.
Me: A bureaucratic sludge. Yeah, yeah.
Them: Well, and, I mean, it's. Everything's kind of. Almost how you would expect it to be in. In a situation where there are kind of these. These silos. So, for instance.
Me: Yeah.
Them: When we get the projects. We have to just get all projects. There's no way for us to know. Give me all the projects that have been updated in the last 24 hours. The reason is they are aggregating what we receive as the project data from multiple different sources themselves. So Napar is kind of like an aggregation service, taking data from different systems.
Me: We're aggregating the aggregate. Yeah.
Them: And so, like. And so, like, you have this. And so, like, yeah, it's very, very complex. They're also, you know, doing the best they can with, like, kind of their, their system and the way things are set up and how different departments want to manage their data in different ways and. But yeah, so, like, this is. This is the. The Get Award Saloon request. And in here, like I used to, this is not how it started to look. But now this is what I have to do, where I get the response and then we get the award data, but then we have to add cycles. To this like we have to because. Like the. It was, it was changed, basically. Like, they pulled awards out and there was like, this issue that was there for a bit where they had made some changes and. Yeah. So anyways, this is like a pretty. This is a smell here that this is not. Right, Right. Like this, this integration. Is a little weird.
Me: Suboptimal.
Them: Yeah.
Me: Yeah. And it's like. Because nothing will change on their end, and they at least can acknowledge that. I mean, I feel like it's better than saying that that will change, but they won't ever do it. I don't know.
Them: Yeah.
Me: If it's a bureaucracy.
Them: Yeah.
Me: All right, well.
Them: Yeah. So my comment here allowed cycles to exist without an associated award. It was just. Yeah, that was when we originally created it. It was that you had award. Awards had cycles. But then that changed and now it's, you know. Yeah, add that in and it's a weird fix. And. Yeah. So, yeah, that would be kind of like, my suggestion for. For that where when you have, like, look back at the. The tickets with the most comments on it, like, back and forth and just being. Just seeing, like, okay, well, why was there so much confusion on this? Or, like, even. Tickets that have, like. I mean, there's a lot of tickets, but tickets that were closed. And then opened again and then close. Right. Like tickets that kind of went through that process of being. Oh, it's done to. Oh, no. Like, there's an issue here, and I think a lot of it will be around kind of. How data that they're doing in Napar, like, is pulled forward to. Trigger functionality on the on the site for showing and hiding information. Because everything else I think is, is pretty solid. Like if we get a project title from Napar, it shows up on on the website. But anything that any data that we get from Napar, where we're supposed to use that to trigger functionality on our end showing hiding. Pretty much like any of. Any of that stuff. Like statuses, status bars, call to actions. Like whether the event is live or not. Anything like that. I think is would benefit from just writing it out and saying, is, is this accurate? Like, is this your. Is our model the same as your model for how this should be put together and structured?
Me: Yeah. I mean, we've basically just, like, adapted our system to. It's. We've. It's like a, you know, contortionist, incredible accomplishment. To, like, you know, accommodate all. These permutations.
Them: Well, yeah, and that's something that, like, in the retro that, like, it'll probably bring up is that, like.
Me: We having a retro?
Them: Having a. Yeah, we're in January the grid of a retro yet.
Me: Oh, right, right.
Them: You know it like having. Like a better. Understand, right? Like the. The. The documentation that we got from. From Napar is. Let me just show you.
Me: Right.
Them: The. Where is it? Phoenix. Is this it?
Me: Like a dxt file. Oh, my God.
Them: Oh, no. This is for. This is for naps. Sorry. That's the NP1. Napar. This is it. So, like, this is the, the document for. That we got for. For. For Napar. Right? And it doesn't. It doesn't have any.
Me: Sending. I actually. Don't.
Them: Like. Like this doesn't have awards or committee.
Me: Can you. Can you cycle those? Can you recycle those, please? Just. I've never seen that. They're probably somewhere, but just.
Them: Yeah. And then this is the. This one for. What is this the. The. Yeah, this is the. The pool party one. So I can give you all three of those ones.
Me: Yeah. See you in mind, just so I can, like, stash them somewhere.
Them: Yeah.
Me: Well, I know we're at time. The rest of my questions search seems pretty straightforward. Yeah, the caching thing is, man.
Them: The only thing about the caching that like where is the dock? Okay. Dates and times. Yeah, we went through that. Still, they're just for the events. We still just need to tighten that up.
Me: Right. Do you think you'll get that through that by the end of this week or. Doesn't seem likely.
Them: I think that. I don't know. It's if. If we can get like, it will be a small change. If we can get the time zone in utc. But if we don't, then we have to do some weird, weird stuff that won't. Won't be. Won't be great.
Me: Yeah. We're gonna have to do some weird stuff. Call it now. But maybe. Maybe we can help.
Them: Yeah. Yeah, the cash. I actually don't know this. I feel like you're. You were on more of that.
Me: Yeah, it's just. It's managed.
Them: Than I was for the.
Me: It's managed by upsun and it's suboptimal.
Them: This stairwell. That's. That's not done. We didn't do any of that yet. Or from his hotspots. I imagine that there is still going to be some hotspots around. Project, but I feel like we're. We've done a pretty good job of, like, adding imagination.
Me: Better. I think the thing that worries me is, like, during launch, they, like, triple the server capacity. And they're paying for, like, whatever it was, and now.
Them: Yeah.
Me: I don't think they're gonna be paying anymore, so I'm assuming at some point we're go back down to what it was originally, so anyway. I think we've definitely gotten it under thumb control, but I don't know if that means.
Them: Yeah.
Me: That it's gonna fit in both size and paint.
Them: Yeah. Open search. I didn't do. I didn't work on that. But there is a. Is a Quran or. I'm sorry, a command for that, that.
Me: Yeah, that's. That's.
Them: Yeah.
Me: Another deploy or what? Ever. Yeah.
Them: I'm not sure about this trb section. I'm working through this this week. A lot of TRB stuff this week.
Me: What's status on that? Like, I know. Is that just like a sub site kind of thing? Is it kind of like ocga? Is it kind of like that?
Them: Reasonable. Yeah, I. I don't know. I was an on ocg, but it is like we're going to be pulling in some data from Aptify right now. I'm pulling in some committee and roster information. But in terms of like, in. In Napar, we have a TRB project and that will create a T or B, like, page, basically unit page. And then we're going to be. Anything that we get from Aptify will be pulled into that tier B page. Through, like, through some connections that we're going to. We're going to make. But the only kind of unknown there right now is there's a bunch of event information that. We will be getting from App Defy, but I'm not pulling it in at the moment because they're not ready for that. To be like, to move forward. So we'll get that in the. But it doesn't seem like it's, it's going to be too, too bad. Like, the, the, the information that we're getting mapped by is pretty, pretty, pretty minimal, and it's just going to be displaying committee cards and. Filtering grouping.
Me: 's good. That's good. Okay? Without the events. Yeah. Okay?
Them: Committee information, so it's. It's not. Not that. And I don't think there's right now any, any issues with the, the three levels of architecture for this. Once we we get the the kind of information from app defi mapped out. Which. Oh, that's another. Yeah. So I'm not sure on this. I wasn't doing. Joyce was doing a lot of the front end setup for these, for the blade components. I don't. I haven't ran into anything that, like, really stuck with me as, like, holy cow. Like, this is kind of a weird, weird component.
Me: Yeah, everything seems pretty clean to me. Let's just see if you saw anything. I think the. What's your feeling on swap?
Them: This. This swap. I feel like it's just been causing so much, like, weird, weird transition. Like. Like, I feel like I'll open a modal and then I'll be, like, back at a different page. And then, like, it just feels like it's, like, just kind of. Yeah. Just kind of weird.
Me: For nothing. But it's like, for what, though? And it also kills SEO or not.
Them: I know.
Me: It messes with SEO and it messes with analytics and all kinds of things and all kinds of issues.
Them: Yeah, I think it's just. Yeah, I. I don't like it. For this project. I mean, I've never used it before on. And I'm sure that for, like, some. Some sites, it's. It's great, but for, like, this size and complexity, I feel like it's.
Me: Yeah. Yeah, for, like a marketing. For a marketing site. Yeah. It's fine.
Them: Yeah.
Me: All right.
Them: Y. Eah.
Me: Binder. What's. What's going on? Binder? I know it's suboptimal in terms of the plan. They have no Talia, like, ping me on, but. Sounds like they don't. We're not getting assets in a. They're serving the assets in a way that's. Like I know Core web vitals really doesn't like. But what do you. Are you across that at all?
Them: Well, when we were integrating, I know that there was some back and forth on getting the. What is it? The. Dynamic asset trend transformations where you can.
Me: Yeah. Yeah. Like, it scales it to the dynamically, which seems like that should just be like, able stakes at this point, but you have to pay an extra $30,000 a month for that.
Them: Yeah. I know, I know. I know. Yeah. Quentin was pretty upset around, you know, around that. Yeah. And.
Me: He did. Asset manager. Oh, my God.
Them: Yeah, that. I mean, I haven't looked like Binder. Integration was one of the first things that I've did when. When. So I. I haven't looked at that in quite a while.
Me: This is reworking really? Well, nobody's. I mean, other than how the. You know. But the integration with the cms.
Them: Yeah, the front end kind of thing. Yeah.
Me: Great.
Them: Yeah, the only gotcha I think that I can think of is on in order to get. The. The integration for like the, the pop up I had to use. Well, I didn't have to use but like I used a livewire component for making sure for the upload functionality. So let's see here in local, if you go to media library and then you go to upload here where you upload. An image, and then there's, like, you know, progression and stuff like that. Then you can view it. That uses. Livewire and uses Alpine.
Me: Oh, wow. Oh. Cool.
Them: And so there is a yeah.
Me: Alpine js.
Them: It uses a. Let me think here. In. This is. Patches. This one. This one. So quill uses. Alpine. They include Alpine, and then they use it for this mask. Plugin. But I needed to. Have a different plugin for it. It. 's. Patches. Alpine. Import, import, import. Note. This is the patches. I don't remember. I think that, like, library ships with its own version of. Of Alpine, and it, like, has all the things that, like, Livewire needs in order to. Function. So in order for it to not conflict with the Twill Alpine, I needed to basically remove the Dwell Alpine and then have Livewire injected its own version of of Albion. So that's the only weird gotcha is this is because of being Alpine being included in Livewire's assets.
Me: Right. Right. Package. Yeah, I got it. I didn't know Alpine was so popular. That's cool. I guess it's like. Better than jquery. Cool. Scheduled jobs queue workers that are critical to understand.
Them: Yeah, I would just keep an eye on on Horizon. It seems like everything's running fairly, like, fine on schedule. I do have a ticket to change the. The timing because they're finding that when. What will happen is they'll have a. A release from NAP and they want to trigger job to update the publication. But it's coincides with when we're updating like projects or events. And so we're cycling through all the projects, which is putting the NAP update at the end of the queue and delaying the NEP update time. So. But, I mean, it's updating on the correct schedule. Now it seems like everything's running fast or running. Running well on that.
Me: So you're. You're going to update it so that naps higher up in the. Is that kind of the idea?
Them: No, no, I'm just going to. They've just requested that we just change the. The times because they have the. They release any P's at like our publication around 11:00 Eastern and so we're just moving. The Franz did not be at that time.
Me: Oh, God. Okay? Cool. Let's see, what else is there? Code base. These are more kind. I feel like we already talked about these a little bit. Like that. Everything's technical debt. Man.
Them: Yeah.
Me: This one. Yeah. I mean, yeah. Trying to think of, like, any sub website that I ever made of that doesn't have technical data.
Them: I mean.
Me: But. Yeah, sorry, go ahead.
Them: Oh, just one thing that. That I've, you know, felt the pain for a while is the. Just the. The. The whole pipeline of committing and having to run all those. It just seems so slow. Like, it really slows me down. Like when I. When I have, like, four tickets where it's just like, I know. Okay, this is. Each of these is just like a change in a single file, but, like, to switch into. Like create a branch and then have that branch, like commit to that branch. It's just like in order for that pre commit hook to. To run. It's. It's quite slow. So that's one area where I was like, man, if I had some time at the. Really optimize that a little bit better, that would be a huge quality of life improvement.
Me: You mean like an internal working method? Or is that what you're saying? Or are you saying more of.
Them: Yeah, just some. Just something that. A little bit faster. Right. Like, I think that when we run.
Me: Like.
Them: Like, the. The cleanup scripts for, like, Duster or Prettier that they run on the entire code base and not really on your stash files. It's slow. Like, it's. It's that, like, just to make it, you know, only run on dirty, then it would just make that whole process really a. Lot faster.
Me: Oh, the lenting. Yeah. Yeah. I'm pushing to. Have you seen this tool? I want to get us to adopt it. I keep saying this, but. We got to, like, update our. CI cd stuff. Anyway. I'm going to get rid of. Get rid of our linting and all that stuff and make it just AI. Yeah. Anyway, it's basically just like a resourcing tool for. It. It. It hides. You can host. You can self host, you can, but it just creates like, a nice interface, and then it. I don't know if it'll. It would replace lentine, but I think it would help with that stuff, make it a little smoother, but, yeah. The dev dev stuff is a little suboptimal.
Them: You'll have to check. Them.
Me: Anyway. Cool. All right. Well, I think this has been great. This has been really helpful. Is there anything else that, like you, comes to mind that you wanted to, like? Terms of. I don't know. There's so much here to talk about, but I don't know if there's anything else. That's.
Them: No, I think like, all the. The integrations are pretty. Like, they all follow the same patterns, like for the. The saloon. So I think that like, they're all very similar. So that's fine. Same with like, the commands and. And so getting data from Napor. Oh, we didn't go through the nap. Maybe. We'll do that one really quick because.
Me: S. I forgot about nap.
Them: That one's handled a little bit. You know, that's handled a little bit different. Where is it? Sync any.
Me: That'd be cool.
Them: P. Where is it? Sync. Oh, it's publications again. Sync publications. So this is another one of those things where. We created all this syncing. Back before market, like, created these new endpoints within the last, I think, month or something for making like, we could make this a lot nicer. But basically what we do is we have a get the current publications. So we have in services, we have these endpoints. So we have this crawl endpoint. And again, this is like a new endpoint that he added in the last, I think, five weeks or something. So this endpoint lists out all the, the different publications. And their last updated date. And then we can get information about the publication here. So this is an endpoint where we get the. The book and then like just book publication information. So in our sync script, we get the current publications, which is using that endpoint. Then we build out a dto, which is where is. Oh. This is okay. This is just going to trigger that job. So we use the. We use the this date, this last updated date to figure out when the like if there's publications that need to be updated. So then we'll build out a like a list of of applications to update and then we'll dispatch the the job for where is that? Get that. Carbon parts. Note that's not it. It's in here. It's sync publication. Yeah. So what? Dispatch a job to sync a publication if it matches the criteria that it has been updated since we last know, like no one about it. Or if we force a sync so a force will just update all of them. So in the sync application we get in this job gets the URL that meta data URL. So this URL is provided to this job. So from here we get the publication dto, so we get the the URL that was provided and then we just get the JSON from this this page we modify the JSON a little bit for passing it to this publication dto and then it builds out the the publication. Then we will. Update or create the publication. In our. In our database. Sync the relationship. So these are relationships that we get from the. From, like, the. The publication page. So, like, this page, it has, like, resources, videos, podcasts. That's all part of this function here where we get any of the division board's topics as well as. Oh, no, the. Yeah, so these are the the really relationships. And then the materials are below. So the, the podcast videos and resources. Those will be in the the resources. So, yeah, we sync the relationships, sync the materials. And then if the publication has display open book set to true. And we have like these, these formats HTML which we use where is it this get get publication format. So this will check to see if the publication list that it has like a GIF pages or X HTML pages. So if we get the.
Me: They're converting them, right? They're. Aren't they actively converting them? Is that. Or is that the reader?
Them: It's that it's been. It's been done. So they, they convert them to GIF from png. So like, now we only have to worry about gif. That was quite recently that we're just was able. I was able to clean up this, this script quite a bit recently. So we get. So then we download the the publication x HTML. So this we store the x HTML locally and then we will link out to the pages hosted on Nap for any of the the GIFs. But for if the if the they have display open book, then we download the the xhml. So here it's kind of complicated, like the. Because we have to also look through the source and get images, stuff like that. But, like, we'll get the chapters, get the pages, and then we'll figure out if the page exists. And then we've downloaded the pages and the process the pages. So when we process the page, that's. When we look for any of the assets. So this is like, image. Some publications have their own css, so we need to also, like, get that out and download that.
Me: Got it. God. I got it. Yeah.
Them: So that's what this does for for those.
Me: Did the reader. I mean, that was designed and built, or was that part of. Was that, like, a package that we use? Just curious.
Them: The reader was done. It was already hosted on np. So it's a code that Mark had developed over the course of whatever, 10, 15 years that we kind of packaged up. We pulled in, converted it from, like, twig to blade, made it into, you know, controllers and kind of, yeah, took the existing functionality and. And. Kind of slotted it into Laravel app.
Me: Got it. Oh, that's cool. So it's just repurposing the work market. Done. Oh, that's cool. I didn't know that. That's full. Nice. Kind of thing. I feel like that's. That's good. That's a good overview. My dog is, like, flipping out. He wants to. Really wants to go out. Like, you've been talking too much.
Them: Yeah.
Me: And take me outside. But, no, this has been really helpful, and you've been so great, Anthony. Thank you so much. And, yeah, this. This project definitely. Wouldn't have been as successful without you, so we appreciate it.
Them: Yeah, it's been. It's been fun.
Me: That's a word for it.
Them: Yeah.
Me: But no, it's. It's definitely one. I'm telling my grandkids like I did. I did Napar.
Them: Yeah. It was. It's neat to see it in now live and. Yeah. Out in the wild.
Me: So cool. All right, well, I'll see you. I'll see you on slack. And I appreciate this. I really appreciate your time. Thank you. Thanks again.
Them: Yeah, there is.
Me: All right, talk to you soon.
Them: All right, Take care.
