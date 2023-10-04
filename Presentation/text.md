1. Welcome everyone to my bachelor thesis presentation.
My thesis is about Metric Fields in 3D, where the working goal
was to optimize frame fields in a new metric.

2. Quick overview what I will talk about.
First, I'm gonna explain what it is we are trying to do, namely hexahedral meshing.
I'm gonna show you the top down view how we try to tackle this problem with integer grid maps, and I'm gonna show how we try to find such an Integer grid map through frame fields.

After this quick introduction, the main part of my thesis:
I show how by introducing a metric field, we can control the frame field generation.
For this, we need to change the typical formulation of smoothness of the euclidean metric into our new, custom metric.

The third part is how we discretize everything to actually being able to calculate everything.

And last but not least, I will show you some of the experiments, where you can see some results.

All what we are doing here is in 3 dimensions. So any time the pictures are in 2d, it is because it is
easier to visualize and represent.

3. Alright. What are we trying to do.

4. 
In many many applications, the geometry of objects has to be represented in some way. Be that for animation or
physical simulations. For example, this spring is represented with these long, hexahedral elements,
on which a stress simulation can be done.
Objects can also be represented with tetrahedral elements, but in practice, hexahedral elements are preferred
because they behave better in terms of numerical precision and stability, and usually, fewer elements are needed to accurately represent an object.
However, while good tetrahedral meshes can be generated automically nowaysdays, automatic generation of a good quality hexahedral mesh remains unsolved.

5. The key idea for finding a hexahedral mesh is through the use of integer-grid maps.
Suppose we have some object. We search for a mapping Phi, which maps the object to the grid. As you can see, the inverse of this mapping, returns exactly a parametrization of such a hexahedralization. 

Directly searching for a good quality mapping is infeasible
unfortunately, as this is a hard mixed-integer non-convex optimization problem.

6. Thus, we relax the problem:
We want a mapping Phi from M to $R^3$.
So, let's take the jacobian of Phi, and we get a 3x3 matrix.
Now we search for an approximation of the gradient, F. We call this mapping F a frame field and each element is called frame.
A frame locally represents the deformed edges of a cube.

7. Now let's think about some of the properties we want F to have, such that it has our desired quality.
Our goals for the frame field is
- smoothness
- and boundary alignment
Smoothness is measured per column of our frame field. The frame field essentially consists of three linearly independent vector fields. Each of these should be smooth, they shouldn't vary.
Boundary alignment is that at the surface, one of the columns should align with the surface normal of the object.

8. Here we see what we want. Basically, these requirements
say that we want this, not this.
On the left, the hex mesh is highly irregular, and here
at the top, the elements aren't boundary aligned.

On the right, we have a nice, smooth mesh. So the hex elements
dont twist and turn randomly. and at the top, the edge is clearly
defined because of the boundary alignment

9. Ok, so the goal is to find the smoothest frame field under the restriction that the frames satisfy boundary alignment. We measure smoothness with an energy function called the dirichlet energy. This energy is really simply
defined where we just integrate the gradient of the frame field. So this basically measures how much the frames twist and rotate within the object. So now as you can see, by minimising this expression, the gradient gets minimised.
That means we minimise the twisting of frames.
And now recall again that frames represent the deformed edges
of the hex elements. So by keeping the frames still, we keep the hex elements still. We keep it as regular as possible.

10. Ok, this is all the introduction we need about frame fields. So now let's talk about how to control it
to make it behave the way we want as a user want.

11. Now, if the frame field is orthonormal, the
extracted hex elements resemble unit cubes.
Now, let us say, for whatever reason, that we want
bigger elements at the top here and smaller elements at the bottom.
To achieve this, we change what orthonormality means.
We assign a matrix $g$ at every point on the object,
which is our metric. And now we instead measure orthonormality
in this new metric. So get the notion of $g$-orthonormality.
Maybe a picture also helps:
This metric $g$ defines that these quads at the top have the same size as the quads at the bottom.
Not for us, who kind of look from the outside, but measured in the metric.

12. So as we have seen, the metric defines lengths and angles in a new way. You could say it deforms the space.
And suddenly, the meaning of "straight" changes.
From the outside, we would say a line isn't straight, while in the metric it is. So we cannot use the euclidean dirichlet smoothness measure anymore, as this assumes a non-curved space.

For an intuition of what is happening, see this picture.
We have this grid, and the metric $g$ deformed the original straight lines. So what is pictured is now straight in the new metric. 

$g$ defines a special quantity called $\omega$, which basically defines at each point, how the space locally rotates, they are infinitessimal rotations.

13. So what we are interested is now how to measure the smoothness in our new metric.
See this example. We have this beam and two frames at point $q$ and $p$. They are parallel.

Now lets deform this beam with $\phi$. Now the frames aren't parallel when viewed from the outside. But we have to think what happenend from the inside. So what we want to measure is this rotation $R_{qp}$ that happens when we move from $q$ to $p$. For this, we integrate the infinitessimal rotations $\omega$ mentionend before, which yiels us, in this example the 90 degree rotation.
So to measure smoothness in the new metric, we need to 
calculate a rotation coefficient which aligns the frames in the new metric.

14. Now I explain how we discretize everything. The integral is calculated numerically, and the metric field is discretized.

15. We cover the object with a tetrahedral mesh. Then we store the metric by storing 3x3 matrices at the vertices. So we
have matrices as support points, and then within the tets, we use barycentric coordinates to linearly interpolate within.

16. However, now by discretizing like this, we have a new problem. When we want to integrate from some point $q$ to $p$,
we need to use the appropriate metric field for that.
So we need to find all tetrahedra that the line segment from $q$ to $p$ lies in and then use the correct metric field.
So in this image, we are at point $q$ and want to integrate to point $q$, and now we need to find all these highlighted intersection points and do a piecewise integration.

17. There is this elegant technique called "Walking on a triangulation" which we can modify to our needs that achieves exactly that.

*Show algorithm on whiteboard*

Notice how the procedure exactly highlighted the edges and triangles traversed. We can store these in a list and then just iterate through to do the integration.
The same approach works in 3d, but there the algorithm highlights faces. But the intuition is exactly the same.

18. So we can put everything together now.
First we store the metric field by defining the metric matrices at the vertices.
Next, we minimize the dirichlet energy with some minimizer.
For this, we discretize the energy:
Instead of an integral, we use a sum over some support points,
where we take the difference of two frames as the gradient.

And this discretization is really easy to modify for the alignment. To compare two frames $F_q$ and $F_p$ in the new metric, we just need to rotate one frame by the rotation as described before.

19. So now let's look at some results. Btw, as a dirichlet energy minimizer, I used an algorithm from Simone, which he kindly provided an implementation that I could modify with the rotation coefficient.

20. As a first experiment, I apply 
the constant metric one one one, which is just the euclidean metric. I attach the same matrix at all these vertices of this tet mesh and run the optimizer.
And, as expected, the constant boundary aligned frame field is returned.

21. Next, we divide the cube along the z-axis into 3 parts.
And then at the bottom, again the constant metric one one one.
At the top 10, 1, 10 and in the middle third it's a linear interpolation between the two.
Left you can see the first component of the matrix.
Here, we see the cube from the front. Clearly visibly how the frame field only changes in the middle third.
From the side, so viewing down the y-axis, we can see that nothing is happening there, which makes sense because the metric is constant in the y-axis.
And lastly, there are 4 singularities which are only points if you slice along the y-axis. This matches the experiment in 2D.