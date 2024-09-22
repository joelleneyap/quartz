---
draft: false
date: 9/21/24
tags:
  - clipping
---
Source: [[Gaboury, Image Objects]] ch3

-> realism in computer graphics is a huge goal, but it's also achieved via illusion, one that privileges appearance over geometry/
# the break of image from object
In the work of Gouraud and Phong, we can see **the break of image from object**—**a decoupling of geometry from visualization that has come to define the contemporary field of graphical research.**
* This is likewise the moment that the illusory quality of graphical images becomes formalized at the algorithmic level such that the **images produced by these systems no longer reflect the underlying architecture of the objects they represent.**
* Gouraud: a negotiation between image and object, in which each serves as a contextual interface with distinct applications. It is a display that **sacrifices accuracy for efficiency, privileging appearance.**
* **the realism of computer graphics remains highly conscripted, and is limited to the visual appearance of an object largely divorced from its physical or geometric structure**
	* This split persists well into the present, and has been complicated by subsequent splits with real-time graphics for digital games, raster graphics for interface design, and countless other subfields that remain structured by research first devel- oped in the 1960s, even as they become differentiated into unique fields of practice.
![[Screenshot 2024-09-21 at 9.45.41 PM.png]]

## Gouraud & Phong
* Significantly, neither of these methods transforms the geometry of an object itself; they simply alter the appearance of a given surface
* While computer-aided models for engineering and design are built to precise material specification, such that the model and object are mathematically identical, shading and other rendering techniques are developed to produce the illusion of a material effect (smooth surfaces, light, color, etc.), but do not necessarily reflect any underlying mathematical or material form.
* Gouraud
	* The idea came to him in a signal processing course taught by Utah pro- fessor Thomas Stockham: **if he created the appearance of a smooth surface with proper shading, the eye would simply ignore the angular form.** In other words, if he **privileged the appearance of the image over any underlying geometry**, he could calculate shaded images in real time.
	* shading algorithm applies the interpolation seen previously in the simulation of curves to the polygon mesh of modeled surfaces, using the vertices of these surface polygons as the data points from which to build its interpolation.
* Phong
	* Extended Gouraud’s work on shading and reflection algorithms for 3D rendered models, producing a shading model that improved on some of the difficulties in Gouraud’s algorithm by making a separate color computation for each individual pixel.33 This “Phong shad- ing” is much more computationally expensive than “Gouraud shading,”