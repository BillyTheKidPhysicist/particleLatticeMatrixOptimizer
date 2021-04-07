# readme
3_18_2021 
This is a collection of files for an outdated method of optimizing the storage ring. In retrospect, it was a poor choice to use this method because it is assumed all magnets can be modeled as a transfer matrix, ie a simple harmonic oscillater. This is clearly not the case with the segmented bending magnet and I verified that fact by comparing this code to the full numeric method. I learned alot however doing this method.

 Briefly I will outline how this method worked.

1: a lattice is contsructed by the user adding elements and their parameters.

2: The parameters can be a Variable type object and used to parametarize the final model.  Sympy is used for symbolic math

3: The lattice is forced to be closed analytically solving a geometric constraint. 

4: From the resulting lattice one can compute the transfer function at each point in the lattice. This is used to compute the beta, alpha and gamma functions at each point. This can also be used to calculate wether the lattice is stable

5: at each point in the lattice parameter space, the injection system is optimized to match with the lattice.

6: optimization is done with a differential evolution algorithm I wrote, and solved in parallel across each thread. The result is considered the final result if there are mutliple 'herds' with close answers. The optimizing the injection is done with more convential methods like l-bfgs. The cost function considers wether the lattice is stable, wether the envelope is clipping the apetures, and how dense the atomic beam is. These three regions are stitched together with 3 sigmoids.