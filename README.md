[![DOI](https://zenodo.org/badge/150148604.svg)](https://zenodo.org/badge/latestdoi/150148604)

# convolution_density_profile
This program is to get well-aligned density profiles from trajectory with multi-components in molecular dynamics using convolution method under periodic boundary condition

## prerequisites in python
* `numpy` and `scipy`: for numerical calculations
* `mdtraj` (> version 1.9.1): to read trajectory and structure file

## How to work: alignment of instantaneous density profiles to get a smooth profile
### introduction
Molecular dynamics is a good tool to simply simulate complex systems such as two phases (solid-liquid, liquid-liquid, liquid-gas) of single or multi-components. From two equilibrated phases in a single cell, we can get density or concentration profiles at time frames for single or multi-components. The problem is that the density profile has instantaneous values, thus we need to average the profiles to get coexistance properties to draw phase diagram such as concenteration - temperature space. During the simulation, because of mass transfer between two phases and fluctuation of interace position, alignment method is necessary to reduce any flucutations.
### convolution method
The idea is to implement convolution method in not only signal processing but also density profile. In engineering field, the method is widely used to get delay time between two identical (sound, light, or electrical) wave signal but different tranvelling time (or travelling distance) from source to detector. Even though very noisy environment may prevent to figure where the signals show, the convolution method amazingly works in obtaning the delay time for signal processing. This strategy may work in this density profile due to following analogy:

| interpretation | wave signal | density profile |
| ---------------| ----------- | --------------- |
| object1 | wave packet with travelling time `t1` | density profile with travelling distance `d1` |
| object2 | wave packet with travelling time `t2` | density profile with travelling distance `d2` |
| delay time or shift distance | `t2-t1` | `d2-d1` |
| In real, | wave packet mixed with noise by environment | density profile with statistical noise due to small number of molecules |
| In theory, | wave packet with sum of sine functions | density profile as sum of two tangent functions |

Once we know all shift distances between any density profiles by convolution, we can align the density profiles accurately by shifting along the normal direction on interface plane (assummed 2D-plane), and then get well averaged density profile to get accurate density or concentration of phases 

### Need to some tests before applying for good results
Basically, slicing method is necessary to get local densities of slabs which are parallel to interface plane. The thickness of slab is the half resolution to get optimal shifting distance for density profile. Thus, to get good result, small slab thickness is good choice.

On the other side, if the small aggregation in the phase exists or your molecules are big enough, convolution might not work unless you increase slab thickness. For very small slab thickness, the density profile would be descrete, which leads wrong optimal shift distances. Thus, we recommend to check the effect of thickness of slab on density profile and coexistance properties. 

### limitataion
currently, I assume the system has only two phases under periodic boundary condition. If your system is in single phase (mixing) or three or more phases, please find alternative way by modifying this code or making your own code. 

### versions
v0.1 upload my home code to github for polymer/ionic liquid system. 
(see tutorial for such a three-component system - cation, anion, and neutral polymer)

### citation
Please cite the following article for convolution method:
> A simulation method for the phase diagram of complex fluid mixtures
> Hyuntae Jung and   Arun Yethiraja)
> The Journal of Chemical Physics 2018 148:24
> https://aip.scitation.org/doi/abs/10.1063/1.5033958
