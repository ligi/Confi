# Confi Concept and Context

For the	[33C3](https://events.ccc.de/congress/2016/wiki/Main_Page) I was adapting [tuxmobils FahrPlan application](http://github.com/tuxmobil/campfahrplan) to the 33C3 as he did not want to do it this year like he did in the years before. At this point I want to thank him for all his work on this application over the years! I have seen some talks that where really important to me and I might have missed otherwise.
In the process of adapting the application I used the aggregated schedule data from [c3voc](https://c3voc.de) because I want to attend more sessions that are not in the main halls. The applications in the main halls are recorded and I can enjoy at home in a calm mindset and do not have to waste precious conference time. I got great feedback about this and attended more sessions outside the main schedule than ever before.
For the	34C3 I want to write a new application from scratch as I have some Ideas that are really hard to retro-fit into the old application architecture. A rewrite from scratch will be faster and more fun. Here I will collect some ideas and corner-stones.

## Multi-phase Conference

The Conference has multiple phases:

 * conference preparation ( [HalfNarp](http://halfnarp.events.ccc.de) / [SCR](https://github.com/ligi/SCR) )
 * attending the conference ( TimeLine / notifications / favorites .. )
 * post-processing the conference ( recordings / feedback )

This should not be reflected via different applications like it is implemented right now. This gets rid of the the overhead of data-sharing between the applications and provides a way better user experience.

## Use RecyclerView for the TimeLine

Adding all the other tracks did not only have these nice advantages. It on the other side made the application really slow in some cases. Especially to the conclusion of the congress when more and more sessions where added. I think by using a RecyclerView ( at least the concept if not even the implementation from AppCompat) here - we can get speed even while we have to deal with a lot of sessions.

## Fine grain system to mark interest

Interest in a talk is not a yes/no thing. There are talks you do not want to miss and there are talks that you would like to see but won't leave some interesting situation for this. This should be reflected in the system.
For recording interest we will use data from the HalfNarp and additional user-input at the conference. We will have to boil down data hard - adding all the sessions made it really difficult to get the overview. To make this a bit better we will use the data from the preparation phase a bit more. If you say at preparation for the conflict resolution in which talk you are not interested in you shall not see it in the TimeLine at the conference and clutter your view.

## Continuous TimeLine

The event is one continuous TimeLine. I always hated switching between days. Different attendees have different biorhythms - especially at a chaos event. The current point in time should be clearly marked but there should be no segmentation by day.

## Collapsing ToolBar

The application should use a collapsing ToolBar ( using the RecyclerView is a good groundwork for this )
Tis gives more screen real estate to relevant information.

## Sync Favorites

The application should contain the ability to Sync Favorites between your own devices and if wanted with other people. There could be a conference following so I see the talks highlighted that people I follow have marked interest in. This should be detached from social networks and have privacy and decentralisation in mind.

## More sources for the TimeLine

I found myself often switching between the EngelSystem and the schedule application. This required a high mental load that I think can be removed up by integrating one interface to the EngelSystem. Also other sources for alternative TimeLine input are possible ( e.g. a system for coordinating meeting with other participants in times that work for you )

## Expert-Free setup and update

Currently to adopt the application to a Congress you have to have expert knowledge. You need to create a flavor and compile the application. Without knowledge of code in general and android in particular this would not work for humans that do not have these skills. Inspired by the 33C3 closing ceremony I want that even physicists can have a chaotic event ;-)

## Integration in the ticket-system

A lot of people do not know that there is an application for the conference in the first place. The rate might be higher at a chaos conference but still there where participants without this knowledge. I want a pointer from the [esPass](http://espass.it) to the application so more people find the application without having to poll a application-store they miss trust the least.
The solution I have in mind currently is that when you setup your conference in [pretix](https://github.com/pretix): you specify a pointer to the conference data that then ends up in confi offering you guidance through the conference.

## Kotlin

I will use [Kotlin](https://kotlinlang.org) to write this application from day #0. Especially all the functional concepts of Kotlin will help to make a nice application - not only on the outside. Also I want to have fun while coding - so Kotlin it is.

## Post-processing the conference

Currently there is no application to properly post-process the conference at all. We can use all the data that aggregated in the preparation and attending phase. I imagine this so I can come back home - give into gravity - and all the recordings of the talks I marked interest in are automagically replayed on my big-screen of choice. This then also keeps track of what you have watched and helps giving feedback. We might even try out some automatic feedback here. So when you watch a talk until the very end this is taken as feedback for [frab](http://frab.github.io/frab) and can be used the next years. Non-positive feedback should be avoided as switching off the talk after like 5 minutes could mean that the talk is bad - but it can also mean that some real-world interrupt happened and the talk is actually pretty good.

---

This document is intended to get early feedback before the implementation phase - please let me know what would work for you!
