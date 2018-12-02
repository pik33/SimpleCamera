# SimpleCamera

A simple camera unit for Ultibo using pure OMX calls
v.0.11 alpha - 20181202

Working alpha code

based on https://github.com/SonienTaegi/rpi-omx-tutorial

Instructions:

(1) call initcamera with your desired parameters

check the result: if it is >$C0000000 then all went OK, the camera is in the idle state, and the result is the address of the main camera buffer

If it is small integer, an error occured

   1 - error while loading the camera component
   2 - error while setting camera number
   3 - error while setting the video format
   4 - error while switching the camera to the idle state
   5 - error while allocating the camera buffer
   6 - camera didn't reached the idle state

If all went OK, you will get pointers to y, u, v buffers in pY, pU, pV and their sizes in sizey, sizeu, sizev

(2) call startcamera. If it returned 0, the worker thread is started

In your main thread wait until filled=true and read the buffers as fast as you can, then set filled=false
If there is no filled=false set by the receiving thread, the camera worked thread will stop itself in one second

(3) when done, call stopcamera

(4) after this you can start it again or...
(5) call destroycamera which will unload it and close omx.

