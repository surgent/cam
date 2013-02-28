cam.js
===

A lightweight wrapper to simplify Javascript camera capture :)

Provides browser agnostic shortcuts to get &lt;img&gt; and &lt;video&gt; DOM elements from a webcam.
Also provides a Capture class for rapid successive still captures as data URLs, &lt;img&gt; DOM elements, or drawn onto a 2d canvas context.

Currently supports Chrome, Opera, and Firefox.

To get things working in Firefox go to "about:config", make your promise, search for "media.navigator.enabled", and double click it to set it to true if it is not already.
Firefox support is a little buggy at the moment since getUserMedia() is not technically ready for prime-time on that browser yet (as of Firefox 19).
