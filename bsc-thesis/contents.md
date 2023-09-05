# Abstract

# Introduction

- why we need hexahedral meshes (storage of geometric objects)
- how we approach the problem (integer grid maps are too hard -> frame fields as relaxation)
- What are frame fields?
- introduction of metric field, what we optimise how we do the change
- structure of thesis

# Mathematical Background 

(best to explain with examples how I need it in my thesis, and just reference to literature)

## differential geometry

### manifold

### Tangent space, Tangent bundle

### Cotangent space, Cotangent bundle

### Tensor

### Differential forms, exterior derivative

### Riemannian metric, $g$-orthonormality

### Connection, covariant derivative, parallel transport

## frame fields

### Integer-grid maps

### frame fields as a relaxation

relaxation because frame fields are over general, sometimes they exhibit non-meshable structure

# Connection for local Integrability

explain how dirichlet with metric gives good integrability of the frame field
(important, explain in own words, make everything clear)

Formulation of connection by starting from local integrability

## smoothness measure in dirichlet

Justification of the Dirichlet Energy, is exactly equal if the metric $g$
is flat ($g$ constant)

## connection evaluation

Reformulations, set up linear system for $\omega$

# Alignment in the metric field

Problem statement, question is how to measure if two frames are "parallel" within new metric. Corresponds to parallel transport.
Calculate rotation $R$ from one point to another how a frame would get rotated within the metric field.

## discretization of metric field to piece-wise linear

## recursive subdivision within tet

# Algorithm for $R$ between two arbitrary points in a mesh

Problem statement

## framework

### note on orientation tests

## Exact formulation of algorithm

Explain everything that was needed to make it exact.
- How to find the location of the starting point,
- pointInTet exact,
- rayTriangleIntersection exact,
- Handling degenerate cases,

# Frame Field optimization

- Problem statement

Just from a high level, it's MBO algorithm,
explain how this metric approach works if you do these pairs of
$||R_{ij}t_i-t_j||$ would work with any dirichlet optimiser

- Caching of coeffs

# Experiments

(Important chapter)
also show how increasing the $k$ parameter increases the amount of singularities
and discuss

Different experiment setups:

- constant metric everywhere -> no singularities

- linearly increasing metric in z-axis, isotropic scaling

- 2d example anisotropic scaling, constant-linear-constant

- larger cubes at the edges of the cube, isotropic scaling

# Conclusion

Future work, how to store rotation coeffs in octree

discussion of discretization

storage of metric fields, other ways to do it (octree, other bases)