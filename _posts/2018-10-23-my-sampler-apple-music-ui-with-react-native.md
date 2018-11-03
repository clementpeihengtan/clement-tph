---
layout: post
title:  "My Sampler - Apple Music Redesigned wiht React Native"
date:   2018-10-23
categories: mediator feature
image: /assets/article_images/2018-10-23-my-sampler-apple-music-ui-with-react-native/apple-music-background-web.png
---

As a developer, I am inspired when I discover creative designs that helps to solve real world problem. 

## Caught my Attention

Recently I have been actively studying and reading articles related to UI/UX design at [medium]('https://uxdesign.cc/'), I came across this interesting [article](https://medium.com/startup-grind/i-got-rejected-by-apple-music-so-i-redesigned-it-b7e2e4dc64bf).
The author, [Jason Yuan](https://jasonyuan.design/) carried out an unsolicited redesign of apple music. He pointed out a lots of suggestion and provided samples of new apple music designs that are simple and yet intriguing. 


## My Sampler

One of the feature, I would love to talk about is the My Sampler feature. This feature really caught my attention, because it addressed and solved the problem of how different type of people explore their music preferences in a creative way. 

## Why not make it a real product? 

Being an inquisitive developers, I would like to make this a real feature that can be used by people. 

> “There are many things that seem impossible only so long as one does not attempt them.” 
― André Gide, Autumn Leaves

I gave it a try. 

## Aim 
This project allows me to further enhance my understanding about react-native especially react native animation which is a powerful tools that allows the creation of fun and splendid user interface. 

## Analyze

On first load, we see the image of the artist, name of the artist and the name of the song as below

![](/assets/article_images/2018-10-23-my-sampler-apple-music-ui-with-react-native/apple-music-my-sampler.png)

There are a few things happen when the image is touched and hold

![](/assets/article_images/2018-10-23-my-sampler-apple-music-ui-with-react-native/apple-music-my-sampler-start-animation.png)

 - The image enlarged.
 - A 'spinner' like thing started to spin ina clockwise manner
 - The '+' and 'x' sign expand from the center and fade in through translation from the y-axis
 - The background become blurred.

 All these happen at the same time. Here we can make our choices by swiping the circle down or up to the '+' or 'x' sign.

## Work In Progress

When I am working on this project, I faced a couple of challenges.

1. There are no react native library that provides the spinner like animation. 
2. Figuring out how to animate different layer
3. Prevent multiple gesture happen at the same time.

How I solve all of them? 

## Solution

### Problem 1 - Spinner like animation

I cut the round circle vertically to create 2 half images. Then, I created 2 semicircles overlay on top of each other and placed them in the left half of the image. Let's call the first semicircle A and the other one B. I first animate both A and B to spin until both fully shown, we stop A's animation and continue B's animation untl it is fully covering the circle. This create a perfect spinning animation. 

The trick here would be handling the zIndex of each layers at different time. For example during the first half of the animation, the left half of the image should be at the highest index, when A and B is shown it's zIndex has to be lowered, so that B can overlay on top of the left half image. 

Below is a demonstration on how it works.

<p data-height="758" data-theme-id="0" data-slug-hash="qJwpww" data-default-tab="result" data-user="clement_peiheng_tan" data-pen-title="qJwpww" class="codepen">See the Pen <a href="https://codepen.io/clement_peiheng_tan/pen/qJwpww/">qJwpww</a> by Clement tan  (<a href="https://codepen.io/clement_peiheng_tan">@clement_peiheng_tan</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<br/>

### Problem 2 - Animation of layer

By utilizing `Animated.Parallel`, we can run multiple animation at the same time. This allows us the fired up all the events when the user touch the image, including expanding the '+' and 'x' icon, expanding the image and start the spinning animation. This problem allows me to get further understanding on how animated api work in react native. 

### Problem 3 - Multiple Gestures Event handler

There is a confusion in the gesture of holing the image to swipe up and down and the horizontal scroll. I solved this issue by disabling the horizontal scroll when user hold and swipe up and down. This is achived by letting the child component to pass a value to parent indicationg the user has pressed the imasge and the parent has to disable the horizontal scroll. When the touch is release, the horizontal scroll animation is reenabled.  

## Final

Here is the final result of the feature

![](https://media.githubusercontent.com/media/clementpeihengtan/clement-tph/gh-pages/assets/article_images/2018-10-23-my-sampler-apple-music-ui-with-react-native/demo-my-sampler-res.gif)

<center><strong>Left - </strong>From Jason Yuans's design, <strong>Right - </strong>Created using react-native with animated API</center>

## Changes in the future

There are some minor details that have not been implemented.

1. The red area when the image is swipe down. 
2. The blur effect should take over the whole page including the navigation bar
3. Light shadow under the image 

## Conclusion

Through this project, I have a better understanding of react native animated API and how to handle multiple animation at the same time within component and between parent and child component. 

Hope you guys enjoy it. Feel free to contact me through my [Linkedin]('https://www.linkedin.com/in/clement-pei-heng-tan-b84889105/') or [Facebook]('https://www.facebook.com/tan.clement.52'), would love to get more opinion from all the talented people out there.
  
