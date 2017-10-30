# WiReS - Wind Reconstructor Server


Flight Simulation in presence of wind and turbulence. A "Wind Reconstruction Server" to interface JSBSim and OpenFOAM

_Università degli Studi di Napoli Federico II_  
_Fraunhofer-Institut für Windenergie und Energiesystemtechnik IWES Nordwest_

---
### Description of directories
- **calc**: contains Python scripts and notebooks, and everything is needed for the workflow. Python `.py` files are mainly used for defining functions and classes, while notebooks are intended for carrying out calculations and presenting the results. The application to edit, run and view the results in a live coding environment is the Jupyter Notebook, which can be launched by typing `jupyter notebook` in a terminal at the current folder, or wherever needed.

- **JSBSim**: contains the core directories and the executable needed for flight dynamics simulations. This is just a minimal distribution of the complete software.
 - **aircraft**: contains aircraft flight dynamics models
 - **engine**: contains propulsive models of engines and propellers
 - **scripts**: contains JSBSim simulations scripts
 - **systems**: contains flight systems models and other utilities of different types

- **WiReS**: is the neutral platform in C++ used to interface JSBSim and OpenFOAM. It is an asynchronous server developed as an OpenFOAM platform. It accepts an OpenFOAM case folder as input and then waits for JSBSim instances (that actt as clients) to start sending flight data to it.

- **OF21x**: is a selection of code to run several OpenFOAM cases. Version 2.1.1 should be preferred, Actuator Line Model is used within a LES type of simulation.

---
### Project objectives definition
The aim of this project is the development of a software architecture for controlling automatic flight
simulations in presence of assigned wind and turbulence fields.

The application for which it has been requested is a risk assessment for landing trajectories of light
aircraft in proximity of wind farms.

The flight simulation model makes use of several different autopilot systems for simulating a real pilot
behaviour, as far as attitude and navigation control are concerned.

Wind distribution is a separate input for the dynamic model, and is considered frozen during each simulation.

A journal article and a public dataset, currently both under development, present the work more thoroughly. An extract from the paper is reported here:
>"The WiReS application makes the flight and fluid dynamics sides of the simulations communicate with each
other. It has been developed as an asynchronous server to work as a database and computational engine. In
principle, the WiReS application is fed with the aircraft position at every time step of the flight dynamics
simulation. The OF mesh domain is then accessed with this information by the server, and the corresponding
wind velocity vector is retrieved and sent back to the aircraft. Within this configuration, JSBSim acts as the
client application, while OF provides the mesh domain and the wind velocity field data structures that are
statically loaded (only once) and continuously accessed by the server.
In order for the OF domain to represent an actual geo-referenced scenario on Earth, the mesh points must
be translated according to the aircraft initial position. For this work, all of the OF meshes are rectilinear
with different local refinements regions, and it is assumed that mesh points coordinates are expressed in a
UTM coordinate system.
The most relevant steps of the interactive process are here covered in detail. For each JSBSim instance,
and for each time step in the flight dynamics simulation: (i) JSBSim transmits the instantaneous aircraft
position in a spherical, Earth-fixed reference frame; (ii) WiReS converts latitude and longitude coordinates to
the UTM Cartesian coordinate system; altitude is untouched; (iii) WiReS uses these new form of the aircraft
position to directly access the OF mesh and interpolate the wind velocity vector field; (iv ) WiReS transforms
the wind velocity vector to the more common (for aeronautic applications) NED reference frame, converts
it to fts􀀀1 and passes it back to the original instance of JSBSim; (v) JSBSim acquires the wind velocity
vector and uses it to update the aircraft velocity vector relative to the wind. (vi) Finally, all aerodynamic
parameters are altered and the aircraft position is propagated to the next time step taking into account
the effects of the wind in that exact location on Earth.
All the operations in the server scope are performed by WiReS in an asynchronous way.
This turns to be extremely useful when many JSBSim instances are launched in parallel, as the interpolation
process depends on the dimension of the CFD domain and on the aircraft position relative to it."

---
### Tools
The whole project completely embraces the open source software philosophy, as you can see from the list below:

- **JSBSim** is the open source flight dynamics model used for flight simulation.  
- **OpenFOAM** is the open source CFD software implemented for simulating wind distribution.
- **ParaView**: is the open source data analysis and visualization application
- **Jupyter Notebooks** represent the structural framework of the software environment.  
- **GIMP** is an open source bitmap images editor.
- **Inkscape** is an open source vector graphics manipulation program.
- **LaTeX** for high-quality typesetting of results and data
