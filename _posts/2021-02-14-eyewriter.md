---
title: "EyeWriter"
modified: "2021-02-14"
category: category-1
tags: 
  - "computervision"
  - "computervisionprojects"
  - "eyewriter"
  - "opencv"
  - "opencv-projects"
  - "opencvprojects"
  - "python"
  - "python3"
image: /images/2021/eyewriter-graphic-1.png
thumbnail: /images/2021/eyewriter-graphic-1.png
---

I've been working on a prototype for a project I call eyeWriter. The basic idea of eyeWriter is to track the user's eye movements and determine where the user is looking on a screen consisting of several communication options and thereby finding what the user wants to communicate. The project has been put through three different competitions and receieved a large number of suggestions. I'm still developing the product into its final version but a peliminary 'proof-of-concept' prototype is complete. Here's a short video I made about it.

<a href='https://www.youtube.com/watch?v=jHoosxEf85E'>The video</a>

## EyeWriter :)

The product will have two variants. 

Both variants will have similar hardware. However one will have a static display unit with options to choose from, while the other will have a dynamic set of options that can be configured based on user requirements. 

I decided to make two variants as the first variant allows people in a difficult financial situation to use our product. In India, the number of those below the poverty line is high and in order to allow a large number of people to use our product, its cost needs to be low. The first variant and its static display allow the product to be made at a low cost, making it financially suitable for a larger group of people.

<p align='center'>
  <img src = "https://aryanaut.files.wordpress.com/2021/02/2nd-variant.png?w=900" alt = 'V1 Interface'>
  <img src = "https://aryanaut.files.wordpress.com/2021/02/optrak-graphic.png?w=900" alt = 'V2 Interface'>
</p>    

V1 User Interface VS. V2 User Interface

Our second variant is for those who have the choice to purchase a more sophisticated product for the same purpose. Our two variants together give our product a larger market and increase its overall impact.

The product will consist of a motherboard where all the image processing happens, a pair of cameras to create a depth map of the surroundings thereby allowing better tracking, and a screen or board with several options. The system will be placed approximately 60-70 centimeters from the user's face. The entire setup is designed to clamp onto a standard hospital stand, however, it can also be placed on any flat surface. Once it is placed, it need only be moved if the location is being changed. 

eyeWriter fits into the assistive device market. It can be used anywhere, from hospitals to bedrooms, and is easily implemented, requiring only a stand to keep the hardware. This setup is simple and lightweight, requiring no knowledge of computers or programming, and needs to be set up only once as long as the patient and the device are relatively stationary.

## Working

eyeWriter's variants both rely on the same basic method. When the user sits in front of opTrak, the system automatically detects his or her face using the python library dlib. It compares all visible shapes from the live camera feed to a set of 68 facial landmarks that roughly depict the shape of the face. Using these same landmarks, the system finds the eye. 

The program then takes the portion of the live camera feed which contains the eye and converts it from an RGB image to an inverted threshold image. The image conversion parameters can be adjusted according to the light level. Since the iris is the darkest part of the eye, its shape can easily be detected by the system by the contour detection method. By this method, the outline of the iris can be plotted from which its center can be found. 

<p align="center">
<img src="https://aryanaut.files.wordpress.com/2021/02/thr.png?w=528" alt="Thresholded Image">
<img src="https://aryanaut.files.wordpress.com/2021/02/examine.png?w=528" alt="Detected Iris Center">
</p>

When the center of the iris is found, the user will be instructed to look at the four corners of the screen. At each position, the system saves the position of the iris. When the position of the iris is recorded at all four points, the user is asked to look at the center of the screen. This calibration method gives the user's iris position relative to the four corners of the screen. Using this information, whenever the user looks at any point on the screen, the computer will be able to calculate which point on the screen the user is looking at (shown in the video)

In the first variant’s template itself is divided into several sections, each section when looked at for 3 seconds triggers a different voice output. The sections will include one for asking for food, one for water, one for medicine, and one for an emergency situation which will alert everyone nearby that the user is in distress. In our second variant, the screen will consist of a number of options and menus which open new windows to more options. So the flexibility of opTrak as a communication device is much more in its second variant.

In addition to these features, our prototype uses a pair of Raspberry Pi Cameras to create a 3D pixel map which allows the system to know how far away the user is and based on that information can automatically adjust its parameters to make the eye-tracking work better.

<p align='center'>
  <img src='https://aryanaut.files.wordpress.com/2021/02/3d-model-of-both-variants.png?w=520' alt="3D Model of the variants - Alternate title for eyeWriter is opTrak">
</p>

That's all I have for now. Live Long and Prosper!

Here's my [GitHub](https://github.com/Aryanaut/EyeText).

[Instagram](https://www.instagram.com/aryan_m05/), [Twitter](https://twitter.com/aryanaut), [Gumroad (graphic novel out here)](https://gumroad.com/aryanaut)
