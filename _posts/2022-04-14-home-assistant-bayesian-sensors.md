---
layout: post
title:  "A Deep Dive Into Bayesian Sensors For Home Assistant!"
excerpt_separator: <!--more-->
categories: [Home Assistant]
tags: [home automation, sensor, DIY]
---

The Bayesian Sensor is a great option that is underused in Home Assistant. This sensor is based on the likelihood of an event occurring based on prior knowledge of elements that may be connected with said event.
<!--more-->
&nbsp;

{% include youtube.html id='oDWQCJbBrKE' %}

## Background

Bayes' theorem, or the Bayesian Sensor in our case, is a concept in probability theory and statistics named after Thomas Bayes that describes the likelihood of an event occurring based on prior knowledge of elements that may be connected with said event. We're using Bayesian inference for the Home Assistant integration, which is a statistical inference method that leverages Bayes' theorem to update the probability of an occurrence as new data or information becomes available.

Start with the wiki page if you want to learn more; that's where I started, and besides I'd be doing you a disservice if I went any farther into the background of this topic. Also, this specific integration was released so long ago, on September 9, 2017, and it's only used by 625 active installations at the time of filming, I mean come on, this is a powerful integration that almost no one is using. And yes, I understand that this number may be skewed because not everyone shares anonymous information with the Home Assistant team, and maybe it is representative of the number of people using it, but that's still a pretty low number in my opinion.

It is for reasons like these that we should all be sharing our data with the team, which I believe is a minor inconvenience given that this software is open source!; Otherwise, they may stop maintaining low-use integrations or remove them completely and we wouldn’t want a great integration like this to be removed!
  
&nbsp;

## Configuration

So, how can we take advantage of this integration I’m referring to? That's an excellent question. To begin using this powerful integration, we simply need to add a few lines to our configuration.yaml file, that’s it, easy right? Well, it really is that simple, but let us first understand some of the variables.

So, the first thing we will do after we open VS Code, or however you edit your yaml files is to open the Home Assistant web page then open ‘Binary Sensors' from the integrations page and click on Bayesian. Then we scroll down a little to the section called “Configuration Variables”, here it lists all the required variables we need. Starting from the top and working our way down, the first variable we see is “prior”, this is the starting probability for our event, weighted based on the likelihood of this event happening without outside influence, i.e. the sun rising verus a light turning on.

Don't worry about the weights for these variables right now; we'll get to them later, and I'll share a tool with you that will make it a lot easier. Moving on, we have the probability threshold, which defaults to 0.5 unless we change it, and tells Home Assistant when it may switch on our bayesian sensor. Finally, we have the name for our sensor, which I prefer to use because we'll be utilizing it for some more complex automations.

Okay, now comes the real strength of this integration: the observations, and you'll repeat these steps for each additional condition you add, as we'll see in the example. First, we must declare the platform we will be using, which can be one of three types: state, numeric state, or template. They provide us three full examples to demonstrate how these function below, but after we decide which platform to use, the next one is entity ID, which is the entity we are monitoring for a change if we chose state or numeric state.

If we're using a template, the value template comes next, and this is where you define the template parameters. The probability given true is then required and simply means that this will be the new probability if it is active, followed by the probability given false, which defaults to 1 minus the probability given true unless we want to weight it differently, and finally the to state, which is used to monitor state change when using state or numeric state.

&nbsp;

## Example
