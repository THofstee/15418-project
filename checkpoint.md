---
title: Checkpoint
layout: default
---

## Checkpoint

### Revised Schedule
4/23: A raytracer
4/27: A parallel raytracer
4/30: Acceleration structures
5/4: Add more integrators and acceleration structures
5/7: Stretch goal of hooking back into lightmap generator
5/9: Demo

### Progress
I looked at [OptiX](https://developer.nvidia.com/optix) to try and write the cloud side. OptiX decided it didn't want to play well so I began to look at other alternatives. One of the other alternatives that was suggested was [VXGI](https://developer.nvidia.com/vxgi), so I tore apart the samples and figured out how it works, thanks to the next to nonexistant documentation. Disappointingly for an implementation that is supposedly not screen space, as far as I can tell I can only get a screen space texture out of the black box implementation. Unsure about what to do for backend at the moment.

For the front end, I have a crude OpenGL implementation of a renderer that would fit in with the backend as described the the CloudLight paper.

### Goals and Deliverables
Front end isn't pretty, but it works. Mainly this leaves the backend. Could I produce all the deliverables? Yeah probably, but that won't be enough. Nice to haves? Don't think so. It's still not completely clear how they would fit in either.

### Demo
Graphs comparing performance and quality or demo of a renderer.

### Issues
The main thing that is concerning me is that honestly this doesn't really feel like a parallel project right now. It feels like a graphics project. Sure, if I continue in this direction I could get to the point where I'm demonstrating amortization over several clients for an otherwise prohibitively expensive operation, but I want to get more out of this.

I talked to Kayvon and he agreed with this. I need to make some part of the system fit to be in a parallel project. I could do the front end, but this feels less like parallel and more like graphics again to me. I'm considering writing a (CUDA?) raytracer at this point for the backend, because I know for sure that would satisfy the parallel requirement, and I could probably hook it back into this system if I wanted. But then the project becomes more of a raytracer project than CloudLight (maybe not a bad thing).