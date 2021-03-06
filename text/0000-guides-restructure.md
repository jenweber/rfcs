- Start Date: (fill me in with today's date, YYYY-MM-DD)
- RFC PR: (leave this empty)
- Ember Issue: (leave this empty)

# Restructuring the Guides Table of Contents

## Summary

As our favorite framework has grown and changed a lot over the past few years, so have our [Ember.js Guides](https://guides.emberjs.com)! This project aims to use the excellent work that has been done by hundreds of contributors and arrange it in a way that provides a natural learning flow for today’s Ember.js developers.

## Motivation

The current structure and flow of the guides reflects the past, not the present experience for Ember developers. It’s time to fix that. With Octane coming down the line, and an influx of new Ember developers, it’s more important than ever to consider the overall learning experience.

At the time the Guides were originally written, things like object-oriented programming in JavaScript, components, routing, and SPAs in general were new ideas. If you look at our guides today, they start by teaching the “Ember Objects” programming concept, in a way that few beginners will use in their apps. However, this made sense at the time, because it would have been so unfamiliar to developers. Now, the learning hierarchy needs have shifted from “learn these new concepts” to “learn how the familiar pieces fit together so you can build quickly.”

## Detailed design

The focus of this RFC is not to write new content, but make better use of what is already there by presenting it in a different order. We aim to rearrange the table of contents without breaking any URLs, with refactors necessary to fix the transitions between topics, and with the minimal _new_ content needed to teach Octane. We take care to not make it look like there is “more to learn.”

The overall learning strategy is to establish a common core of sequential knowledge, and then later topics can be read standalone, skipping around. What this means is that if beginners read through to routes, they could skip around the topics lower down the chain successfully.

Finally, it is important to acknowlegde that the Guides are intended to represent the "Happy Path" of using Ember. It is not possible to have something that is a perfect fit for everyone's app needs, nor should it cover our entire API surface.

### Process and preparation

This Table of Contents plan was developed over the course of many months, meetings, and writing sessions. It includes input from many people in the community. Here are the sources of inspiration, information, and planning:

- Chris Garrett's ([@pzuraq](https://github.com/pzuraq)) 2018 Roadmap Blog Post, [Ember as a Component-Service Framework](https://medium.com/@pzuraq/emberjs-2018-ember-as-a-component-service-framework-2e49492734f1), May 2018
- My own Roadmap blog post reflections, [Be loud and be ready](https://gist.github.com/jenweber/a9fbea98478fc3841fb8b24f7dc961c8), May 2018
- Extensive discussion in Ember Learning Team Meetings, which are held weekly and open to the public
- The [2018 Roadmap RFC](https://github.com/emberjs/rfcs/blob/26c4d83fb66568e1087a05818fb39a307ebf8da8/text/0000-roadmap-2018.md) by [Tom Dale](https://github.com/tomdale)
- The Octane Strike Team meetings and followup conversations
- Ember.js Framework Core Team meetings
- A [Twitter poll](https://twitter.com/jwwweber/status/1081352702083452928), "Name two things you think the guides should do well/better"
- Discussion on Discord of the initial Table of Contents draft with some key contributors and content creators
- [Dan Monroe](https://github.com/cah-danmonroe)'s trailblazing work to [convert the Guides to use Angle Brackets](https://github.com/ember-learn/guides-source/pull/357)
- Countless hours of Q&A on Stack Overflow and Discord
- Experience training new Ember developers in-house
- Public Ember 101 workshops run in Boston, Massachusetts, USA
- Studying the guides and tutorials of other JavaScript libraries
- The successful restructure and rewrite of the [Ember CLI Guides](https://cli.emberjs.com) (a far more drastic project than this RFC aims to be)
- Attempting to reorder the Guides in a branch, as an experiment

### Table of Contents

This is the aspirational version. There will be many intermediate states between here and there, outlined later in this RFC.

**Core Concepts**

- What is Ember?
- Getting Started
- Anatomy of an app (future new content)

**Fundamentals**

- Template syntax
- Working with JavaScript
- Components
- Routing (includes Routes, Router, and Controllers)
- State management (aka computed properties)
- Services

**Leveling up**

- Template helpers
- Data management (future new content that references separate Ember Data guides)
- Addons and dependencies
- Testing
- Configuration
- Deploying
- Upgrading
- Debugging (currently named Ember Inspector)

### Topic naming

As much as possible, we aim for the topics to be named after their general web development concepts, and not the Ember-specific implementation of them.

### Logic for ordering and grouping

In this section, we will cover why this order and grouping is being proposed.

#### Groupings

Groupings are added for the benefit of new learners. It breaks up the content visually and gives them a clue about which sections to pay the most attention to.

Just because something is included in "Leveling up" does not automatically make it an "advanced" topic. The main logic for the division between "Fundamentals" and "Leveling up" is the following test: Can someone ignore this section and still use Ember effectively? Can it be learned in any order if someone knows the basics? If so, it goes in "Leveling up." Another test is this: "Does someone need prior knowledge of another topic in order to understand this section? Which topic?" Topics that are important prior knowledge should generally go in "Fundamentals."

#### Templates & Template helpers

Templates come before components, since it is possible for someone to not know JavaScript/Handlebars and still contribute to Ember. For example, designers could effectively work in only templates, using plain HTML. To make Templates work as the opening topic, additions are necessary in the introduction.

Template Syntax will cover Handlebars basics and built-in features like `{{input}}`, `{{#each}}`, and `{{#if}}`.

Template helpers are split out and moved to "Leveling Up" because developers do not need to use them to write basic Ember apps (they are not a prerequisite). This section includes writing custom Helpers and using built-in helpers like `get`, `let`, and `array`. Although helpers themselves are not considered a difficult topic, they are used most often when developers understand their app's architecture and the flow of data. Also, template helpers have more in common with JavaScript functions than concerns relating to layout and data flow.

Lastly, another reason to split out Template syntax from Template Helpers is because the syntax section is expected to expand with the addition of Octane content.

An alternative to this split is to reduce the documentation of helpers themselves in the Guides, and lean on the API docs instead, however great care should be taken in removing documentation. Without a strong case for it, we lean towards leaving them in the Guides.

#### Working with JavaScript

A common concern of new learners is, what is JavaScript and what is special to Ember? The Working with JavaScript section incorporates the existing JavaScript Primer and new content that will help make the distinctions clearer. Ember.js has procatively adopted JavaScript APIs as they become available, such as Classes and Decorators, in some cases before the larger JavaScript community becomes familiar with them. Key people in the Ember Community are also involved in the development of JavaScript itself through TC39. To an extent, it is our responsibility to at least suggest to developers which JavaScript concepts they must learn in order to feel comfortable with Ember.

#### Components

Components will need the most refactor work and new content for Octane, so here’s the subtopic breakdown:

- Creating a component (includes Component Types post-Octane)
- Displaying data in a Template
- Adding actions
- Nesting components (includes suggestions of when to break things into components)
- Passing arguments
- Using computed properties (extremely basic example, link to the Computed Property section)
- Working with arrays of data
- Lifecycle hooks

#### State management

The State Management section is important because whether "computed properties" are available in their current state or as Decorators, the nunances must be within easy reach for existing Ember developers and future learners. We rename this topic in alignment with the Topic Naming convention mentioned above.

#### Routing

This RFC proposes grouping Routes, Routing, and Controllers under the same topic heading.

If that sounds like a lot, it's because it is. "Routing" is a responsibility that is divided into many pieces:

- the route declarations in `router.js`, including dynamic segments
- the Handlebars route template, the middleman for passing data from the controller to components
- the Route JavaScript file, which contains the model hook for fetching data and Transition rules in the form of hooks. The model hook receives the query params that are defined in the Controller
- Controllers, which hold the results of the model hook, actions and other attributes that need to be passed to child components, and query param definitions.

Common beginner mistakes are to define actions and attributes in a Route and try to pass them to components, plus attempts to access the result of the model hook in functions in the route JavaScript. Beginners think of Routes as "special components" and are surprised by their limitations. This becomes a long-lived pain point if developers hand off the controller's responsibilities to Components.

For better or for worse, there's a mental-model codependency between Routes and Controllers that is unlikely to change in the near term. Our Guides should reflect the best possible learning experience for today's constraints, rather than be a reflection of the codebase architecture. By grouping these topics together, we have an opportunity to heal confusion over Controllers and help new developers avoid unexpected pitfalls.

Based on initial feedback, this grouping is the most divisive part of the proposal. This grouping is informed by reflecting on how one might teach Controllers to a new developer, while working together in person. In order to reach consensus, any objections to the grouping should suggest solutions that include an explanation of how and where one would teach Routes, actions, routing with Query params, and passing arguments to the model hook.

#### Services

The Services documentation is currently sparse, but it is included in "Fundamentals" for two reasons. First, an understanding of Services is a prerequisite for understanding Ember Data's store service. Second, the Router service is not well known by new developers, as it is solely found in the API documentation, and it provides behavior that new developers expect to have. Third, the popularity of the mental model of Ember as a Components-Services framework is a signal that this may be an effective teaching strategy.

#### Ember Data

Ember Data will be gradually extracted into its own Guides. 2-3 years ago, there was a push to provide better official documentation of Ember Data, as a "first class citizen." It was intermingled with the rest of the Ember.js Guides as a result. We will continue to treat Ember Data as a first class citizen, yet with improved separation of concerns similar to the approach to Ember CLI Guides. Ultimately, the content in other Guides topics will be refactored to show both Ember Data and non-Ember Data approaches, in an effort to lower the perceived cognitive overhead of Ember.

This change reflects the overall drive of the JavaScript Ecosystem towards interchangeable, composable parts.

The Ember Data team is especially requested to review this shift and provide feedback.

#### Deploying and Upgrading

These sections have some existing content. They will aim to _not_ duplicate the contents of the CLI Guides, but rather reference content found there. They are included in the top-level Table of Contents for two readons, discoverability and to showcase Ember's strengths

#### Ember Inspector

Although the Ember.js Guides are versioned, the Inspector Guides do not need to follow the same versioning strategy. It would be reasonable to separate them out into their own, unversioned Guides. However the content is quite stable and therefore lower priority than other refactors.

The Ember Inspector team is requested to consider whether naming the section "Debugging" would improve discoverability of Ember Inspector for new developers, and whether the eventual unversioned separation aligns with expected technical development.

#### Unchanged topics

Configuration, Testing, and Addons & Dependencies remain unchanged in their approach.

#### Removals

Notably missing is Ember Object Model. This is on purpose. It will be pulled into other sections, in a “show, don’t tell” kind of approach. Also removed is "Application Concerns," which are separated into their appropriate alternate subtopics.

### Why doesn’t this RFC include rewriting content?
Individual pages have already been refactored over the past two years by many contributors. Examples include the Ember Objects page, Controllers, using third party libraries, and explanations of data management. Many of the pain points that current Ember devs remember from their early days have been fixed. For example, it’s clear that Ember Data/JSONAPI aren’t mandatory, that you *can* use things like fetch, that Computed Properties need to be consumed for them to fire… we’re in a pretty good place! If we choose a good structure for the Table of Contents, it will make it much easier to write/rewrite individual sections.

### Improving the learning story

Octane’s planned introduction of Angle Brackets, decorators, Glimmer components, and more mean that we need an easy way for past Ember devs to onboard. The Components and Templates API is the most heavily affected (for the better, but people will still need to study them).

One of the most common points of confusion for new devs has become “how do the pieces fit together?” The Super Rentals tutorial covers the bases well for using the CLI and adding basic interactions. Anecdotally, thanks to the tutorial, it seems that the main remaining questions are mostly architectural. The faster we can get the “Mental Model” of Ember across, the better.

### Technical approach

Thanks to Chris Manson’s work ([@real_ate aka @mansona](https://github.com/mansona)) on the Guides app architecture, we can move content around while preserving existing links! The Table of Contents specified in the `pages.yml` file of guides-source can have any paths, and is not 100% dependent on the physical file structure to create URLs. It is very important that we don’t break existing blog articles, community tutorials, Stack Overflow answers, etc, both for user experience and SEO reasons.

All guides content is markdown. When we rearrange content, we’ll have to fix the links. However there are tests in place that check for bad links, so we can do this confidently.

## How we teach this

Community buy-in is important to reduce perception of churn and encourage perception of “leveling up” our resources. Significant efforts will be put towards informing the community of upcoming changes, and giving them the opportunity to participate.

We will also test an early beta restructuring with beginner-level developers and developers who don’t know Ember. Although the rollout for the live site will take months, a rough cut, undeployed, could be completed in 1-2 weeks. It could serve as a North Star for the work to be done.

### Implementation plan
This work will need to be done over many months/the next year, and will be done incrementally in the deployed guides. The plan prioritizes the refactors that will make Octane Guides writing easier. It will be communicated in the form of Quest issues, with help requested via the Ember Times, Discord, Discuss, etc.

1. Settle on a Table of Contents layout*
2. Make the refactors necessary for Components to come before Templates*
3. Switch the order in the live Guides*
4. Work Computed Properties into the Components section*
5. Create an Upgrading section (this will house the Octane conversion guide)*
6. Write What is Ember. This will be where we give a light intro into how the pieces fit together, and link to CLI guides resources on the file structure*
7. Make the refactors necessary to add Controllers into the Routes explanations
8. Group Controllers with Routes in the live Guides
9. Make Services its own topic
10. Rename “Glossary” to “JavaScript concepts” and move the JS Primer there
11. Create Deploying section. Low on content, links to CLI Guides resources.
12. Create Styles section. Low on content, links to CLI Guides resources.
13. Rename Models to “Connecting to an API”

*must be done before the first Octane edition release

## Drawbacks

This refactor is biased towards new user experience, so existing Ember users could experience the most drawbacks.

1. The will need to discover where old content lives → mitigated by the site search, which is now stabilized
2. Experienced developers who haven’t looked at the Guides for a long time will all reference it during the Octane upgrade, and may be surprised to find a new layout. It’s another “new thing to learn” → mitigated by consolidating most of the new things to learn into the Components section
3. There will likely be some wrinkles to iron out with regards to content that should have been refactored during rearranging, but was overlooked → we know that the community will help identify these issues, thanks to the awesome response to the CLI docs refactor in 2018

## Alternatives

The main architectural pattern choices were as follows:

1. On one extreme, make every section standalone
2. The middle ground, establish a “Common Core” to be read sequentially, and then have standalone sections that rely on knowledge of the core
3. The other extreme, make the entire guides sequential

We choose the middle ground, because it requires the least new writing, and if we chose to move towards one of the other extremes, it does not prevent that choice nor would we throw away work.

It’s also useful to study the learning flow of other front end libraries in order to determine possible alternatives. Let’s look at a few.

### React
React is known for having low learning overhead for someone who is making their first app. With its popularity, we can guess that new users may expect to find similar topics easily accessible in our guides. This list is most useful for considering what should be in our Components section.

1. Hello World
2. Introducing JSX
3. Rendering Elements
4. Components and Props
5. State and Lifecycle
6. Handling Events
7. Conditional Rendering
8. Lists and Keys
9. Forms
    1. Lifting State Up
    2. Composition vs Inheritance
    3. Thinking In React

The Overview section of the React Tutorial also helps show what we may be missing:

- What Is React?
- Inspecting the Starter Code
- Passing Data Through Props
- Making an Interactive Component
- Developer Tools

Nowhere on our current site do we have a highly visible explanation of what Ember is, beyond snippets. In light of this glaring omission, we have added a “What is Ember” section to the Guides Table of Contents above. It is not meant to replace the ongoing “Why Ember” and marketing-focused descriptions that are underway.

### Vue
As a fully-featured framework, Vue is an easier comparison for possible Table of Contents listings. Keep in mind that much of this type of content is present in our CLI docs instead, so this list will look longer than what we are aiming for.

Introduction
What is Vue.js?
Getting Started
Declarative Rendering
Conditionals and Loops
Handling User Input
Composing with Components
Relation to Custom Elements
Ready for More?
The Vue Instance
Template Syntax
Computed Properties and Watchers
Class and Style Bindings
Conditional Rendering
List Rendering
Event Handling
Form Input Bindings
Components Basics
Components In-Depth
Component Registration
Props
Custom Events
Slots
Dynamic & Async Components
Handling Edge Cases
Transitions & Animation
Enter/Leave & List Transitions
State Transitions
Reusability & Composition
Mixins
Custom Directives
Render Functions & JSX
Plugins
Filters
Tooling
Single File Components
Unit Testing
TypeScript Support
Production Deployment
Scaling Up
Routing
State Management
Server-Side Rendering
Internals
Reactivity in Depth
Migrating
Migration from Vue 1.x
Migration from Vue Router 0.7.x
Migration from Vuex 0.6.x to 1.0
Meta
Comparison with Other Frameworks
Join the Vue.js Community!
Meet the Team

One possible lesson here is that we could split up Components like Vue did with Component Basics and Components In-Depth. Their dedicated section on Computed Properties inspired the inclusion in our new Table of Contents.

### Angular
Angular is also a full-featured framework that has a lot in common with Ember.

FUNDAMENTALS
Architecture

  Architecture Overview
  Intro to Modules
  Intro to Components
  Intro to Services and DI
  Next Steps

Components & Templates

  Displaying Data
  Template Syntax
  User Input
  Lifecycle Hooks
  Component Interaction
  Component Styles
  Angular Elements
  Dynamic Components
  Attribute Directives
  Structural Directives
  Pipes

Forms
Observables & RxJS
Bootstrapping
NgModules
Dependency Injection
HttpClient
Routing & Navigation
Animations

SETUP & DEPLOYMENT
Project File Structure
Workspace Configuration
npm Dependencies
TypeScript Configuration
Ahead-of-Time Compilation
Building & Serving
Testing
Deployment
Browser Support
Dev Tool Integration

Angular is the closest match to our current guides structure. Notably, they work Styles in as part of their Components section.

### Trends

All three of the libraries above cover forms in their own dedicated section. They also cover styles and animation, which we do not cover at all. These are all good candidates for future guides.

## Unresolved questions

- What does the community think of this structure? How can it be improved?
- Is it good for new learners? Is it good for existing users?
- What possible pain points does the community see?
- Are there any areas missing from the Table of Contents?
- What do people think of removing the “Ember Object Model” section?
