---
title: Pinhole, computational, and corner cameras
keywords: (insert comma-separated keywords here)
order: 17 # Lecture number for 2020
---

Authors:
Gurdeep Sullan, Eva Prakash, Danny Tse, Ryan Kirk, Zijian Zhang, Bronson Sansoni, Chandra Rajyam, Diego Vargas

Introduction
============

A camera is an important tool in computer vision that can represent the
three-dimensional world around us in two-dimensional photographs that we
can analyze.

Pinhole Cameras
===============

A camera operates by receiving the light rays emitted from a real-world
object on a piece of film. However, if every light ray from the object
was allowed to be projected onto the film, each pixel on the film would
capture the light emitted from all parts of the object, creating an
unfocused and blurry image.

![image]({{ site.baseurl }}/assets/images/pinhole_nobarrier.png =100x100) *(Image taken from CS 131 Lecture 17)*
This figure displays how without any type of filtering applied to the
light rays emitted from an object, the projected image on the film will
be noisy and unclear.

A pinhole camera system works around this problem by adding a barrier
between the object and the film with a small opening, or aperture, in
the middle of the barrier. The barrier boundaries block off the majority
of the light rays and let a focused subset of rays pass through the
aperture to create a sharper, clearer image on the film. Since the light
rays emitted from the top part of the object can only pass through the
aperture if they are angled downwards, and the light rays emitted from
the bottom part of the object can only pass through the aperture if they
are angled upwards, the image projected onto the film will be
upside-down.

![image]({{ site.baseurl }}/assets/images/pinholecamera2.png =100x100) *(Photo taken from Stanford CS231A Course
Notes 1: Camera Models)* This figure displays how in a pinhole camera
system, light rays emitted from an object filter through an aperture in
a barrier to create an inverted image of the object on a film.

The system of projecting an inverted image created by a pinhole camera
onto a wall of a darkened room instead of a film is called camera
obscura. Camera obscura was practiced in classical China and Greece and
commonly used for tracing images onto paper.

![image]({{ site.baseurl }}/assets/images/camera_obscura.png =100x100) *(Photo taken by group member)* This figure
displays the inverted projected image of the makeshift camera obscura
created in the garage of a group member.

Dimensionality Reduction
------------------------

The dimensionality reduction that is performed by a camera can often
cause key information about the three-dimensional world to be lost in
the two-dimensional image based on the viewpoint and configuration used
by the camera. The length, proximity, and angles of subjects captured in
a photograph can be misrepresented depending on how the subjects are
oriented with respect to the camera and each other. In the example
below, since the subjects are all positioned at different distances and
angles, we are unable to say with certainty who is taller than whom,
which ball is closer, or whether each person is parallel or
perpendicular to everyone and everything else.

![image]({{ site.baseurl }}/assets/images/perspective.png =100x100) *(Image taken from CS 131 Lecture 17)* This
figure is an example of a photograph in which dimensionality reduction
from three dimensions to two dimensions has caused a loss of length and
angle information.

However, straight lines are preserved in an image, and tracing parallel
lines will lead to an intersection at a vanishing point along a
vanishing line within an image.

![image]({{ site.baseurl }}/assets/images/vanishing.JPG =100x100) *(Photo taken by group member)* This figure
displays an image with a vanishing line shown in red and the path toward
a vanishing point shown in blue.

Projective Geometry
-------------------

Let us assume we have the pinhole camera system shown below.

![image]({{ site.baseurl }}/assets/images/pinholecamera1.png =100x100) *(Photo taken from Stanford CS231A Course
Notes 1: Camera Models)* This figure is a mathematical model of a
pinhole camera system with labeled relevant variables.

We have an aperture $O$ and we want to project the three-dimensional
point $P$ through $O$ into a two-dimensional point $P’$ on the film. We
define our coordinate system to be centered at $O$, with $P$ having the
three-dimensional coordinates ($x$, $y$, $z$) and $P’$ having some
two-dimensional coordinates ($x’$, $y’$). We can project the aperture
$O$ onto the film as point $C’$, with the line spanning from $C’$ to $O$
with length $f$ being the optical axis. Using the law of similar
triangles between triangle $P'C'O$ and the triangle with corners $P$,
$O$, and ($0$,$0$,$z$), we can derive

$x’ = f\frac{x}{z}$, $y’ = f\frac{y}{z}$

