---
title:  "Streams are for everyone"
date:   2018-02-11 10:10:55
categories: [javascript, streams]
tags: [javascript, code, streams]
---

## Streams are for everyone

I have been fiddling with reactive programming for a while, mostly with RxJS, and I simply love the tools.

If you don't know what an observable is, it's basically a `Promise`-style wrapper in which events can be composed.  In other words, you can map over the output of functions that would otherwise use callbacks.

This is an example of an event emitter for tracking a user's status:

~~~js
function createOnlineEmitter() {
  let cbs = []; //array of registered callbacks for the event
  let unsub; //function for removing the main event listener

  //this is the main event listener that gets registered with window.online/offline event
  const mainListener = (isOnline) => {
    //call all the subscribed callbacks
    cbs.forEach(cb => cb(isOnline));
  };

  const registerMainListener = () => {
    const boundOnline = mainListener.bind(null, true);
    const boundOffline = mainListener.bind(null, false);
    window.addEventListener('online', boundOnline);
    window.addEventListener('offline', boundOffline);
    //return unsubcribe functionality in a closure
    return function unsubscribe() {
      window.removeEventListener('online', boundOnline);
      window.removeEventListener('offline', boundOffline);
    };
  };

  const addCb = (cb) => {
    cbs.push(cb);
    //register main listener only once
    //use existence of `unsub` as indicator if main event listener is added or not
    if(!unsub) {
      unsub = registerMainListener();
    }
  };

  const removeCb = (cb) => {
    const index = cbs.indexOf(cb);
    if(index > -1) {
      cbs.splice(index, 1);
    }
    //if no callbacks left, remove main event listener
    if(cbs.length === 0 && unsub) {
      unsub();
      unsub = null;
    }
  };

  return function initOnlineEmitter(cb) {
    addCb(cb);
    //call it async with the initial val
    setTimeout(() => {
      cb(navigator.onLine);
    });
    //return unsubscribe function to caller
    return removeCb.bind(null, cb);
  };
}

// implement it
const onlineEmitter = createOnlineEmitter();
let unsub = onlineEmitter(isOnline => console.log(isOnline));
unsub();
~~~

Not too bad, but this is what the implementation would look like with observables:

~~~js
const { Observable } = require('rxjs/Observable');
require('rxjs/add/observable/fromEvent');
require('rxjs/add/operator/map');
require('rxjs/add/observable/merge');

function createOnline$() {
  //merge several events into one
  return Observable.merge(
    //use .map() to transform the returned Event type into a true/false value
  	Observable.fromEvent(window, 'offline').map(() => false),
  	Observable.fromEvent(window, 'online').map(() => true),
    //start the stream with the current online status
  	Observable.create(sub => {
  		sub.next(navigator.onLine);
  		sub.complete(); //this one only emits once, so now we end it
  	})
  );
}

// implement it
const onlineSub = createOnline$().subscribe(isOnline => console.log(isOnline));
onlineSub.unsubscribe();
~~~

Simple example. Observables are awesome tools.
