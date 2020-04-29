---
layout: default
---

# Milestone

## Accomplishment 

We decided to use 3D textures to hold our different attributes that describe a fire. In our simulation, we calculated the corresponding values for velocity, pressure, and temperature for voxels of fire molecules.

Here is the formula that we used: 

<div align="center">
<img src="assets/images/formula.png" width="480px" />
<figcaption align="middle">  </figcaption>
</div> 

In the formula, u is the velocity, p is the pressure, ρ is the density of the molecule mass, and f is the external force on molecules. The first term represents the advection, which is the velocity of a fluid that causes the fluid to transport objects, densities, and other quantities along with the flow. The term inside the parenthesis is the divergence, which represents the rate at which density exits the region. <br/>
The second term simulates how pressure gathers and generates force and provide accelerations to the surrounding molecules. <br/>
When time advances, we compute the advection and divergence based. Based on the interaction between neighboring molecules, we propagate the changes in temperature, pressure, and velocity correspondingly. We then update the values in each 3D texture and render the resulting molecules to the screen. <br/>

<!-- <div align="center">
<img src="assets/images/fire.png" width="480px" />
<figcaption align="middle"> Rendering Result </figcaption>
</div> 

<div align="center">
<img src="assets/images/sim_box.png" width="480px" />
<figcaption align="middle"> The green color represents the propogation of density. </figcaption>
</div> 

<div align="center">
<img src="assets/images/sim_pipeline.png" width="480px" />
<figcaption align="middle"> Visualization of the simulation and rendering pipeline. </figcaption>
</div>  -->
 

<div align="middle">
  <table style="width=100%">
    <tr>
      <td>
        <img src="assets/images/fire.png" align="middle" width="400px"/>
        <figcaption align="middle">Rendering Result</figcaption>
      </td>
      <td>
        <img src="assets/images/sim_box.png" align="middle" width="400px"/>
        <figcaption align="middle">The green color represents the propogation of density</figcaption>
      </td>

<td>
        <img src="assets/images/sim_pipeline.png" align="middle" width="400px"/>
        <figcaption align="middle">Visualization of the simulation and rendering pipeline</figcaption>
      </td>




    
  </table>
</div>


## Challenges

The main difficulty of our implementation comes from debugging the propagation of the attributes across timestamps. Unity is not designed to accommodate print debugging so we created a script in Python to calculate the values for a 2D fire simulation. It turns out that the values propagated as expected, which proved that our formula was correctly implemented. We then created a debugging shader to fill in empty textures so that we can see how the values advance in our model. 

## Future Goals 

In the next stage, we would like to introduce the buoyant force, an attribute used in the simulation of smoke and fire. The buoyant force is influenced by temperature and density, and it changes the velocity of molecules to make the simulation more realistic. 
We also expect to generate a GIF or a real-time application to render the simulations and incorporate some environmental objects in our rendering. 


## Video Link 
https://www.youtube.com/watch?v=jdkjiDlUR0A&feature=youtu.be 


## Resources and References

1. “Real-Time Simulation and Rendering of 3D Fluids”, Keenan Crane, Ignacio Llamas, Sarah Tariq
https://www.cs.cmu.edu/~kmcrane/Projects/GPUFluid/paper.pdf  
2. “GPU Gems - Chapter 38. Fast Fluid Dynamics Simulation on the GPU”, Mark J. Harris,
University of North Carolina at Chapel Hill, https://developer.download.nvidia.com/books/HTML/gpugems/gpugems_ch38.html
3. “Smoke Simulator”, Rachel Bhadra, Jonathan Ngan, Kenneth Tsai, https://rachelbhadra.github.io/smoke_simulator/index.html

