# N-body simulations in cosmology

![Cosmic Web](https://www.alcf.anl.gov/sites/default/files/styles/965x543/public/2019-09/Habib_hacc_outer_rim_1600x800.png)

In this project you will experiment with [GIZMO](http://www.tapir.caltech.edu/~phopkins/Site/GIZMO.html) and [GADGET-4](https://wwwmpa.mpa-garching.mpg.de/gadget4/), two professional N-body simulation software, frequently used in cosmology.

The goals of this project are diverse. The first one is to learn the usual process of installing and running a scientific software that uses `make` instead of `CMake` to build it and configuration and parameterfiles to set up the simulation. The second goal of the project is to give an introduction to gravitational N-body simulations and showcase how large scale astrophysical and cosmological simulations work and look like.

**Important note**: You'll have to use Linux/MacOS or at least WSL for this project, since GIZMO, GADGET and their dependencies can't be ran on Windows without losing your sanity.


## Recommended steps for the project

1. Install a local version of [GIZMO](https://bitbucket.org/phopkins/gizmo-public/src/master/) and [GADGET-4](https://gitlab.mpcdf.mpg.de/vrs/gadget4) along with its dependencies listed in their tutorials. (The dependencies should entirely overlap and their installation should be almost identical.) You can find the GIZMO tutorial [here](http://www.tapir.caltech.edu/~phopkins/Site/GIZMO_files/gizmo_documentation.html#tutorial), while the GADGET-4 tutorial [here](https://masterdesky.github.io/blog/astro/sim/gadget4-install).

2. Set up the configuration file for a [test problem](http://www.tapir.caltech.edu/~phopkins/Site/GIZMO_files/gizmo_documentation.html#tests) provided with the GIZMO code, recompile the software with this new configuration and run any selected test problem.

3. Experiment with N-body test problems, provided with the GADGET-4 N-body simulation code **in GIZMO**. GIZMO is a direct descendant (fork) of the GADGET simulation software family and designed to be entirely compatible with it. While GIZMO doesn't include (good) gravitational N-body demo simulations in their public release, GADGET does.
Two interesting N-body examples you can try:
   * [collision of galaxies](http://www.mpa-garching.mpg.de/mpa/research/current_research/hl2005-2b/hl2005-2b-en.html)
   * [large scale evolution of the Universe](http://www.mpa-garching.mpg.de/galform/millennium/)

4. For each problem above, evaluate the simulation results and visualize them using your favorite programming language (obvious recommendation is Python). Eg. in case of cosmological large scale structure simulations, you can calculate the [power spectrum](https://arxiv.org/pdf/1503.05920.pdf), one of the most important evaluation metric of such simulations.

5. Create new initial conditions using the GADGET-4 software and run a cosmological N-body simulation with GIZMO using said initial conditions. Configure the `Config.sh` and the necessary `parameterfile` accordingly.


## Notes
- Running a simulation with GIZMO or any GADGET software can be broken down into four steps (after installation):
   1. Turning on the relevant **compile-time options** in the `Config.sh` file and recompiling the software. (The correct setup is always provided in case of demo simulations.)
   2. Preparing the initial conditions of the simulation. (Also provided in case of demo simulations.)
   3. Setting up a `parameterfile` that defines the **run-time options** of the simulations. (Also provided for the demo simulations.)
   4. Executing the software binary and waiting for the simulation to finish.

   It looks much more terrifying, than it actually is, don't worry. The results will be awesome. Check what GIZMO's capable of as demonstrated at the [official site](http://www.tapir.caltech.edu/~phopkins/Site/GIZMO.html) of GIZMO.

- The simulations will result in the creation of *snapshots*. These are "checkpoints" of the simulation at specific (usually equal) time intervals. Eg. an N-body simulation snapshot will contain the position, velocity, mass, etc. values at a specific time during the simulation. But eg. a fluid simulation will contain the pressure and density maps and other physical parameters that the user requested from the software to save at every checkpoint.

   When we're talking about "analysis", these snapshot files contain the actual data we want to process, visualize, etc. You will also work with these in this project.


- You'll need to use the [Plancks 2018.](https://arxiv.org/pdf/1807.06209.pdf) cosmological parameters in astrophysical/cosmological `parameterfiles` to run a simulation. The last column of Table 2. contains the relevant parameters in this linked article. (But beware, because parameters above and below the first horizontal separator are not consistent with each other and it's not mentioned anywhere in the article! However you can easily calculate the remaining parameters from either set of values. You'll only need the *Omega* parameters and the Hubble parameter.) The [LCDM wikipedia article](https://en.wikipedia.org/wiki/Lambda-CDM_model) could shed some more light on them.

- If you have any questions, ask the topic's advisor or [ChatGPT](https://chat.openai.com/chat) that (not so surprisingly) has an extensive knowledge in classical N-body simulations and all the related literature. As of February 2023 it can't create `Config.sh` nor `parameterfiles` though, unfortunately.

## Further useful links

- [Gadget File Viewer](https://github.com/jchelly/gadgetviewer): A lightweight visualization tool for GADGET-type simulation snapshots (works for bot GIZMO and GADGET).

- [Introduction](http://www.artcompsci.org/msa/web/index.html) to N-body simulation by P. Hut and J. Makino (local [copy](http://csabai.web.elte.hu/http/simulationLab/hutMakinoTutorial.pdf) and [code](http://csabai.web.elte.hu/http/simulationLab/hutMakinoStarterCode.tar))

- [Another introduction](https://pdfs.semanticscholar.org/96aa/9d4c0c867364aff6b8549e67b93f198bf56d.pdf) gravitational N-Body simulations

 
Generating initial conditions:
* [Starscream](https://github.com/jayjaybillings/starscream): for collisions of galaxies 
* [NGenIC](https://www.h-its.org/2014/11/05/ngenic-code/): general cosmology IC generator with [Zel'dovich perturbation theory](https://ui.adsabs.harvard.edu/abs/1970A&A.....5...84Z) (1st order)
* [2LPTic](http://cosmo.nyu.edu/roman/2LPT/): general cosmology simulations with [second-order Lagrangian perturbation theory](https://ui.adsabs.harvard.edu/abs/1998MNRAS.299.1097S) (2nd order)

**Note:** GADGET-4 has a built-in initial condition generator module that encompasses both NGenIC and 2LPTic.

