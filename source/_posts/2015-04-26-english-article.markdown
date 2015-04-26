---
layout: post
title: "English article"
date: 2015-04-26 16:32:51 +0700
comments: true
categories: 
---
When building a game, often there is much more to it than simply building the game mechanics.

There are many different types of games that can easily be built with a framework of choice. From tic-tac-toe to Magic The Gathering, there are a ton of different games that can be built with Angular. Card games, trivia games, board games, mobile hide-and-seek, etc. can be built using raw, unoptimized AngularJS.

Think about the last time you were in an Applebee’s (a chain restaurant popular in the US) and there was an interactive trivia game on the different TVs. Using a single-page-app (SPA), it can be built in an afternoon. With CSS3/HTML5, we don’t even need fancy animation libraries as 2D and 3D can be performed using only native web elements.

For instance, to run a 3D wipe of an element, we can apply CSS3 to it. Then, when we are ready for the element to transition, we can simply apply the CSS class.

What about building DOM-heavy games? Isn’t Angular really poor at handling LOTS of run-time DOM manipulations? It can be. Due to the way Angular 1.x runs, it has it’s own event handler, which adds overhead to the DOM and building any heavy pixel-heavy games can be painful. Because of the extra event loop, building a DOM-manipulation-based game in only Angular may not be the best approach.

However, there are many other components to building a game, for instance, most (if not all) games have scoreboards. There are HUDS (heads up displays), chat messages, event feeds, multiplayer stats, high scoreboards. How about game invitations, providing a pay-wall to guarentee a player has access to play premium content?

These are all elements that game libraries are not optimized to provide and can be tricky & complex to build. On the other hand, web application libraries such as angular are great at building these components.

While game libraries are great at handling physics, animation, and sounds, we’ll use angular to power the container.

In today’s post, we are looking at how to build the eco-system of a game using angular as the vehicle to deliver the game content, node/express to power the game’s back-end, phaser.io and socket.io to connect the two in real-time.

The game flow looks like the following: