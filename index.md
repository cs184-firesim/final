---
layout: default
---

# Final Report

## Summary

In this project, we achieved real time simulation and rendering of fire effects in both 2D and 3D. 
Our implementation utilized Unity post processing and HLSL shaders as the programming platform, and we adopted popular techniques in noise generation, physical simulation and volumetric rendering. 
Our 2D fire is implemented with panning Voronoi noise and Perlin noise, while our 3D fire relies on a custom fluid-simulation and ray-marching procedure. 
We measured our rendering effects and performance on an NVIDIA 2060 graphics card and obtained near real-time results.

## Technical Approach

### 2D Fire

We multiplied Voronoi noise and Perlin noise textures and interpolated their product with a standard u-v texture. 
We then took Gaussian Blob samples to simulate the features of fire. Lastly, we applied a color gradient to give an orange color to the blob.

<div align="middle">
<img src="assets/images/sim_pipeline.png" align="middle" width="480px" />
<figcaption align="middle"> Visualization of the simulation and rendering pipeline. </figcaption>
</div> 

### 3D Fire

#### Simulation

We decided to use 3D textures to hold different attributes that describe a fire. In our simulation, we calculated the corresponding values for velocity, smoke density, temperature, and fuel level in each cell of a 3D voxelized grid.

We based our simulation off the Navier Stokes equation for fluid dynamics:

<div align="center">
<img src="assets/images/formula.png" width="480px" />
<figcaption align="middle">  </figcaption>
</div> 

In the formula, u is the velocity, p is the pressure, ρ is the density of the molecule mass, and f is the external force on molecules. 
The first term represents the advection, which is the velocity of a fluid that causes the fluid to transport objects, 
densities, and other quantities along with the flow. The term inside the parenthesis is the divergence, which represents the rate at which density exits the region.
The second term simulates how pressure gathers and generates force and provides accelerations to the surrounding molecules. 

For each time step, we compute the advection and divergence based on the interaction between neighboring voxels, 
and propagate the changes in temperature, pressure, and velocity correspondingly. 
We then update the values in each 3D texture and render the resulting volume to the screen with the rendering pipeline. 

For the external force field of the Navier Stokes equation, we simulated both buoyant force and vorticity force using the following equations:

<div align="middle">
<img src="assets/images/temperature.png" align="middle" width="300px"/>
<figcaption align="middle"> Formula for simulating buoyancy</figcaption>
</div> 

<div align="middle">
<img src="assets/images/vorticity-0.jpg" align="middle" />
<figcaption align="middle"> Formula for simulating vorticity (1/3)</figcaption>

<img src="assets/images/vorticity-1.jpg" align="middle" />
<figcaption align="middle"> Formula for simulating vorticity (2/3)</figcaption>

<img src="assets/images/vorticity-2.jpg" align="middle" />
<figcaption align="middle"> Formula for simulating vorticity (3/3)</figcaption>
</div>  

The buoyant force is influenced by temperature and density, and it changes the velocity of molecules to make the simulation more realistic. With a higher temperature, the molecules will rise with a larger velocity. 
The other force that we applied to our molecules is vorticity force. This force helps us restore some of the curling behavior of smoke that was lost due to the discrete nature of the simulation.

#### Rendering

## Results


<div align="middle">
<img src="assets/images/fire.png" align="middle" width="480px" />
<figcaption align="middle"> Rendering Result </figcaption>
</div> 


