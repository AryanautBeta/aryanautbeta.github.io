---
title: "Palm motion detection and tracking for drawing!"
date: "2020-10-22"
category: category-1
tags: 
  - "computer-vision"
  - "hand-tracking"
  - "opencv-projects"
  - "projects"
  - "tech"
image: "/images/2020/10/detected_contours.png"
---

Recently I made a program to track my hand movements and translate that into cursor movements on the computer screen. I used OpenCV and Python3 to do so. **Here's how it works!**

First the program reads the video from the connected camera (USB webcam in my case). After that, it converts the frame to black and white. The B/W image is then thresholded so that points that are brighter are considered as white and the darker points are considered black.

From here the program detects the largest contour in the image.

<p align="center">
<img src='/images/2020/10/hand-1.jpg'>
    
<img src='/images/2020/10/gray-1.png'>
    
<img src='/images/2020/10/canny-1.png'>

<img src='/images/2020/10/detected_contours-1.png'>
</p>

After that, I detect the convex hull in the image. With this, it will join the tips of the fingers to form a polygon. To better explain my point, here's how it looks.

<p align="center">
<img src='/images/2020/10/output-0.png'>

<img src='/images/2020/10/output-1.png'>
</p>

After finding the convex hull, to detect the pointer finger, we find the furthest point from the center that is within the convex hull (in blue).

<p align="center">
<img src='/images/2020/10/output-2.png'>
</p>

Let's call this point **_fPos(x, y)_**. To improve the tracking, it is best to use a pointed object such as a pencil to test this program.

<p align="center">
<img src='/images/2020/10/output-3.png'>
</p>

Now we need to find the position on the screen where the mouse cursor should be relative to **_fPos(x, y)_**. I did this by first finding the ratios between the dimensions of the video. My webcam's video resolution is 640x480 and my screen's resolution is 1920x1080. So the center of the video will be _**videoCenter(320, 240)**_ and the screen's center will be _**screenCenter(960, 540)**_. If we divide **_videoCenter_'s** x-coordinate by **_screenCenter_'s** x-coordinate, we get _**ratioX**._ Similarly we can do the same with _**videoCenter**_ and **_screenCenter_'s** y-coordinates to obtain _**ratioY**_. Now to get the position of the cursor on the screen relative to _fPos_ is:-

_**sPos(x1, y1)** where_ **_x1_ = _(x_\*_ratioX_)÷2** _and_ **_y1 \= (y\*ratioY)_÷2**

Now using the python module **[_pynput_](https://pypi.org/project/pynput/)** we can set the mouse cursor position to _sPos_ and now we can control the mouse with hand movements.

[Here is a demo](https://youtu.be/AOcOx\_yZM98)

**Conclusion**

Though the program has a few bugs now, I had fun doing it and I hope that others can have fun with it too. If you'd like to test this program, just have Python and OpenCV installed along with a few other modules listed here -

- [dlib](https://pypi.org/project/dlib/)
- [numpy](https://pypi.org/project/numpy/)
- [keyboard](https://pypi.org/project/keyboard/)
- [pynput](https://pypi.org/project/pynput/)
- [PIL](https://pypi.org/project/Pillow/)
- [matplotlib](https://pypi.org/project/matplotlib/)
- [pyautogui](https://pypi.org/project/PyAutoGUI/)

You'd also need to clone the project from github [here](https://github.com/Aryanaut/handtracking) and run _**main-1.py**_. Controls -

_**d** - drawing, **e** - eraser, **left-click** - clear screen, **right-click** - toggle mouse control_

That's all I have for now!
