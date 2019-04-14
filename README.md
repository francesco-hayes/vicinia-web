# Vicinia
My *chaotically* written code for the 2019 Hackathon hosted by PackHacks at North Carolina University.

## Team Members
* Francesco Hayes (me): Web Developer
* Boston Cartwright: Mobile App Developer
* Tyler Smith: Backend Developer
* Michelle Charette: "Math Guy" on Backend Developer

## Description
The website takes advantage of the **Vue.js Framework**, **Three.js WebGL Library**, and **GSAP Animation Library** to present
the end product (the app) in a practical, clean, and entertaining manner. All of the frameworks except for Vue.js were new and experimental. It was my first time in real implementation.

I encountered plenty of bugs involving packaging errors with the **Three.js Library** due to some of their packages being separate and not included within the core. This caused plans to shift from using GPU Accelerated Graphics to CPU Power, which caused a change in design dramatically. Nevertheless, Michel and I managed to form a sphere using BufferGeometry and 2D Points successfully. This issue was the longest.

The rest involved tedious work in configuring the **GSAP Library** to trigger animations correctly and not allow the user to spam events. The built-in functions for the TimelineMax would cause the WebGL to break and not render, so the workaround was to include a switch and trigger in the event.

It took a total of 15 hours to develop the end product with no errors. This time does not include clean-up in the code. We were tired by then...

## Photos

<img src="https://vicinia.net/img/mobile_01.2765fb34.webp" alt="Vicinia Splash Photo" width="250"/><img src="https://vicinia.net/img/mobile_02.e0ca32d0.webp" alt="Vicinia Username Photo" width="250"/><img src="https://vicinia.net/img/mobile_04.5f60fc8e.webp" alt="Vicinia Chat Photo" width="250"/>

## Extra
I want to thank SVU for sponsoring our trip this year! It was a great first experience for the entire team, and we look forward to competing in more Hackathons shortly.


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
