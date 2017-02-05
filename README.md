# Confi Concept and Context

For the	[33C3](https://events.ccc.de/congress/2016/wiki/Main_Page) I was adapting [tuxmobil's FahrPlan application](http://github.com/tuxmobil/campfahrplan) to the 33C3 as he did not want to do it this year like he did in the years before. At this point I want to thank him for all his work on this application over the years! I have seen some talks that were really important to me and I might have missed otherwise.
In the process of adapting the application I used the aggregated schedule data from [c3voc](https://c3voc.de) because I want to attend more sessions that are not in the main halls. The presentations in the main halls are recorded and I can enjoy them at home in a calm mindset and do not have to waste precious conference time. I got great feedback about this and attended more sessions outside the main schedule than ever before.
For the	34C3 I want to write a new application from scratch as I have some ideas that are really hard to retro-fit into the old application architecture. A rewrite from scratch will be faster and more fun. Here I will collect some ideas and corner-stones.

## Multi-phase conference

The conference has multiple phases:

 * Conference preparation ( [HalfNarp](http://halfnarp.events.ccc.de) / [SCR](https://github.com/ligi/SCR) )
 * Attending the conference ( timeline / notifications / favorites .. )
 * Post-processing the conference ( recordings / feedback )

This should not be reflected via different applications like it is implemented right now. This gets rid of the overhead of data-sharing between the applications and provides a way better user experience.

## Use RecyclerView for the timeline

Adding all the other tracks did not only have these nice advantages. It on the other side made the application really slow in some cases. Especially to the conclusion of the congress when more and more sessions where added. I think by using a RecyclerView ( at least the concept if not even the implementation from AppCompat) here - we can get speed even while we have to deal with a lot of sessions.

## Fine grain system to mark interest

Interest in a talk is not a yes/no thing. There are talks you do not want to miss and there are talks that you would like to see but won't leave some interesting situation for this. This should be reflected in the system.
For recording interest we will use data from the HalfNarp and additional user input at the conference. We will have to boil down data hard - adding all the sessions made it really difficult to get the overview. To make this a bit better we will use the data from the preparation phase a bit more. If you say at preparation for the conflict resolution in which talk you are not interested in you shall not see it in the timeline at the conference and clutter your view.

## Continuous timeline

The event is one continuous timeline. I always hated switching between days. Different attendees have different biorhythms - especially at a chaos event. The current point in time should be clearly marked but there should be no segmentation by day.

## Collapsing ToolBar

The application should use a collapsing ToolBar ( using the RecyclerView is a good groundwork for this )
This gives more screen real estate to relevant information.

## Change management

It is quite common that the schedule of the conference changes before and while it is happening. The application must be able to load a new version of the conference schedule. Changes must be presented to the user in a suitable way. Changes include cancelation, location change, time change, speaker change or content related changes such as a new title or description, ... The user should be able to choose which changes she wants to see. The following filters might be useful: "only changes affecting favorites", "only events of the future".

## Sync favorites

The application should contain the ability to sync favorites between your own devices and if wanted with other people. There could be a conference following so I see the talks highlighted that people I follow have marked interest in. This should be detached from social networks and have privacy and decentralisation in mind.

## More sources for the timeline

I found myself often switching between the EngelSystem and the schedule application. This required a high mental load that I think can be removed by integrating one interface to the EngelSystem. Also other sources for alternative timeline input are possible ( e.g. a system for coordinating meeting with other participants in times that work for you )

## Expert-Free setup and update

Currently to adopt the application to a Congress you have to have expert knowledge. You need to create a flavor and compile the application. Without knowledge of code in general and Android in particular this would not work for humans that do not have these skills. Inspired by the 33C3 closing ceremony I want that even physicists can have a chaotic event ;-)

## Integration in the ticket system

A lot of people do not know that there is an application for the conference in the first place. The rate might be higher at a chaos conference but still there where participants without this knowledge. I want a pointer from the [esPass](http://espass.it) to the application so more people find the application without having to poll a application store they mistrust the least.
The solution I have in mind, currently is, that when you setup your conference in [pretix](https://github.com/pretix): you specify a pointer to the conference data that then ends up in confi offering you guidance through the conference.

## Kotlin

I will use [Kotlin](https://kotlinlang.org) to write this application from day #0. Especially all the functional concepts of Kotlin will help to make a nice application - not only on the outside. Also I want to have fun while coding - so Kotlin it is.

## Post-processing the conference

Currently there is no application to properly post-process the conference at all. We can use all the data that was aggregated in the preparation and attending phase. I imagine this so I can come back home - give into gravity - and all the recordings of the talks I marked interest in are automagically replayed on my big-screen of choice. This then also keeps track of what you have watched and helps giving feedback. We might even try out some automatic feedback here. So when you watch a talk until the very end this is taken as feedback for [frab](http://frab.github.io/frab) and can be used the next years. Non-positive feedback should be avoided as switching off the talk after like 5 minutes could mean that the talk is bad - but it can also mean that some real-world interrupt happened and the talk is actually pretty good.

---

This document is intended to get early feedback before the implementation phase - please let me know what would work for you!
