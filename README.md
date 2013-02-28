# cam.js

A lightweight wrapper to simplify Javascript camera capture :)

Provides browser agnostic shortcuts to get &lt;img&gt; and &lt;video&gt; DOM elements from a webcam.
Also provides a Capture class for rapid successive still captures to data URLs, &lt;img&gt; DOM elements, or canvas 2d contexts.

Currently supports Chrome, Opera, and Firefox.

To get things working in Firefox go to "about:config", make your promise, search for "media.navigator.enabled", and double click it to set it to true if it is not already.
Firefox support is a little buggy at the moment since getUserMedia() is not technically ready for prime-time on that browser yet (as of Firefox 19).


## API Overview

* __cam.supported()__

  > Returns true if camera capture is plausible
  
* __cam.media(callback)__

  > Gets an object url representing a camera stream for use as the src of &lt;video&gt; elements or null on error
  
  > *callback* Will be called with and when parameters `url` and `stream` are ready
  
  > Be aware that some browsers will ask the user for permission to access the camera each time this is called
  
* __cam.video(callback)__

  > Gets a &lt;video&gt; DOM element with a camera attached as the video source or null on error
  
  > *callback* Will be called with and when parameters `video`, `url`, and `stream` are ready
  
  > Be aware that some browsers will ask the user for permission to access the camera each time this is called

* __cam.image(callback)__

  > Opens the camera, gets an &lt;img&gt; DOM element from it or null on error and closes the camera
  
  > *callback* Will be called with parameter `img` once an &lt;img&gt; DOM element is captured
  
  > Be aware that some browsers will ask the user for permission to access the camera each time this is called

* __cam.Capture__

  > Capture class for rapidly capturing multiple frames from the camera
  
  * __start(callback)__
  
    > Starts a capturing session
    
    > *callback* Will be called with this object as a parameter when the camera is ready or null on error
    
  * __stop()__
  
    > Stops a capturing session
    
  * __width()__
  
    > Returns the width of the capture frame in pixels or null on error
    
  * __height()__
  
    > Returns the height of the capture frame in pixels or null on error
    
  * __captureDataURL()__
  
    > Returns a captured frame formated as a base64 encoded png image file or null on error
    
  * __captureImage()__

    > Returns a captured frame in the form of an &lt;img&gt; DOM element or null on error
    
  * __captureContext2d(context2d)__
  
    > Captures a frame and draws it on to a canvas (stretched to fit)
    
    > *context2d* The 2d context used to draw the image on to a canvas


## Examples

### Show video from camera

    cam.video(function(elm) {
        if(elm)
            document.body.appendChild(elm);
    }

### Show image from camera

    cam.image(function(elm) {
        if(elm)
            document.body.appendChild(elm);
    }

### Capture to canvas for processing

    var cap = new cam.Capture();
    var canvas = document.createElement("canvas");
    var ctx = canvas.getContext("2d");
    
    cap.start(function(cap) {
        if(cap)
            process();
    });
    
    function process() {
        cap.captureContext2d(ctx);
        
        //Your code here
        
        setTimeout(process, 50);
    }
