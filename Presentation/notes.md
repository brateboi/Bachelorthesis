Defending questions:
There doesn't exist left/right in 3d, but analogue is that we have positive orientation / negative orientation.
In 2d, we always have a "valid" configuration of left right, in
3d we always have a "valid" configuration by positive negative orientation with orientation predicate.
Edges turn to Faces, 2 orientation tests instead of 1.

Why not geodesic: -> There are infinite amount of geodesics with respect to the connection $\omega$,
so why not take the straight line for easier integration.
parallel transport is only path independent if metric is flat,
so it allows isometric embedding into R3. We assume that
our metric field is flat everywhere away from singularities. Which follows from local integrability.

Why these artefacts in the singularities. Its because of numerical imprecision. Need to run optimizer to higher depths, but runtime is exponential because the implementation that is not yet adaptive.

--------------- Changes for speech
Dont say hexahedral elements are better, just say we don't have automatic good quality generation of them. 


Phi is not integer grid map, we search for a seamless map $\phi$,
which smoothly maps our object into R^3.
Then in a next procedure step, we quantize this map to get an 
actual integer grid map, where the hexahedral mesh can be extracted from.


Smoothness is just minimizing the gradient, so the change of frames. Don't say we want the frames to be as constant as possible. 

Its quadrangulation example, but the intuition is the same. We need to align to boundary and features.

Say that we use frobenius norm.
So we minimize gradient field which is turned with frobenius norm to scalar field which we can integrate and minimize.

$g:\mathcal{M} to \mathbb{R}^{3x3}$, provides matrix at every point.

Object is tetrahedral mesh and we store metrics at vertices.

Walking:
Intuition is the same, in 2d, l r always intersects with line segment. In 3d, we always check that uvw intersects with line segment. So face always intersects.


Put weights to sum for integration. Integration is done with $d\volume$.
Add third experiment in 3d


Singularities are just where there are 3 or 5 neighboring quads.