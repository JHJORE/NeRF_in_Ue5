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
Compression, coldmap, other options than coldmap

### Problem with all NeRF models: 
have to get camera positions. Normally done using colmap, but this takes quite some time. Can use other applications or use Lidar data, but then you need special hardware. iPhones have Lidar capabilities and can use certain apps, android phones don’t have this.

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


### PolyCam - No one had IOS so we couldn't test it.


### Multiplayer plugin (did not work with Volinga)
- Worked decently, not very easy to use and to set up. We had some problems with persistence and with using Git. Recommend watching the video from unreal on how it is used. It does work well if you are using traditional unreal engine tools.
- Git support is in Beta, works decently, but we have experienced some issues and some merge conflicts. Fixing merge conflicts doesn't work, we had to revert some changes.

### Oculus
Does not work in enterprise mode for VR and unreal engine. Struggled to connect to the computer wirelessly in enterprise mode. All the following problems were solved when it was set to consumer mode.

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

<div id="conclusion"></div>

## Conclusion

