# Abstract

# Introduction

- why we need hexahedral meshes (storage of geometric objects)
- how we approach the problem (integer grid maps are too hard -> frame fields as relaxation)
- What are frame fields?
- introduction of metric field
- structure of thesis

# Mathematical Background

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

Formulation of connection by starting from local integrability

## smoothness measure in dirichlet

Justification of the Dirichlet Energy, is exactly equal if the metric $g$
is flat ($g$ constant)

## connection evaluation

Reformulations, set up linear system for $\omega$

# Calculation of rotation coefficient within tet

Problem statement, question is how to measure if two frames are "parallel" within new metric. Corresponds to parallel transport.
Calculate rotation $R$ from one point to another how a frame would get rotated within the metric field.

## discretization of metric field to piece-wise linear

## recursive subdivision within tet

# Algorithm for $R$ between two arbitrary points in a mesh

Problem statement

## framework

### note on orientation tests

## Exact formulation of algorithm

# Frame Field optimization

- Problem statement

- Simone algorithm from a high level

- Caching of coeffs

# Experiments

Different experiment setups:

- constant metric everywhere -> no singularities

- linearly increasing metric in z-axis, isotropic scaling

- 2d example anisotropic scaling, constant-linear-constant

- larger cubes at the edges of the cube, isotropic scaling

# Conclusion

Future work, how to store rotation coeffs in octree