Moving the film closer to the pinhole scales the size of the projected
image down, and moving the film farther from the pinhole scales the size
of the projected image up. Increasing aperture size allows more light
rays to filter onto the film, creating a blurrier projected image.
Decreasing aperture size sharpens the image by applying a stronger
filter to the light rays passing through the pinhole. However, an
aperture that is too small will create an image that is too dark and
subject to diffraction effects.

![image]({{ site.baseurl }}/assets/images/IMG_0826.JPG =100x100) ![image]({{ site.baseurl }}/assets/images/IMG_0825.JPG =100x100) ![image]({{ site.baseurl }}/assets/images/IMG_0827.JPG =100x100)
*(Photo taken by group member)* This figure displays how the image of a
dog changes with increasing camera aperture. At a very low aperture, not
enough light can pass into the camera, creating a darkened image. At a
medium-sized aperture, a reasonable amount of light can pass through and
a clear image is produced. At a very high aperture, too much light
passes into the camera and the image is blurry.

Cameras and Lenses
==================

Effects of a Lens
-----------------

### Role of a Lens

The role of a lens is to focus light on the film.

![image]({{ site.baseurl }}/assets/images/Role_of_lens.png =100x100)

### Focal Point

Every lens has a focal point and a focal length, $f$.

![image]({{ site.baseurl }}/assets/images/Focal_point.png =100x100)

Rays that pass through the center of the lens are not deviated. All
parallel rays of light converge at a single point (the focal point) on a
plane located at focal length, $f$.

### Circle of Confusion

There is a specific distance at which objects are "in focus" (at this
distance, rays of light converge at a single point).

![image]({{ site.baseurl }}/assets/images/Circle_of_confusion.png =100x100)

Objects that are at a depth different to this specific depth do not
converge at a single point (are "out of focus") and create a 'circle of
confusion.'

![image]({{ site.baseurl }}/assets/images/Circles_of_confusion_3d.jpg =100x100)

*(Photo taken from theimage.com)* As you can see here, objects that are
further from the true focus point converge beyond the plane of focus,
while objects closer than the true focus point converge before the plane
of focus.

Mathematics of Lenses
---------------------

### Laws of Geometric Optics

Light travels in straight lines through homogeneous mediums.\
Reflection upon a surface: the incoming ray, surface normal and
reflected ray are co-planar (residing within the same plane).\
Refraction: When a ray passes from one medium to another.

### Reflection

![image]({{ site.baseurl }}/assets/images/Reflection_and_refraction.png =100x100)

where $r_1$ is the incoming ray, $r_1$' is the reflected ray, and
$\alpha_1$ is the incident angle. The surface normal is not pictured,
but is the unit vector $\begin{bmatrix}0\\1  \end{bmatrix}$.

### Refraction

Refraction follows Snell's Law:
$$n_1\sin{\alpha_1} = n_2\sin{\alpha_2}$$

In the figure above and in Snell's law, $n_1$ is the index of refraction
for the first medium, $n_2$ is the index of refraction for the second
medium, $\alpha_1$ is the incident angle, and $\alpha_2$ is the
refraction angle.

### Very Thin Lenses

A very thin lens is a lens with a very small thickness, which is
negligible in relation to the radius of the curve of the lens. This
assumption simplifies ray tracing calculations.

![image]({{ site.baseurl }}/assets/images/Thin_Lens.png =100x100)

With thin lenses, we can ignore the effect of the thickness has on how
the ray travels. We can simply just focus of the light travel itself.
$P$ is the origin of the light rays. $O$ is the center of the lens. $f$
is the focal length. $P$' is the point at which they rays converge at
the distance $z$'. $z$' $= f + z_0$. $R$ is the radius of the lens. $n$
is the index of refraction for the lens. Based off of the assumptions of
thin lenses, we can actually derive the focal distance $f$ of the lens.
$$f = \frac{R}{2(n-1)}$$

For small angles, we can apply Snell's law, which states
$n_1\sin{\alpha_1} = n_2\sin{\alpha_2}$: $n_1 = 1$ is the index of
refraction for air. $n_2 = n$ is the index of refraction for the lens.
$\alpha_1$ is the incident angle. $\alpha_2$ is the reflection angle.
Based on this information and our assumptions of thin lenses, the point
$P$' can be calculated. Then, we can calculate the
$\begin{bmatrix}x'\\y'  \end{bmatrix}$ coordinates of where the rays
converge.\
$$z' = f + z_0$$ where $x$ is the $x$-component of the coordinates of
$P$, $y$ is the $y$-component of the coordinates of $P$, and $z$ is the
$x$-component of the distance from $P$ to $O$.\
Thus we can solve for the coordinates of $P$': $$x'= z'\frac{x}{z}$$ The
formula is the same for the $y$-component of $P$', just substitute the
$y$ coordinate of $P$ for the $x$ coordinate: $$y'= z'\frac{y}{z}$$

