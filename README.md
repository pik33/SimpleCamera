# SimpleCamera

A simple camera unit for Ultibo using pure OMX calls
v. 0.13 alpha - 20181220

Working alpha code

based on https://github.com/SonienTaegi/rpi-omx-tutorial

Instructions:

(1) provide a buffer for the camera

(2) call initcamera with your desired parameters: xres, yres, fps and your buffer address

(3) check the result: if it is >$C0000000 then all went OK, the camera is in the idle state, and the result is the address of the main OMX camera buffer

If it is small integer, an error occured

   1 - error while loading the camera component
   2 - error while setting camera number
   3 - error while setting the video format
   4 - error while switching the camera to the idle state
   5 - error while allocating the camera buffer
   6 - camera didn't reached the idle state

(4) call startcamera. If it returned 0, the worker thread is started

In your main thread wait until filled=true. You have a frame in your buffer. Set filled to false again.

(5) when done, call stopcamera

(6) after this you can start it again or...

(7) call destroycamera which will unload it and close omx.

