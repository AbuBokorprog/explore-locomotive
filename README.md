# Locomotive

### If you want to use the Locomotive

Locomotive ব্যবহার করার জন্য কয়েকটি জিনিস খেয়াল রাখতে হবে। স্ট্রাকচার ভালোভাবে ডিজাইন করতে হবে। সবগুলো পেজের parent হতে হবে main কন্টেইনার।

আরো জানতে হলেঃ ```https://github.com/locomotivemtl/locomotive-scroll

```

- **First**: You have to link css and js links of locomotive in the index.html file.

```

https://cdn.jsdelivr.net/npm/locomotive-scroll@3.5.4/dist/

```

- **Second**: You have to import the js code from LocomotiveScroll github.

```

https://github.com/locomotivemtl/locomotive-scroll

````

### **Example**:

```javascript
const scroll = new LocomotiveScroll({
  el: document.querySelector("#main"),
  smooth: true,
});

let tl = gsap.timeline();

tl.from("#page1 #box", {
  scale: 0,
  duration: 2,
  delay: 2,
  rotate: 360,
});
tl.from("#page2 #box", {
  scale: 0,
  duration: 2,
  rotate: 360,
  scrollTrigger: {
    trigger: "#page2 #box",
    scroller: "#main",
    // markers: true,
    start: "top 80%",
    end: "top 30%",
    scrub: 2,
  },
});
````

## If you want to use Locomotive with Gsap

- After importing css and js links, import the javascript code from locomotive scrollTrigger codePen.

```
https://codepen.io/GreenSock/pen/ExPdqKy
```

```javascript
gsap.registerPlugin(ScrollTrigger);

// Using Locomotive Scroll from Locomotive https://github.com/locomotivemtl/locomotive-scroll

const locoScroll = new LocomotiveScroll({
  el: document.querySelector("#main"),
  smooth: true,
});
// each time Locomotive Scroll updates, tell ScrollTrigger to update too (sync positioning)
locoScroll.on("scroll", ScrollTrigger.update);

// tell ScrollTrigger to use these proxy methods for the "#main" element since Locomotive Scroll is hijacking things
ScrollTrigger.scrollerProxy("#main", {
  scrollTop(value) {
    return arguments.length
      ? locoScroll.scrollTo(value, 0, 0)
      : locoScroll.scroll.instance.scroll.y;
  }, // we don't have to define a scrollLeft because we're only scrolling vertically.
  getBoundingClientRect() {
    return {
      top: 0,
      left: 0,
      width: window.innerWidth,
      height: window.innerHeight,
    };
  },
  // LocomotiveScroll handles things completely differently on mobile devices - it doesn't even transform the container at all! So to get the correct behavior and avoid jitters, we should pin things with position: fixed on mobile. We sense it by checking to see if there's a transform applied to the container (the LocomotiveScroll-controlled element).
  pinType: document.querySelector("#main").style.transform
    ? "transform"
    : "fixed",
});

// each time the window updates, we should refresh ScrollTrigger and then update LocomotiveScroll.
ScrollTrigger.addEventListener("refresh", () => locoScroll.update());

// after everything is set up, refresh() ScrollTrigger and update LocomotiveScroll because padding may have been added for pinning, etc.
ScrollTrigger.refresh();
```

### **Examples:**

```javascript
gsap.registerPlugin(ScrollTrigger);

// Using Locomotive Scroll from Locomotive https://github.com/locomotivemtl/locomotive-scroll

const locoScroll = new LocomotiveScroll({
  el: document.querySelector("#main"),
  smooth: true,
});
// each time Locomotive Scroll updates, tell ScrollTrigger to update too (sync positioning)
locoScroll.on("scroll", ScrollTrigger.update);

// tell ScrollTrigger to use these proxy methods for the "#main" element since Locomotive Scroll is hijacking things
ScrollTrigger.scrollerProxy("#main", {
  scrollTop(value) {
    return arguments.length
      ? locoScroll.scrollTo(value, 0, 0)
      : locoScroll.scroll.instance.scroll.y;
  }, // we don't have to define a scrollLeft because we're only scrolling vertically.
  getBoundingClientRect() {
    return {
      top: 0,
      left: 0,
      width: window.innerWidth,
      height: window.innerHeight,
    };
  },
  // LocomotiveScroll handles things completely differently on mobile devices - it doesn't even transform the container at all! So to get the correct behavior and avoid jitters, we should pin things with position: fixed on mobile. We sense it by checking to see if there's a transform applied to the container (the LocomotiveScroll-controlled element).
  pinType: document.querySelector("#main").style.transform
    ? "transform"
    : "fixed",
});

// each time the window updates, we should refresh ScrollTrigger and then update LocomotiveScroll.
ScrollTrigger.addEventListener("refresh", () => locoScroll.update());

// after everything is set up, refresh() ScrollTrigger and update LocomotiveScroll because padding may have been added for pinning, etc.
ScrollTrigger.refresh();

// const scroll = new LocomotiveScroll({
//   el: document.querySelector("[data-scroll-container]"),
//   smooth: true,
// });

// const scroll = new LocomotiveScroll({
//   el: document.querySelector("#main"),
//   smooth: true,
// });

let tl = gsap.timeline();

tl.from("#page1 #box", {
  scale: 0,
  duration: 2,
  delay: 2,
  rotate: 360,
});
tl.from("#page2 #box", {
  scale: 0,
  duration: 2,
  rotate: 360,
  scrollTrigger: {
    trigger: "#page2 #box",
    scroller: "#main",
    // markers: true,
    start: "top 80%",
    end: "top 30%",
    scrub: 2,
  },
});
tl.from("#page3 #box", {
  scale: 0,
  duration: 2,
  rotate: 360,
  scrollTrigger: {
    trigger: "#page3 #box",
    scroller: "#main",
    // markers: true,
    start: "top 80%",
    end: "top 50%",
    scrub: 2,
  },
});
```