Issues with Lenses
------------------

Lenses, susceptible to flaws like many other things in nature, do not
come with issues. What if the lens has different refractive indices for
different wavelengths? In this section, we will address chromatic
aberration, spherical aberration, and radial distortion.

### Chromatic Aberration

Do you notice that, sometimes, when you take a photo with a camera, that
the edges in it seem discolored and blurry? This is due to lens having
different refractive indices for different wavelengths, and as a result,
a lens is unable to focus all wavelengths of color to the same point. In
more technical terms, we refer to this as \"chromatic aberration,\" or
\"color fringing.\"

![image]({{ site.baseurl }}/assets/images/chromatic.jpg =100x100)

*(image taken from Wikipedia)* This figure depicts an image taken by a
high quality lens, with minimal chromatic aberration on the top, versus
a low quality image with significant chromatic aberration.

Here, we discuss a more abstract model.

![image]({{ site.baseurl }}/assets/images/abstract_chromatic.png =100x100)

*(image taken from CS131 Lecture 17)*

As you can see from the above figure, we have the red, green, and blue
wavelengths focusing at different points. Chromatic aberration has
implications for the human eye as well. In fact, the human eye is most
sensitive to the green wavelength, with red and violet light appearing
out of focus. There are two types of chromatic aberration. Longitudinal
chromatic aberration, also known as \"bokeh fringing\", occurs when
different wavelengths of light are focused at different distances after
passing the lens. Transverse chromatic aberration occurs when different
wavelengths of light focus at different positions along the same focal
plane. Chromatic aberration can be minimized through using special types
of glass (i.e. low dispersion glass) and digital post-processing.

### Spherical Aberration

![image]({{ site.baseurl }}/assets/images/spherical_ex.png =100x100)

*(image taken from CS131 Lecture 17)* Example of Spherical Aberration.

Now, consider a spherical lens. Much like chromatic aberration, in
spherical aberration, the wavelengths of light focus at different
points, compromising the sharpness of the image and resulting in an
overall unfocused image. Ideally, all rays should converge at a single
point, but, like shown below, this is not always possible.

![image]({{ site.baseurl }}/assets/images/spherical_abb.png =100x100)

*(image taken from CS131 Lecture 17)* An abstract depiction of spherical
aberration. Here, the rays further from the optical axis focus closer.

Like chromatic aberration, there are two types of spherical aberration.
Positive spherical aberration is when the peripheral rays are bent too
much, and negative is when they are not bent enough. This effect can be
minimized by using particular lens systems (i.e. using combinations of
convex and concave lens).

### Radial Distortion

The third and final issue (that we will discuss) with lenses is radial
distortion. We can classify this distortion as either a \"pincushion
distortion\" or a \"barrel distortion.\" In a pincushion distortion, the
image magnification increases as the distance from the optical axis
increases. In contrast, in a barrel distortion, the opposite is true--
the image magnification decreases as the as distance from the optical
axis increases.

![image]({{ site.baseurl }}/assets/images/radial_abs.png =100x100)

*(image taken from CS131 Lecture 17)* Radial distortions can be
classified as either a pincushion or a barrel distortion.

![image]({{ site.baseurl }}/assets/images/radial_example.png =100x100)

*(image taken from CS131 Lecture 17)* An example of a barrel distortion.

Radial distortion can be corrected with software, using Brown's
distortion model. The software corrects the distortion by warping the
image in the reverse direction.

The Geometry of Pinhole Cameras
===============================

In this section of the lecture, we will talk about the geometry of a
pinhole camera. Especially, we will focus on the projection matrix for
modeling the projection from 3D space into a 2D image. The intrinsic
parameters and the extrinsic parameters will be discussed individually.

Projection Geometry
-------------------

![image]({{ site.baseurl }}/assets/images/Pinhole camera_real world.JPG =100x100)

*(Image taken from CS131 Lecture 17 slides)* Relating a real-world point
to a point on a camera.

For this section, we will consider a scenario where we have an ideal
pinhole camera without any lenses. As shown in the image above, a point
$P$ from the real world is projected into a 2D point $P’$ on the image
plane through the pinhole $C$. The focal length of this pinhole camera
is $f$, and as shown in the image, we will be able to observe a
symmetric virtual image on the other side of this system.\
As has been discussed earlier, using similar triangles, we could map the
x, y, z coordinates of the point $P$ onto $P’$ using the following
equation $$\begin{aligned}
P = (x, y, z) \rightarrow P' = (f \dfrac{x}{z}, f \dfrac{y}{z})\end{aligned}$$

