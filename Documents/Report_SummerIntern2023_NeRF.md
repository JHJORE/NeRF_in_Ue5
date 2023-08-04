# Title: An Exploration of the Implementation of NeRF with Unreal Engine 5

## Table of Content
- [📑 Abstract](#abstract)
- [🚀 Introduction](#introduction)
- [🔮 NeRF](#nerf)
- [🎮 Unreal Engine 5](#unrealengine-5)
- [🎮 NeRF in Unreal Engine](#nerf-in-unreal-engine)
- [🔍 Explored Technologies](#explored-technologies)
- [🔧 Other Relevant Technologies](#other-relevant-technologies)
- [🏁 Conclusion](#conclusion)


<div id="abstract"></div>

## 📑 Abstract

<div id="introduction"></div>

## 🚀 Introduction
Neural radiance fields (NeRF) are a new and emerging technology that has the potential to revolutionize the way we create and interact with 3D content. NeRFs are a type of Machine Learning model that can be trained to represent a scene's 3D geometry and appearance from a set of 2D images. Once trained, a NeRF can be used to generate novel views of the scene from any angle and create interactive 3D experiences.
The current state of NeRF research is rapidly evolving. In the past few years, there have been significant advances in the accuracy and efficiency of NeRF models. As a result, NeRFs are now being used in a variety of applications, including robotics, computer graphics, and virtual reality.

This report delves into the promising prospects of Neural Radiance Fields (NeRF) in its application within Equinor. Initially executed as a summer intern project, the investigation provided a proof-of-concept emphasizing the practicality of deploying NeRF in creating digital twins. To bring this concept to life, Unreal Engine 5 was employed as the physics engine underpinning the NeRF models.
The outcomes of this initiative were encouraging, indicating that NeRF holds significant potential to become an invaluable tool within Equinor's arsenal.

<div id="nerf"></div>

## 🔮 Nerf
#### Requirement: 
- GPU to Train the NeRF model

**Neural Radiance Fields (NeRFs)** represent a novel approach for synthesizing photorealistic views of complex scenes by optimizing an underlying continuous volumetric scene function using a sparse set of input views. NeRFs are trained to represent the radiance of a scene, which is the total amount of light emitted or reflected from a point in the scene. This information can then render novel views of the scene from arbitrary viewpoints.
NeRFs are trained using a set of 2D images of a scene. NeRFs are fully-connected deep networks, taking a single continuous 5D coordinate (spatial location (x, y, z) and viewing direction (θ, φ)) as input and output a 2D coordinate: the volume density and view-dependent emitted radiance at that spatial location. The NeRF is then optimized to minimize the error of rendering a set of captured images.
NeRFs have several advantages over traditional 3D reconstruction methods:

1. They can represent scenes with complex geometry and appearance.
2. They can synthesize views from arbitrary viewpoints, even if those viewpoints were not included in the training data.
3. They can do this in real-time, making them suitable for virtual and augmented reality applications.

### Advantages of Neural Radiance Fields
A distinct advantage of NeRF models lies in their expedited training speed. NeRFs demonstrate an impressive ability to train quickly compared to other traditional techniques. Furthermore, the accessibility of NeRFs is significant. For instance, the data required to train a NeRF model can be simply obtained using a regular smartphone, eliminating the need for high-end hardware. 

Another beneficial attribute of NeRFs is their capability to capture shadows and reflections more effectively than other methods, leading to a more detailed and realistic representation of the 3D environment. NeRFs are also notable for maintaining relevant scale among all objects in the scene, resulting in accurate spatial relationships and depth perception, all while rending in real-time, allowing for a highly immersive experience. This makes it easy to integrate with VR and the Industrial Metaverse. Lastly, since the NeRF model is stored as values in a neural network. It is a surprisingly efficient method of compressing the file.

### Challenges with NeRF models: 
Despite the substantial advantages that NeRF models present, particular challenges persist. One such issue is the tendency for the rendered images to appear blurry, potentially leading to inaccurate point clouds and compromised visual fidelity. The biggest time constraint for NeRF is the pre-processing of training data. Sorting a photo position relative to other photos is typically performed using Colmap. Although alternatives exist, such as using Lidar, these options necessitate specific hardware. For example, while iPhones can leverage their built-in Lidar capabilities,  Android phones do not offer this feature. Therefore, if the option to substitute Colmap arises, it is highly recommended.

Lastly, a common constraint in traditional NeRF implementation is the requirement for a defined center during video filming. The conventional usage of NeRFs leans towards object capture rather than environmental representation, demanding a clearly defined center around which to navigate during filming. Some models have been developed not requiring this, such as  [LocalRF](https://github.com/facebookresearch/localrf), but they require highly specialized hardware, have long training periods, and are challenging to replicate the code. As technology evolves, it is hoped that these limitations can be overcome, thereby broadening the use cases and accessibility of NeRF models.

### How to Capture a Good NeRF
The methods to capture a NeRF vary depending on the subject of interest. Leveraging the default high-resolution phone camera setting is ideal for object capture. It is advisable to film the object of interest three times from distinct perspectives. The initial filming should be done at the standard level, followed by a low-angle shot, and finally, from a high angle. This ensures comprehensive coverage of all possible angles of the object.

On the other hand, capturing an environment requires a different strategy. The size of your area largely determines the approach, particularly influencing the degree of wide-angle used. With larger spaces, a greater wide angle is needed. This decision, however, comes with a trade-off: although a wide angle helps minimize blur and random point clouds, it might reduce the resolution of the NeRF. However, to maximize the quality of your NeRF model, it's advisable to implement an algorithm that eliminates blurry photos from your training data before initiating the training process. This pre-processing step significantly enhances the resultant NeRF's quality. Below is a list of commonly used cameras and their drawbacks with filming NeRF

#### iPhone
The iPhone currently stands as the premier choice for smartphone cameras.
#### Google Pixel Camera
While the Google Pixel camera can produce satisfactory NeRFs, its reliance on post-processing to compensate for hardware limitations can cause issues. The post-processing may enhance photos for human observers, but it can mislead the AI during model training, leading to increased blurring.
#### Samsung Camera
The performance of Samsung's camera varies depending on the model, generally producing mid to high-end results. Nonetheless, in most instances, the iPhone camera tends to surpass the performance of Samsung's offering.
#### GoPro
While the GoPro camera may not surpass smartphones in terms of quality, it provides a range of unique features. For GoPro, we suggest using the modes: Cinematic, Wide, Ultra-wide, and Hyper-wide. 

Hyper-wide typically offers little benefit and might only help capture extremely expansive environments. In contrast, Ultra-wide and Wide modes often yield excellent results, particularly for larger environments. The normal setting is most suitable for standard NeRFs or smaller rooms.

<div id="unrealengine-5"></div>

## 🎮 Unreal Engine

<div id="nerf-in-unreal-engine"></div>

### 🎮 NeRF in Unreal Engine
#### Requirements
#### - Beefy computer
#### - Volinga


### Volinga - Completely new technology, plugin works, exporter works
You use Volinga to export a .chkpt file or video/images into an .nvol file that you can use in Unreal Engine to view the nerf model. If you use the site, you have to be aware that it is connected to their cloud, so they will get access to any sensitive data trained on it. They have an enterprise license you can buy that gives you access to a desktop app. With the desktop app you can train data locally, where you can use sensitive data. 
When training on the site, you can upload photos, videos, and .chkpt-files. When using the desktop app you can only use .chkpt-files. Using NeRFStudio is necessary when using the desktop app to train the .chkpt-file. 

During our weeks it only worked with NeRFStudio version 0.3.1. Otherwise the chkpt-file is not compatible with the Volinga exporter. NeRFStudio or Volinga might have updated their applications later. 

- Helpful, updated their plugin after we had a request for removing collision of the Volinga nerf actor
- Active on Discord


### Volinga with Unreal
Volinga has a plugin you can download on their website. After you download it you have to put it in the Plugin-folder of Unreal Engine. This gives the Volinga nerf actor which stores the nerf model. You can change size of the cube to remove the parts of the model that aren’t relevant, taking away all the NeRF-fog. You can also change the scale of the model. 
The earlier version of the plugin had some problems, but the newest version we teste was more stable. 
One problem with the plugin is that you can only have one Volinga NeRF actor in one level, so stitching rooms or buildings together requires multiple levels and NeRF actors.

The way we made the business center was by making each room its own level with its own NeRF model. Going from one room to another was done by having a trigger point that opens another level and spawns in the player at a preset spawn point.

There is probably an easier way to do it than the way we did it, but as we were totally new to Unreal Engine, this was the best we managed to do.

Volinga does not work with VR yet, but they have said that they will add this functionality later.


<div id="explored-technologies"></div>

## 🔍 Explored Technologies

### Instant-NGP - [GitHub](https://github.com/bycloudai/instant-ngp-Windows)
It worked well, not too difficult to set up. A big upside with it is its speed, it is a lot faster than NeRFStudio. It also works with VR. We did not do anything more than exploring with it because we found no other uses, there was no way to incorporate it into Unreal Engine. 

### NeRFStudio - [GitHub](https://github.com/equinor/eit-nerfstudio)
Very easy to use and a lot of documentation. We tried both running NeRFStudio directly, and using the Docker image that Jonas made, and we preferred using the Docker image. We used it on windows with WSL using Distro and Ubuntu. 
- Nerfacto
	- The normal way of training NeRF models
- Volinga
	- The training method that gives you a .chkpt-file you can use with the Volinga exporter. 
	- This required version 0.3.1. To use this version you have to change the remote image version in the .env-file to "dromni/nerfstudio:0.3.1" and choose “2: Run prebuildt official image dromni/nerfstudio:0.3.1”

### MERF
Did not work
### LocalRF
Was hard to even make the code from the repo work. The documentation was bad. Hard to even run. Additionally, when we got it to run it took forever to train. The output did not look like the paper at all. Would be interesting to integrate if we could travel in any path and training was quicker.

Learning, always be skeptical of new technology. If it's from a credible university or company it does not matter. It will be hard to replicate.



### Multiplayer plugin (did not work with Volinga)
- Worked decently, not very easy to use and to set up. We had some problems with persistence and with using Git. Recommend watching the video from unreal on how it is used. It does work well if you are using traditional unreal engine tools.
- Git support is in Beta, works decently, but we have experienced some issues and some merge conflicts. Fixing merge conflicts doesn't work, we had to revert some changes.

### Oculus
Does not work in enterprise mode for VR and unreal engine. Struggled to connect to the computer wirelessly in enterprise mode. All the following problems were solved when it was set to consumer mode. We managed to connect the headset to our PCs using a cable. When we tried to connect it to our PCs wirelessly, we could not get it to work on the Equinor internet, but we made it work on networks at home. 


### HTC Vive
Difficult to set up, need to set up the sensors. You have to use cable. A good headset, but we would recommend Oculus

### SteamVR
Works with Oculus, but not enterprise Oculus. We used it to get VR to work with InstantNGP


<div id="other-relevant-technologies"></div>

## 🔧 Other Relevant Technologies
The following technologies can be relevant for exploration, unfortunately, we did not get to explore them.

### Luma
Expensive. We don't think it will work as well with rooms as it does with objects and we don't know how of if it works with Unreal Engine.

### PolyCam
No one had IOS so we couldn't test it. Seems interesting to not have to use colmap, you can save a lot of time. 

<div id="conclusion"></div>

## 🏁 Conclusion

