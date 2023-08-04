# Title: Rapport An Exploration of the Implementation of NeRF with Unreal Engine 5

## Table of Content
- Abstract
- Introduction
- Nerf
- UnrealEngine 5
- Nerf in Unreal Engine
- Explored Technologies
- Other Relevant Technologies
- Conclusion

## Abstract
## Introduction
Neural radiance fields (NeRF) are a new and emerging technology that has the potential to revolutionize the way we create and interact with 3D content. NeRFs are a type of Machine model that can be trained to represent a scene's 3D geometry and appearance from a set of 2D images. Once trained, a NeRF can be used to generate novel views of the scene from any angle and create interactive 3D experiences.
The current state of NeRF research is rapidly evolving. In the past few years, there have been significant advances in the accuracy and efficiency of NeRF models. As a result, NeRFs are now being used in a variety of applications, including robotics, computer graphics, and virtual reality.

This report delves into the promising prospects of Neural Radiance Fields (NeRF) in its application within Equinor. Initially executed as a summer intern project, the investigation provided a proof-of-concept emphasizing the practicality of deploying NeRF in creating digital twins. To bring this concept to life, Unreal Engine 5 was employed as the physics engine underpinning the NeRF models.
The outcomes of this initiative were encouraging, indicating that NeRF holds significant potential to become an invaluable tool within Equinor's arsenal. The report concludes with a discussion the future possibilities for NeRF at Equinor.


  
## Nerfs

## Unreal Engine

### NeRF in Unreal Engine
#### Volinga
#### Requirments

## Explored Technologies

### Instant-NGP - [GitHub](https://github.com/bycloudai/instant-ngp-Windows)
### NeRFStudio - [GitHub](https://github.com/equinor/eit-nerfstudio)
- Nerfacto
- Volinga

### MERF - did not work
### LocalRF
Was hard to even make the code from the repo work. The documentation was bad. Hard to even run. Additionally, when we got it to run it took forever to train. The output did not look like the paper at all. Would be interesting to integrate if we could travel in any path and training was quicker.

Learning, always be skeptical of new technology. If it's from a credible university or company it does not matter. It will be hard to replicate.

## Problem with all NeRF models: 
have to get camera positions. Normally done using colmap, but this takes quite some time. Can use other applications or use Lidar data, but then you need special hardware. iPhones have Lidar capabilities and can use certain apps, android phones don’t have this.

## Volinga - Completely new technology, plugin works, exporter works
- Helpful, updated their plugin after we had a request for removing collision of the Volinga nerf actor
- Active on Discord

Easy to export NeRF chkpt-file to nvol-file to use in Unreal. The site is connected to the cloud, so you can't train any sensitive data using it. Have to get an enterprise license to be able to train locally on their desktop app. Have not tested it yet, but we assume it works the same as the site. When you use the site, you can also input a video, and they can train the model for you and export the nvol-file. When you use the desktop app you can only input chkpt-files, this means you have to train the model locally.

Only works with NeRFStudio version 0.3.1. Otherwise the chkpt-file is not compatible with the Volinga exporter.

## Volinga with Unreal
A Volinga nerf actor which stores the nerf model. Can size it, change scale. This means you can get a lifelike size so when you walk around in first person you don't feel too small or too large.

Had some problems with the plugin in earlier versions, the newest version is more stable.

One problem is that you can only have one Volinga NeRF actor in one level, so stitching rooms or buildings together requires multiple levels and NeRF actors.

Each room is its own level with its own NeRF model, and going from one room to another is done by having a trigger point that opens another level and spawns in the player at a preset spawn point.

There is probably an easier way to do it than the way we did it, but as we were totally new to Unreal Engine, this was the best we managed to do.

Volinga does not work with VR yet, but they have said that they will add this functionality later.

## Luma - Expensive, don't think it will work as well with rooms as it does with objects. Don't know how it works with Unreal Engine.

## PolyCam - No one had IOS so we couldn't test it.

## Unreal Engine

### Multiplayer plugin (did not work with Volinga)
- Worked decently, not very easy to use and to set up. We had some problems with persistence and with using Git. Recommend watching the video from unreal on how it is used. It does work well if you are using traditional unreal engine tools.
- Git support is in Beta, works decently, but we have experienced some issues and some merge conflicts. Fixing merge conflicts doesn't work, we had to revert some changes.

## Oculus
Does not work in enterprise mode for VR and unreal engine. Struggled to connect to the computer wirelessly in enterprise mode. All the following problems were solved when it was set to consumer mode.

## HTC Vive
Difficult to set up, need to set up the sensors.

## SteamVR
Works with Oculus, but not enterprise Oculus.

## GoPro
Camera mode: cinematic, wide, ultrawider, and hyperwide.
Hyperwide does not work, quality shit, Could potentially work for very large environments.
Ultrawide
Works well with large environments, similar to wide.
Wide
Similar results to ultrawide, better for large rooms.
Normal best for normal nerf or small rooms.

Used GoPro quickpro app: easy to use and export pictures.
GoPro does not produce better nerfs than a phone camera, only the wide feature that gives it an advantage for larger rooms.

## Google Pixel Camera
OK camera, it can produce OK nerfs.

## Samsung Camera
Depending on what model, it produces mid to high models.

## Other Relevant Technology
The following technologies can be relevant for exploration, unfortunately, we did not get to explore them.

## Conclusion