to achieve the transformation from a 3D space to a 2D plane. To be
noted, this transformation is non-linear due to the division of the
non-constant coordinate z, which depends on how far the object is from
the camera. However, we would prefer this projection to be a linear
transformation, so that it could be represented as a dot product of a
matrix and an input vector of the point $P$. This linear representation
would make our downstream analysis easier.

Homogeneous Coordinates
-----------------------

![image]({{ site.baseurl }}/assets/images/Pinhole camera_real world 2.JPG =100x100)

*(Image taken from CS131 Lecture 17 slides)* 3D projection of point $P$
into $P'$.

Recalling from a previous lecture, we were able to get around this
problem by using the **homogeneous coordinate** system. For a 2D point
(x, y), we could design a homogeneous image coordinate by adding an
additional dimension. We could apply the same trick to obtain the
homogeneous scene coordinates for the 3D point $P$ (x, y, z):
$$\begin{aligned}
    (x, y) \rightarrow \begin{bmatrix} x \\ y \\ 1 \end{bmatrix} 
\hspace*{8mm}
(x, y, z) \rightarrow  \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix}\end{aligned}$$
In order to convert back from homogeneous coordinates to standard
coordinates, we simply divide them with the third dimension. Note that
the equality between a vector and its homogeneous coordinates only
exists when the final coordinate equals 1: $$\begin{aligned}
    \begin{bmatrix} x \\ y \\ w \end{bmatrix}  \rightarrow (\dfrac{x}{w}, \dfrac{y}{w})
\hspace*{8mm}
\begin{bmatrix} x \\ y \\ z \\ w \end{bmatrix}  \rightarrow (\dfrac{x}{w}, \dfrac{y}{w}, \dfrac{z}{w})\end{aligned}$$
Using homogeneous coordinates, we can re-formulate the previous
projection equation in Cartesian coordinates: $$\begin{aligned}
    P = (x, y, z) \rightarrow P' = (f \dfrac{x}{z}, f \dfrac{y}{z})\end{aligned}$$
into homogeneous coordinates: $$\begin{aligned}
    P' = \begin{bmatrix} f x \\ f y \\ z \end{bmatrix} 
= \begin{bmatrix}
f & 0 & 0 & 0\\
0 & f & 0 & 0\\
0 & 0 & 1 & 0
\end{bmatrix} 
\begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} \end{aligned}$$ These
equations are exactly the same, but now the whole process is linear
because we can write down the coordinates by multiplying the vector with
a 3x4 matrix $M$. We term this matrix as the **projection matrix**,
where parameter $f$ is the focal length. In short, we can write the
projection equation as

$$\begin{aligned}
    P' = M P \hspace{8mm} 
M = \begin{bmatrix}
f & 0 & 0 & 0\\
0 & f & 0 & 0\\
0 & 0 & 1 & 0
\end{bmatrix} , P = \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} \end{aligned}$$
where we now map a 4D space into a 3D space.

Applications
------------

Pinhole cameras have important applications in both object recognition
and image compositing. Using a 3D representation, we are able to account
for objects that are farther away. Specifically, we can tell objects are
farther away because they have a smaller scale. This is very important
in autonomous driving applications because the driver would want to know
if objects being detected are nearby or far away. For image composition,
if you would like to insert an object into an image, the 3D projection
allows you to properly scale the inserted image depending on where it
needs to be inserted. A few examples with pictures of people inserted at
the proper scale ratio are shown below. The individuals inserted are a
larger size relative to those farther in the background prior to
insertion.\

![image]({{ site.baseurl }}/assets/images/image_scale.png =100x100)\
*(image taken from CS131 Lecture 17)*

