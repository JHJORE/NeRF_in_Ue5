# Title: Rapport An Exploration of the Implementation of NeRF with Unreal Engine 5

## Table of Content
- [Abstract](#abstract)
- [Introduction](#introduction)
- [Nerf](#nerf)
- [UnrealEngine 5](#unrealengine-5)
- [Nerf in Unreal Engine](#nerf-in-unreal-engine)
- [Explored Technologies](#explored-technologies)
- [Other Relevant Technologies](#other-relevant-technologies)
- [Conclusion](#conclusion)

<div id="abstract"></div>

## Abstract

<div id="introduction"></div>

## Introduction
Neural radiance fields (NeRF) are a new and emerging technology that has the potential to revolutionize the way we create and interact with 3D content. NeRFs are a type of Machine Learning model that can be trained to represent a scene's 3D geometry and appearance from a set of 2D images. Once trained, a NeRF can be used to generate novel views of the scene from any angle and create interactive 3D experiences.
The current state of NeRF research is rapidly evolving. In the past few years, there have been significant advances in the accuracy and efficiency of NeRF models. As a result, NeRFs are now being used in a variety of applications, including robotics, computer graphics, and virtual reality.

This report delves into the promising prospects of Neural Radiance Fields (NeRF) in its application within Equinor. Initially executed as a summer intern project, the investigation provided a proof-of-concept emphasizing the practicality of deploying NeRF in creating digital twins. To bring this concept to life, Unreal Engine 5 was employed as the physics engine underpinning the NeRF models.
The outcomes of this initiative were encouraging, indicating that NeRF holds significant potential to become an invaluable tool within Equinor's arsenal.

<div id="nerf"></div>

## Nerfs
#### Requirement: 
- GPU to Train the NeRF model

**Neural Radiance Fields (NeRFs)** represent a novel approach for synthesizing photorealistic views of complex scenes by optimizing an underlying continuous volumetric scene function using a sparse set of input views. NeRFs are trained to represent the radiance of a scene, which is the total amount of light emitted or reflected from a point in the scene. This information can then render novel views of the scene from arbitrary viewpoints.
NeRFs are trained using a set of 2D images of a scene. NeRFs are fully-connected deep networks, taking a single continuous 5D coordinate (spatial location (x, y, z) and viewing direction (θ, φ)) as input and output a 2D coordinate: the volume density and view-dependent emitted radiance at that spatial location. The NeRF is then optimized to minimize the error of rendering a set of captured images.
NeRFs have several advantages over traditional 3D reconstruction methods:

1. They can represent scenes with complex geometry and appearance.
2. They can synthesize views from arbitrary viewpoints, even if those viewpoints were not included in the training data.
3. They can do this in real-time, making them suitable for virtual and augmented reality applications.

### Advantages of Neural Radiance Fields
A distinct advantage of NeRF models lies in their expedited training speed. NeRFs demonstrate an impressive ability to train quickly compared to other traditional techniques. Furthermore, the accessibility of NeRFs is significant. For instance, the data required to train a NeRF model can be simply obtained using a regular smartphone, eliminating the need for high-end hardware. Another beneficial attribute of NeRFs is their capability to capture shadows and reflections more effectively than other methods, leading to a more detailed and realistic representation of the 3D environment. NeRFs are also notable for maintaining relevant scale among all objects in the scene, resulting in accurate spatial relationships and depth perception, all while rending in real-time, allowing for a highly immersive experience. This makes it easy to integrate with VR and the Industrial Metaverse. Lastly, since the NeRF model is stored as values in a neural network. It is a surprisingly efficient method of compressing the file.

### Challenges with NeRF models: 
Despite the substantial advantages that NeRF models present, particular challenges persist. One such issue is the tendency for the rendered images to appear blurry, potentially leading to inaccurate point clouds and compromised visual fidelity.
The process of training NeRF models also presents a challenge regarding time consumption. Acquiring photo positions, typically performed using Colmap, can be pretty time-consuming. Although alternatives exist, such as using Lidar data or other applications, these options necessitate specific hardware. For example, while iPhones can leverage their built-in Lidar capabilities through certain apps, Android phones do not offer this feature. Therefore, if the option to substitute Colmap arises, it is highly recommended due to its potential to reduce training times.
Lastly, a common constraint in traditional NeRF implementation is the requirement for a defined center during training. The conventional usage of NeRFs leans towards object capture rather than environmental representation, demanding a clearly defined center around which to navigate during filming. Some models have been developed that do not require this, but they order highly specialized hardware, have lengthy training periods, and are challenging to replicate. As technology evolves, it is hoped that these limitations can be overcome, thereby broadening the use cases and accessibility of NeRF models.

### Google Pixel Camera
OK camera, it can produce OK nerfs.

### Samsung Camera
Depending on what model, it produces mid to high models.

<div id="unrealengine-5"></div>

## Unreal Engine

<div id="nerf-in-unreal-engine"></div>

### NeRF in Unreal Engine
#### Requirements
#### Volinga


### Problem with all NeRF models: 
have to get camera positions. Normally done using colmap, but this takes quite some time. Can use other applications or use Lidar data, but then you need special hardware. iPhones have Lidar capabilities and can use certain apps, android phones don’t have this.

### Volinga - Completely new technology, plugin works, exporter works
You use Volinga to export a .chkpt file or video/images into an .nvol file that you can use in Unreal Engine to view the nerf model. If you use the site, you have to be aware that it is connected to their coud, so they will get access to any sensitive data trained on it. They have an enterprise license you can buy that gives you access to a desktop app. In this you can train data locally, which enables sensitive data. 
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

## Explored Technologies

### Instant-NGP - [GitHub](https://github.com/bycloudai/instant-ngp-Windows)
It worked well, not too difficult to set up. A big upside with it is its speed, it is a lot faster than NeRFStudio. It also works with VR. We did not do anything more than exploring with it because we found no other uses, there was no way to incorporate it into Unreal Engine. 

### NeRFStudio - [GitHub](https://github.com/equinor/eit-nerfstudio)
Very easy to use and a lot of documentation. We tried both running NeRFStudio directly, and using the Docker image that Jonas made, and we preferred using the Docker image. We used it on windows with WSL using Distro and Ubuntu. 
- Nerfacto
	The normal way of training NeRF models
- Volinga
	The training method that gives you a .chkpt-file you can use with the Volinga exporter. 
	This required version 0.3.1. To use this version you have to change the remote image version in the .env-file to "dromni/nerfstudio:0.3.1" and choose “2: Run prebuildt official image dromni/nerfstudio:0.3.1”

### MERF - did not work
### LocalRF
Was hard to even make the code from the repo work. The documentation was bad. Hard to even run. Additionally, when we got it to run it took forever to train. The output did not look like the paper at all. Would be interesting to integrate if we could travel in any path and training was quicker.

Learning, always be skeptical of new technology. If it's from a credible university or company it does not matter. It will be hard to replicate.



### Multiplayer plugin (did not work with Volinga)
- Worked decently, not very easy to use and to set up. We had some problems with persistence and with using Git. Recommend watching the video from unreal on how it is used. It does work well if you are using traditional unreal engine tools.
- Git support is in Beta, works decently, but we have experienced some issues and some merge conflicts. Fixing merge conflicts doesn't work, we had to revert some changes.

### Oculus
Does not work in enterprise mode for VR and unreal engine. Struggled to connect to the computer wirelessly in enterprise mode. All the following problems were solved when it was set to consumer mode. We managed to connect the headset to our PCs using a cable. When we tried to connect it to our PCs wirelessly, we could not get it to work on the Equinor internet, but we made it work on networks at home. 


### HTC Vive
Difficult to set up, need to set up the sensors.

### SteamVR
Works with Oculus, but not enterprise Oculus.

### GoPro
Camera mode: cinematic, wide, ultrawider, and hyperwide.
Hyperwide does not work, quality shit, Could potentially work for very large environments.
Ultrawide
Works well with large environments, similar to wide.
Wide
Similar results to ultrawide, better for large rooms.
Normal best for normal nerf or small rooms.

Used GoPro quickpro app: easy to use and export pictures.
GoPro does not produce better nerfs than a phone camera, only the wide feature that gives it an advantage for larger rooms.


<div id="other-relevant-technologies"></div>

## Other Relevant Technology
The following technologies can be relevant for exploration, unfortunately, we did not get to explore them.

### Luma
Expensive. We don't think it will work as well with rooms as it does with objects and we don't know how of if it works with Unreal Engine.

### PolyCam
No one had IOS so we couldn't test it. Seems interesting to not have to use colmap, you can save a lot of time. 

<div id="conclusion"></div>

## Conclusion

