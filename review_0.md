<!-- markdownlint-disable MD033 MD041-->

# Research Proposal
# A High Order Finite Volume Method Using RBF Reconstruction for Solving the Non-Conservative Convection Equations

## 1. Introduction

### 1.1. Reconstruction High Order Finite Volume Method

Numerical methods with high (3 or higher) order of spacial accuracy have been extensively used in computational fluid dynamics (CFD). There are typically three types of high order space discretization methods suitable for convective problems: finite difference (FD), finite volume (FV) and discontinuous Galerkin (DG), and the finite volume method is able to handle unstructured mesh while being robust with the presence of strong discontinuities [[1]](#ref1). 

In FV schemes, the computational domain $\Omega$ is partitioned into non-overlapping control volumes $I_i$, where $\Omega=\bigcup^N_{i=1}I_i$ . A solution is numerically stored as average values of each CV, and represented as a reconstructed piecewise-smooth function. The conservative terms of the PDE are represented as fluxes integrated on CV interfaces, with others terms as volume integrations. Therefore the spatial differential PDE operator is discretized into a arithmetic operator. Accuracy of the FV scheme greatly depends on the reconstruction procedure, while the major concern of high order FV methods is to build a high order reconstruction method. 

The earliest kind of high order reconstruction in FV method is the k-exact scheme [[2]](#ref2). More recent work [[3,4,5,6]](#ref3) also include reconstruction schemes using a compact local stencil. In these methods, the solution is approximated with high order polynomials in each control volume. Using some appropriate method to calculate polynomial coefficients in each volume, high order of spacial convergence can be achieved. 

Although polynomials have been proven to be optimal under certain criteria, in some convex problems adopting Galerkin methods for example, opting to non-polynomial basis functions could still be beneficial to nonlinear convection problems. In fact, applications of radial basis functions (RBFs) in PDE methods including FV have been investigated in various literatures. 

### 1.2. Radial Basis Functions and Relevant PDE Methods

RBFs are functions defined in $\mathbb{R}^d$ in the form of $\phi(\mathbf{x})=f(||\mathbf{x}||)$, where $||\cdot||$ is a norm commonly being the Euclidean norm. They are widely used for scattered data interpolation, data reconstruction and computer graphics. 

One of the earliest PDE methods utilizing RBFs is the radial basis function collocation method (RBFCM) [[7,8,9,10]](#ref7). As the original RBFCM uses globally supporting RBFs, which is costly, a series of local RBF collocation methods have been proposed [[11,12,13]](#ref11). As RBF only relies on a base point, RBFCM is a mesh free method.

Another mesh free RBF method is based on finite differential ideas (RBFFD), which directly approximates the derivatives with RBF [[14]](#ref14). As RBFFD is entirely central, stabilizing measures such as artificial viscosity are necessary in convective problems [[15,16]](#ref15). 



### 1.3. RBFs in High Order Finite Volume Reconstruction

Apart from mesh free methods, RBFs can also improve meshed methods including FV.Effectiveness of incorporating RBFs in high order finite volume have also been investigated. 

In a series of research [[17, 18, 19]](#ref17), RBF is combined with a nodal form of FV, the control-volume finite element (CV-FE), to improve accuracy. The original CV-FE reconstructs polynomials on the simple volumes, such as tetrahedra, while FV control volumes are established surrounding each tetrahedra node. In [[17]](#ref17), the original field reconstructed with shape functions is overlapped with additional RBF approximation using node values other than in the origin stencil. As the RBF-augmented reconstruction necessarily involves a larger stencil and more nodal values, it gains much higher accuracy. The RBF-augmented CV-FE is able to be 3rd-order accurate in 3-D problems and 5th in 2-D, compared to the original 2nd-order. This method was tested on diffusion-dominated problems, and its effectiveness is unknown in advection-dominated region.

Another approach to utilize RBFs in high order FV is to simply change the polynomials into RBFs, as is in [[20]](#ref20), where a fully RBF-WENO finite volume method was proposed. The RBF-WENO in [[20]](#ref20) replaces all the polynomials with RBFs in each candidate stencil, constructing appropriate linear weight expression and smoothness indicators. The results of this RBF-WENO indicate the choice of shape parameter and RBF type is essential to accuracy and stability, and proper settings could lead to similar or higher accuracy compared with regular polynomial WENO FV. A similar approach is also taken in [[21]](#ref21), where polynomials in WENO stencils are totally replaced with RBFs. Analysis in [[21]](#ref21) pointed out RBF-WENO is only applied in smooth regions and replaced with regular ENO with the help of discontinuity detector. Both RBF-WENO schemes in [[20]](#ref20) and [[21]](#ref21) were tested in 1-D discontinuous problems including Euler equation. In [[22]](#ref22), the multiquadric RBF is expanded into Taylor series, and an RBF-WENO that does not revert to classical WENO is derived.

While the RBF related FV methods above are using RBFs as part of or all of the reconstruction basis, one can also adopt a pure polynomial basis while using RBFs to derive the high order coefficients, as is in [[23]](#ref23) . When the polynomial reconstruction is viewed as a taylor expansion, the coefficients of polynomial basis correspond to approximate partial derivatives of the solution. Using a smooth enough RBF and enough stencil points, one can approximate any high order derivative with RBF interpolation. The results indicate that this method is able to out perform common k-exact reconstruction on 2-D unstructured grids.

### 1.4. Solving Non-Conservative Equations with High Order FV

(Huang et.al.)


## Research Objective


## Research Method











# References
*****


<!-- Reference: FV -->
<span id="ref1"></span>
[1] Shu, C.-W. (2003). "High-order finite difference and finite volume WENO schemes and discontinuous Galerkin methods for CFD." International Journal of Computational Fluid Dynamics 17(2): 107-118.
	
<span id="ref2"></span>
[2] Barth, T. and P. Frederickson (1990). Higher order solution of the Euler equations on unstructured grids using quadratic reconstruction. 28th aerospace sciences meeting.

<span id="ref3"></span>
[3] Wang, Q., et al. (2016). "Compact high order finite volume method on unstructured grids I: Basic formulations and one-dimensional schemes." Journal of Computational Physics 314: 863-882.

<span id="ref4"></span>
[4] Wang, Q., et al. (2016). "Compact high order finite volume method on unstructured grids II: Extension to two-dimensional Euler equations." Journal of Computational Physics 314: 883-908.
	
<span id="ref5"></span>
[5] Wang, Q., et al. (2017). "Compact high order finite volume method on unstructured grids III: Variational reconstruction." Journal of Computational Physics 337: 1-26.
	
<span id="ref6"></span>
[6] Zhang, Y.-S., et al. (2019). "Compact high order finite volume method on unstructured grids IV: Explicit multi-step reconstruction schemes on compact stencil." Journal of Computational Physics 396: 161-192.

<!-- Reference RBF_other -->

<span id="ref7"></span>
[7] Kansa, E. J. (1990). "Multiquadrics—A scattered data approximation scheme with applications to computational fluid-dynamics—I surface approximations and partial derivative estimates." Computers & mathematics with applications 19(8-9): 127-145.

[8] Golberg, M., et al. (1996). "Improved multiquadric approximation for partial differential equations." Engineering Analysis with boundary elements 18(1): 9-17.
	
[9] Šarler, B. (2005). "A radial basis function collocation approach in computational fluid dynamics." Computer Modelling in Engineering & Sciences 7: 185-193.
	
[10] Šarler, B., et al. (2004). "Radial basis function collocation method solution of natural convection in porous media." International Journal of Numerical Methods for Heat & Fluid Flow.

<span id="ref11"></span>
[11] Divo, E. and A. J. Kassab (2007). "An efficient localized radial basis function meshless method for fluid flow and conjugate heat transfer."
	
[12] Sanyasiraju, Y. and G. Chandhini (2008). "Local radial basis function based gridfree scheme for unsteady incompressible viscous flows." Journal of Computational Physics 227(20): 8922-8948.
	
[13] Sarra, S. A. (2012). "A local radial basis function method for advection–diffusion–reaction equations on complexly shaped domains." Applied mathematics and Computation 218(19): 9853-9865.

<span id="ref14"></span>
[14]Tolstykh, A. and D. Shirobokov (2003). "On using radial basis functions in a “finite difference mode” with applications to elasticity problems." Computational Mechanics 33(1): 68-79.
	
<span id="ref15"></span>
[15]Fornberg, B. and E. Lehto (2011). "Stabilization of RBF-generated finite difference methods for convective PDEs." Journal of Computational Physics 230(6): 2270-2285.
	
[16]Shankar, V., et al. (2015). "A radial basis function (RBF)-finite difference (FD) method for diffusion and reaction–diffusion equations on surfaces." Journal of Scientific Computing 63(3): 745-768.
	


<!-- RBF REC -->

<span id="ref17"></span>
[17] Moroney, T. J. (2006). An investigation of a finite volume method incorporating radial basis functions for simulating nonlinear transport, Queensland University of Technology.
	
[18] Moroney, T. J. and I. W. Turner (2006). "A finite volume method based on radial basis functions for two-dimensional nonlinear diffusion equations." Applied mathematical modelling 30(10): 1118-1133.
	
[19] Moroney, T. J. and I. W. Turner (2007). "A three-dimensional finite volume method based on radial basis functions for the accurate computational modelling of nonlinear diffusion equations." Journal of Computational Physics 225(2): 1409-1426.

<span id="ref20"></span>
[20] Bigoni, C. and J. S. Hesthaven (2017). "Adaptive WENO methods based on radial basis function reconstruction." Journal of Scientific Computing 72(3): 986-1020.
	
<span id="ref21"></span>
[21] Guo, J. and J.-H. Jung (2017). "A RBF-WENO finite volume method for hyperbolic conservation laws with the monotone polynomial interpolation method." Applied Numerical Mathematics 112: 27-50.
	
<span id="ref22"></span>
[22] Aràndiga, F., et al. (2020). "On the reconstruction of discontinuous functions using multiquadric RBF–WENO local interpolation techniques." Mathematics and Computers in Simulation 176: 4-24.

<span id="ref23"></span>	
[23] Liu, Y., et al. (2021). "Efficient high-order radial basis-function-based differential quadrature–finite volume method for incompressible flows on unstructured grids." Physical Review E 104(4): 045312.
	




	

	

	