![image]({{ site.baseurl }}/assets/images/depth_probing1.png =100x100) ![image]({{ site.baseurl }}/assets/images/depth_probing3.png =100x100)\
*(image taken from screenshots at
http://grail.cs.washington.edu/projects/shadow/)*

Intrinsic Assumptions
---------------------

There are a number of intrinsic assumptions about the camera that are
made about $M$ in the projection $P'$ introduced above.
$$\begin{aligned}
P' &= MP \\
&= \begin{bmatrix}
f & 0 & 0 & 0\\
0 & f & 0 & 0\\
0 & 0 & 1 & 0
\end{bmatrix} 
\begin{bmatrix}
x\\
y\\
z\\
1
\end{bmatrix}\end{aligned}$$ We can define a matrix $K$, which is
referred to as the matrix of intrinsic parameters or the camera
intrinsics. $$\begin{aligned}
K = \begin{bmatrix}
f & 0 & 0 \\
0 & f & 0 \\
0 & 0 & 1 
\end{bmatrix}\end{aligned}$$ Which allows us to state the projection
matrix in compact form $$\begin{aligned}
P' &= K \begin{bmatrix} I & 0 \end{bmatrix} P\end{aligned}$$ There are
three main assumptions we make about $M$:

-   Note that $f$ is equal in both dimensions, making the assumption
    that it is a unit aspect ratio.

-   The optical center is assumed to be at $(0,0)$

-   Assume there is no skew

\
These assumptions work in an ideal world. In order to apply the
projection matrix to real world images, we need to relax these
assumptions. Specifically, we can:

-   Say the optical center is at $(u_0, v_0)$

-   Assume rectangular pixels instead of square pixels. This means
    adjusting the focal length to be different in each dimension, we
    will refer to this as $\alpha$ and $\beta$.

-   Allow for some skew, we will call this $s$.

### Removing the Optical Center Assumption

We can generalize from the optical center being at $(0, 0)$ to having
the optical center at $(u_0, v_0)$. We update our projection
transformation, more specifically matrix $K$, in a corresponding manner:

$$\begin{aligned}
K = \begin{bmatrix}
f & 0 & u_0 \\
0 & f & v_0 \\
0 & 0 & 1 
\end{bmatrix}\end{aligned}$$ So we have:

$$\begin{aligned}
P' = K \begin{bmatrix} I & 0 \end{bmatrix} P \rightarrow
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} = \begin{bmatrix}
f & 0 & u_0 & 0 \\
0 & f & v_0 & 0 \\
0 & 0 & 1   & 0
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}\end{aligned}$$

### Removing the Square Pixel Assumption

If the image plane is not square but rectangular, we can assume
different focal lengths in the vertical and horizontal directions
$\alpha$ and $\beta$. Like before we update our matrix $K$

$$\begin{aligned}
K = \begin{bmatrix}
\alpha & 0 & u_0 \\
0 & \beta & v_0 \\
0 & 0 & 1 
\end{bmatrix}\end{aligned}$$ this results in a projection transformation
of

$$\begin{aligned}
P' = K \begin{bmatrix} I & 0 \end{bmatrix} P \rightarrow
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} = \begin{bmatrix}
\alpha & 0 & u_0 & 0 \\
0 & \beta & v_0 & 0 \\
0 & 0 & 1   & 0
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}\end{aligned}$$

### Removing the no skew assumption

To introduce some amount of skew we can introduce a parameter $s$ which
starts to make each of the projected horizontal and vertical distances
be a combination of $x$ and $y$. The updated K matrix is:

$$\begin{aligned}
K = \begin{bmatrix}
\alpha & s & u_0 \\
0 & \beta & v_0 \\
0 & 0 & 1 
\end{bmatrix}\end{aligned}$$ And the updated projection transformation
is:

$$\begin{aligned}
P' = K \begin{bmatrix} I & 0 \end{bmatrix} P \rightarrow
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} = \begin{bmatrix}
\alpha & s & u_0 & 0 \\
0 & \beta & v_0 & 0 \\
0 & 0 & 1   & 0
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}\end{aligned}$$

Extrinsic Assumptions
---------------------

Whereas intrinsic assumptions are those that are fixed to a particular
camera, there are other camera related parameters which determine a
final image but which we can vary outside of the camera, we call those
parameters/assumptions Extrinsic.\

### Real world Camera: Translating from origin

Instead of assuming the camera is located at $(0, 0, 0)$ assume it's
located at $(t_x, t_y, t_z)$. The projection transformation, after
taking into account the new camera translation:

$$\begin{aligned}
P' = K \begin{bmatrix} I & \bar{t} \end{bmatrix} P \rightarrow
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} = \begin{bmatrix}
\alpha & s & 0 & t_x \\
0 & \beta & 0 & t_y \\
0 & 0 & 1   & t_z
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}\end{aligned}$$

### Real world Camera: Rotating the camera

Counter clockwise rotation of the camera around each of the three
coordinate axes $(x, y, x)$ can be characterized by three corresponding
angles of rotation around the corresponding axis:
$(\alpha, \beta \gamma)$. Rotation of a point around an axis can be
described with a matrix transformation. So for each of the three
rotations we can define a separate rotation transformation:

