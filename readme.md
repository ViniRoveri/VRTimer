![Homepage screenshot](./src/img/Capa%20VR%20Timer.png)

# VR Timer ([Website link](https://viniroveri.github.io/VrTimer/))


## What is this?

A timer focused on the practice of the Rubik's Cube, following the official competition rules.


## Why is this?

To have a timer with simple usability and clean design that offers, without too much complexity, everything you need to practice the sport.


## What challenges did I overcome working on this?

- ### Times storage

Times are stored even if the user closes or reloads the page. For this the obvious solution is to use `Local Storage`, but there is a problem that JavaScript does not read the `entries` of an object in order, making it impossible to display the times the way I wanted. So the solution I found was to create a `State` that consists of an `Array` with the times, and to read this `Array` to have all the times stored and shown in order. And finally, so that times are not lost when reloading the page, each time a time is added to the `Array` I create a copy of this `Array` in `Local Storage` using a `JSON.parse` of it like `value`, so the times are stored in the browser and I can do the reverse process each time the user opens the page to recreate the `Array` of times, pulling the value from `Local Storage`, for the site to work normally again.


- ### Individual commands for each time

When clicking on each time, a pop-up will show: the time, the scramble, the date it was done and options such as adding a penalty or deleting it. For that I needed to create a generic pop-up and each time a time was clicked pass its information via `props` to the pop-up. For this to be possible, I created an `Object` at each time that inherits a `Class` that stores each of the information to be demonstrated and/or changed.


- ### Automatic average calculator

The averages (except the Global) are calculated using official competition rules, where the best and worst times are ignored and the average of the remaining is taken. The calculation logic only involves basic math and manipulation of the time array, the real challenge was getting the display of averages to update each time a time was added, removed or modified. For that I used `useEffect` to keep track of each time the `Array` or a specific time was changed, and run the average calculation commands.


- ### Timer that works both on keyboard and touch screen

In order not to have code repetition, I created a generic function that identifies which moment the timer is in(Before starting, during inspection, during solve or after completion) and takes the correct action based on that. The next step was to find a common ground between the keyboard and the touch screen, and after many tests the best match I found was `onkeyup`/`onkeydown` for the keyboard and `onTouchStart`/`onTouchEnd` for the touch screen. After that, I just added the generic function created to each of these events with some small adjustments that I thought were necessary and the timer was already working 100%.


- ### Scramble generator

This challenge was separated into two steps, the first was to discover how computers generate scrambles, and the second to replicate this. The challenge became greater because there was no shuffling generator written in JavaScript on the internet for me to base myself on, so I went after understanding the theoretical logic behind all the generation, and in my own words (or my own codes) I was able to perfectly recreate the professionally used generators.