---
title: Proposal
---

## Proposal
### Summary
I will implement the irradiance map solution of [CloudLight](https://research.nvidia.com/publication/cloudlight-system-amortizing-indirect-lighting-real-time-rendering/) and compare performance and quality tradeoffs to local computation.

### Background
Cloud rendering is a promising platform for graphics rendering in the future. Rendering (games) in the cloud has the potential for methods that would be unreasonable for a local machine, such as possibly raytracing the entire scene to achieve a higher level of quality.

The CloudLight paper is a first attempt into rendering games in the cloud. Traditional techniques for parallel rendering don't translate well towards rendering games for many clients, and as the number of clients increases much of the work becomes duplicated. With many clients connecting to a single cloud, this allows us to perform operations that would traditionally be too expensive for a single user, and amortize the cost across many clients. One such possibility for amortiziation is Global Illumination.

The irradiance map solution proposed is comprised primarily of two parts:

1. A cloud side raytracer which aggregates diffuse reflections to a global illumination lightmap, which is then H.264 encoded and streamed to the client as a video.
2. The client side renderer, which is just a typical renderer with lightmap support. The only difference here is the client now needs to decode the H.264 stream, and update the lightmap as it receives them.

### Challenge
Launching a separate instance of a raytracer for every viewport is clearly inefficient if multiple viewports are sharing a scene. We need to break down the problem into portions that are viewport independent and those that aren't, allowing us to amortize the cost of operations across many viewports. Global illumination is one component of a scene that is viewport independent, and as such can be amortized across clients.

Global illumination is very expensive to compute, and requires a significant amount of processing power on the client side. As such, without a sufficient GPU it becomes impossible to compute global illumination while keeping real time framerates. However global illumination is a very attractive feature to have, as it increases the realism of a rendered scene.

Notable challenges would be the amount of components that need to be implemented: a remote side raytracer, networking code, as well as the client side code to piece information together and incorporate it into its rendering pipeline.

### Resources
In a similar vein to the paper, multiple frameworks would be used to speed up development times of the various components.

Raytracing  -   OptiX
Networking  -   Asio / SDL_net
Window      -   SDL / GLFW
Graphics    -   OpenGL
H.264       -   C++ / libav / FFmpeg

Client side would probably be my laptop. Access to a machine with a beefy GPU that I could run at a whim (Gates / latedays / other) would be used for the cloud side.

Code would be written from scratch.

### Platform
The platform chosen is due to tradeoffs between performance and creation time. Using OptiX will hopefully speed up creation of the cloud side raytracer. The remaining platform components are typical of games, and since CloudLight is targeted towards rendering games it makes sense to use a system similar to this.

### Goals and Deliverables
Plan to achieve:  
Demonstrate a system with multiple viewports interacting with a single remote server, and compare performance to a system where work is not amortized.

Hope to achieve:  
Integrate this with Yong's system

### Schedule
April 1: Become confused  
April 4: Talk to Yong  
April 5: Talk to Kayvon  
April 5: Formulate a concrete project idea  
April 9: Crude raytracer in OptiX  
April 16: Crude renderer in OpenGL  
April 22: Irradiance map creation in OptiX  
April 29: Implement irradiance map in OpenGL  
May 6: Communication code between host and client  
May 9: Feel accomplished (hopefully)