$$\begin{aligned}
R_x(\alpha) &= \begin{bmatrix}
1 & 0 & 0 \\
0 & cos(\alpha) & -sin(\alpha) \\
0 & sin(\alpha) & cos(\alpha)
\end{bmatrix} \\
R_y(\beta) &= \begin{bmatrix}
cos(\beta) & 0 & \sin(\beta) \\
0 & 1 & 0 \\
-sin(\beta) & 0 & cos(\beta)
\end{bmatrix} \\
R_z(\gamma) &= \begin{bmatrix}
cos(\gamma) & -sin(\gamma) & 0 \\
sin(\gamma) & cos(\gamma)  & 0 \\
0 & 0 & 1
\end{bmatrix}\end{aligned}$$

### A Generic Projection Matrix

We can multiply these matrices together, and update the resulting
projection matrix, note that instead of an identity matrix $I$ we have a
rotation matrix

$$\begin{aligned}
P' = K \begin{bmatrix} R & \bar{t} \end{bmatrix} P \rightarrow
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} =  \begin{bmatrix}
\alpha & s & u_0 \\
0 & \beta & v_0 \\
0 & 0 & 1  
\end{bmatrix}
\begin{bmatrix}
r_{11} & r_{12} & r_{13} \\
r_{21} & r_{22} & r_{23} \\
r_{31} & r_{32} & r_{33} \\
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}\end{aligned}$$ Here $r_{ab}$ refers to the entry in the
$a$ row and $b$ column of the matrix $R_x R_y R_z$.\
Note that we have 5 degrees of freedom from the camera intrinsic
parameters (2 coordinates for the center of the camera, an angle of
skew, and 2 focal lengths) and 6 degrees of freedom from the camera
extrinsic parameters (3 angles of rotation and 3 coordinates of
translation)

Orthographic Projection
-----------------------

This is a special case of perspective projection, where the distance
between the Center of Projection (COP) to the image plane is infinite.
It's also called parallel projection because parallel lines are drawn
from the object's vertices to the image plane such that each parallel
line is orthogonal to the image plane. The projection matrix for this
type of projection is:

$$\begin{aligned}
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} =  \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix} = \begin{bmatrix}
x \\ 
y \\ 
1
\end{bmatrix} \to \begin{bmatrix}
x \\ 
y
\end{bmatrix}\end{aligned}$$ Note that size does not change with
distance from the camera since there is no scale factor as illustrated
below.

![image]({{ site.baseurl }}/assets/images/Orthogonal_Perspective.JPG =100x100)\
*(Image taken from CS131 Lecture 17 slides)*

Scaled Orthographic Projection
------------------------------

Scaled orthographic projection, also known as \"weak perspective\",
occurs when the object dimensions are small compared to the distance to
the camera. The corresponding projection matrix is:

$$\begin{aligned}
w \begin{bmatrix}
u \\
v \\
1
\end{bmatrix} =  \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & s
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix} = \begin{bmatrix}
x \\ 
y \\ 
s
\end{bmatrix} \to \begin{bmatrix}
\frac{x}{s} \\ 
\frac{y}{s} \\ 
1
\end{bmatrix} \to \begin{bmatrix}
\frac{x}{s} \\ 
\frac{y}{s} \\ 
\end{bmatrix} \end{aligned}$$ The use of the constant $s$ rather than
the $1$ in $\S \, 4.7$ is put into effect through the reversal of
homogeneous coordinates to create a scaling factor of $\frac{1}{s}$ for
each of the coordinates.

Field of View (Zoom)
--------------------

Zooming into an area will enlarge corresponding objects, but it will
narrow the field of view as illustrated in the graphic below.

![image]({{ site.baseurl }}/assets/images/Field_of_Zoom.JPG =100x100)\
*(Image taken from CS131 Lecture 17 slides)*

References
==========

Wu, Jiajun “Camera Models.” CS 131:  Computer Vision; Foundations and Applications.  Stanford University.  Palo Alto, CA. November 2020.  Lecture.Wang, Yifan, et al.  

“People as Scene Probes.” Computer Vision – ECCV 2020 Lecture Notes in ComputerScience, 2020, pp.  438–454., doi:10.1007/978-3-030-58607-226.http://grail.cs.washington.edu/projects/shadow/“

Depth of Field - Depth of Focus amp; Circles of Confusion - II.”Introduction,www.theimage.com/digitalphoto2/index7b.html.
