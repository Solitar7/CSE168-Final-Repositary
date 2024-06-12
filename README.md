# CSE168 Final Project - Volumetric 

#### By Yuning Wen

## Proposal

//This is the final project for UCSD CSE 168 SP24. I'm planning to do the homogeneous volumes and may finally finish it with different scenes or even Heterogeneous volumes in some way if possible. First of all, these are some of the pictures that inspire me to do the homogeneous volume.

For the final project for UCSDE CSE 168 SP24, I'm trying to approach the homogeneous volumetric rendering with a single volume that holds the whole space. The following pictures are some examples that inspire me to do the volumetric rendering.

- From Stanford CS 348b competition

![Insp_1](Insp_1.png)

![Insp_2](Insp_2.png)

- From Tyndall effect

![Tyndall](Real_World_Tyndall_Effect_Insp_3.jpg)

Due to the accessibility and the nice effect of this algorithm, I decide to have a try to approach and implement this algorithm.

## Mathematics and formulas

[Lecture Slides](https://cseweb.ucsd.edu/~viscomp/classes/cse168/sp24/lectures/168-lecture15.pdf) is one of the most important source that I'm using, and I have also used the material from CSE 272 taught by Tzu-Mao Li in Winter 2024, both the [slide](https://cseweb.ucsd.edu/~tzli/cse272/wi2024/lectures/09_participating_media.pdf) (only this one is considered since only homogeneous volumetric rendering is trying to be approached) and the [material in homework](https://cseweb.ucsd.edu/~tzli/cse272/wi2024/homework2.pdf).

Without consider the emissive volumes, we then only need to consider a homogeneous volume, which takes in two constants: sigma_a, the coefficient for absorbtion; and sigma_s, the coefficient for scattering. Here's the formula that I'm trying to approach through path tracing:

$$L(p(0), \omega) = \int_0^{t_{\text{hit}}} \exp(-\sigma_t t) \sigma_s L_{\text{scatter}}(p, \omega) d t + \exp(-\sigma_t t_{\text{hit}}) L_e(p(t_{\text{hit}}))$$

$$L_{\text{scatter}}(p, \omega) = \int_{S^2} \rho(p(t), \omega, \omega') L(p(t), \omega') d \omega'$$

These formulas should call each other recursively begin with $L(p(0), \omega)$ that takes the origin and direction calculated through the position of the pixel on the final image and other information set inside the scene. Termination should be executed when a certain number of depth is reached or by using the Russian roulette.

By using path tracing, instead of doing the whole real integration, we always use Monte Carlo to estimate the final result by sampling a random point in the scope of the integration and then divide the final result by the importance pdf to try to approach the result of the integration. As the number of sample increases, the average of the integration result may better approach the final result, and thus finer rendering results are expected as the number of sample per pixel (spp) increases.

## Rendering Result

First of all, I may not promise that I have implemented my algorithms totally correct. But the following pictures are the rendering result in some simple scene.

Materials:
- [Source 1](https://graphics.pixar.com/library/ProductionVolumeRendering/paper.pdf)
- [Source 2](https://en.wikipedia.org/wiki/Beer%E2%80%93Lambert_law)
