# StitchedNeRF_2
This project provides a unique 3D exploration experience through the use of Neural Radiance Fields (NeRFs) and Unreal Engine 5. We've taken multiple NeRF models, exported them into Unreal Engine 5, and stitched them together to create one extensive NeRF model. This combined model represents a detailed replica of the Equinor Business Center that players can navigate and explore.

**Requirements**
1. Unreal Engine 5
2. Volinga Plugin
3. (Optional)GPU to handle NeRF training

**Setup and Running the Project**
1. Install Unreal Engine 5: If you haven't already, download and install Unreal Engine 5 from the [Official Website](https://www.unrealengine.com/en-US).
2. Get the Volinga Plugin: Visit the [Volinga.ai](https://volinga.ai/) website and download the Volinga plugin.
3. Enable Volinga Plugin in Unreal Engine 5: Open Unreal Engine 5 and navigate to the plugin settings. Search for the Volinga plugin and enable it. You might need to restart Unreal Engine for the changes to take effect.
4. Open the Project: Navigate to the location of the StichedneRF_2.uproject file in your file explorer. Double-click the file to open the project in Unreal Engine 5.
5. Explore Equinor Business Center: Upon successfully loading the project, you can start exploring the 3D environment of the Equinor Business Center.

We hope you enjoy this immersive experience of exploring the Equinor Business Center in Unreal Engine 5. Happy exploring!

**The Following presents a comprehensive summary of our research findings and achievements during our summer internship project for [Equinor](https://www.equinor.com).**

# An Exploration of the Implementation of NeRF with Unreal Engine 5

Video showing the project: [https://youtu.be/MIEbp1fxDJo](https://youtu.be/I6brS7sqggk)

[![Watch the video](https://img.youtube.com/vi/I6brS7sqggk/0.jpg)](https://youtu.be/I6brS7sqggk)

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
This research delves into the potential of Neural Radiance Fields (NeRFs) for creating interactive 3D representations of real-world environments using Unreal Engine 5 and its integration within Equinor. The project, conducted as part of a summer internship at Equinor, demonstrates how NeRFs can be effectively utilized to create digital twins of complex environments.
Utilizing Volinga, a plugin designed to render NeRFs in Unreal Engine 5. the team created a digital twin of Equinors business center, each room representing an individual level containing a unique NeRF model. The project demonstrated significant potential in enabling NeRF integration within real-time rendering engines and further applications within the Industrial Metaverse. The research highlights the feasibility of using NeRFs and Unreal Engine 5 for industrial applications and interactive 3D experiences

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

### Advantages of NeRF
A distinct advantage of NeRF models lies in their quick training speed. NeRFs demonstrate an impressive ability to train quickly compared to other traditional techniques. Furthermore, the accessibility of NeRFs is significant. For instance, the data required to train a NeRF model can be simply obtained using a regular smartphone, eliminating the need for high-end hardware. 

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

##  🎮 NeRF in Unreal Engine

<div id="nerf-in-unreal-engine"></div>

#### Requirements
- Beefy computer
- Volinga


###  [Volinga](https://volinga.ai/) - Completely new technology, plugin works, exporter works
As of writing, Volinga is a new plugin still in beta. Volinga has a singular purpuse of making NeRF compatible with the UnrealEngine 5. It accomplishes this by converting a checkpoint file into a format (.nvol) compatible with UnrealEngine 5. Notably, Volinga accepts video inputs, trains a NeRF based on it, and converts the checkpoint file into .nvol format.  Since Volinga is a new start-up, they are very accommodating and active on Discord and email. We highly recommend contacting their team if you have any bugs or requests.

**DISCLAIMER!!**

If you upload your chkpt file or video to their website, it is connected to Volingas cloud. Any sensitive information should not be uploaded! If you need to upload sensitive information, contact them and ask for their desktop, which offers local training.

### Volinga Desktop
Volinga also offers an enterprise desktop solution. This desktop variant currently provides the same features as their website, albeit with minor modifications. The desktop version only accepts checkpoint files for export, not videos, and these checkpoint files must be trained using NeRFStudio version 0.3.1. If you use the eit-nerfstudio repo made internally in Equinor, you have to change the remote image version in the .env-file to "dromni/nerfstudio:0.3.1" and choose “2: Run prebuildt official image dromni/nerfstudio:0.3.1”



### Volinga with Unreal
For effectively incorporating the Volinga plugin with Unreal Engine 5, following the detailed guidelines provided in Volinga's documentation is advisable. 

Essentially, Volinga establishes a cubic NeRF actor that houses the NeRF model as a hologram. This cube's dimensions can be altered to excise irrelevant portions of the model, thereby eliminating any NeRF-fog. The model's scale can also be adjusted as needed. It should be noted that within Unreal Engine 5, the NeRF model lacks physical properties, functioning instead like a hologram. However, by utilizing the tools available in Unreal Engine 5 to superimpose a physical environment onto the NeRF, the model appears to possess physical properties and can interact with all items within the Unreal Engine 5 environment. While early plugin versions faced stability issues, the most recent version we examined proved significantly more stable.

A current drawback of Volinga is its limitation to a single Volinga NeRF actor per level. This creates a challenge when multiple models are required, necessitating the "stitching" of levels by placing a single model in each. Theoretically, it might be possible to stream all levels within a single world, although we have yet to test this.

In creating our business center, we designated each room as an individual level with its unique NeRF model. Transitioning from one room to another was facilitated through trigger points that initiate another level and spawn the player at a preset location. Although there may be simpler methods of achieving this, our experience with Unreal Engine was limited.

As of now, Volinga lacks compatibility with VR. However, the team has announced plans to incorporate this functionality in the future.


<div id="explored-technologies"></div>

## 🔍 Explored Technologies

#### Instant-NGP - [GitHub](https://github.com/bycloudai/instant-ngp-Windows)
It worked well, not too difficult to set up. A big upside with it is its speed, it is a lot faster than NeRFStudio. It also works with VR. We did not do anything more than exploring with it because we found no other uses, there was no way to incorporate it into Unreal Engine. 

#### NeRFStudio - [GitHub](https://github.com/equinor/eit-nerfstudio)
Very easy to use and a lot of documentation. We tried both running NeRFStudio directly, and using the Docker image internally from Equinor, and we preferred using the Docker image. We used it on windows with WSL using Distro and Ubuntu. 
- Nerfacto
	- The normal way of training NeRF models
- Volinga
	- The training method that gives you the .chkpt-file you can use with the Volinga exporter. 

#### MERF - [GitHub](https://creiser.github.io/merf/)
An intriguing NeRF model, but proved impractical due to technical issues with the requirements.txt, preventing us from installing all requirements and consequently running the code.


#### LocalRF - [GitHub](https://localrf.github.io/)
The tool's poor documentation posed challenges in making the repo work. Moreover, the prolonged training time and discrepancies in output as compared to the paper rendered it unattractive. Nonetheless, if issues with the training duration and path navigation were resolved, integration might prove beneficial.


#### Multi user editor - plugin (did not work with Volinga)
- Major drawback, with the current version of Volinga.ai multiuse editor, is rendered useless.
- Worked decently, not very easy to use and to set up. We had some problems with persistence and with using Git. Recommend watching the [video](https://www.youtube.com/watch?v=MPIpOdNmNGE) from unreal on how it is used. It does work well if you are using traditional unreal engine tools.
- Git support is in Beta, works decently, but we have experienced some issues and some merge conflicts. Fixing merge conflicts doesn't work, we had to revert some changes.


#### Oculus
In enterprise mode, we experienced difficulties with VR and Unreal Engine compatibility. Connecting the headset to our computers wirelessly also presented challenges. However, switching to consumer mode resolved these issues. While we successfully established a wired connection between the headset and our PCs, wireless connectivity proved problematic on Equinor's network, though it was achievable at home.


#### HTC Vive
HTC Vive: Despite providing a quality VR experience, the setup process, especially concerning sensor arrangement, was troublesome. The cable requirement might be a drawback for some users. Oculus would be our recommendation over the HTC Vive.

#### SteamVR
SteamVR: Functioned well with Oculus but faced issues with enterprise Oculus. Used successfully to implement VR with InstantNGP.


<div id="other-relevant-technologies"></div>

## 🔧 Other Relevant Technologies
There are several other technologies that are pertinent to the field of our project and warrant further investigation. Due to various constraints, we were unable to explore these during the course of our work.

**[Luma AI](https://lumalabs.ai/):** This technology stands as a potential option, albeit with a considerable price tag that may limit its accessibility. Our preliminary analysis suggests that Luma might not perform as proficiently with room-scale models as it does with individual objects. Additionally, its compatibility and interoperability with Unreal Engine are yet to be determined, which could impact its usefulness within our project context.

**[PolyCam](https://poly.cam/):** PolyCam represents a promising avenue, particularly with its potential to bypass the need for Colmap, offering the prospect of significant time savings. Unfortunately, we were unable to carry out a practical evaluation of PolyCam as it necessitates iOS, which was not available among our team members.
<div id="conclusion"></div>

## 🏁 Conclusion
This exploration confirmed the feasibility of integrating NeRF into Unreal Engine 5, leading to a highly interactive, immersive experience. This successful demonstration serves as a testament to the potential of NeRF within an industrial setting for Equinor.

Current NeRF models may not match the high visual fidelity associated with some alternative technologies, yet they offer distinct advantages that are hard to dismiss. Particularly noteworthy is the technology's speed and accessibility, in addition to its user-friendly nature. Such attributes make NeRF appealing for fast, efficient digital twin creation and exploration. Considering that NeRF is only three years old, its current pace of advancement suggests a promising future in the rapidly evolving industrial metaverse.

Our work indicates that NeRF is a practical and powerful tool for developing immersive digital environments, opening up new possibilities for industrial applications.
