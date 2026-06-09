Guiding Principles
==================

Consider a simple grid on graph paper. From a programming perspective, we have a ``Grid`` object with a collection of ``Cell`` children. Each cell corresponds to a square of the grid. The ``Grid`` object has a location in space, and each cell also has a location in space, but we often do not say "I want the cell with ``(x, y)`` position ``(50, 50)``". Instead, we often think of grids as a 2D array and ask for the cell at *index* ``(1, 1)``. Indices are simple numbers (regardless of grid structure) whereas coordinates require knowledge of grid size, cell index, and cell sizes. Unfortunately, for applications like games, in order to actually render a grid, you need to have knowledge of coordinates to actually render a grid correctly. This library provides various utilities for converting the indices of a grid to physical coordinates.

Even worse, graph paper is a fairly simple grid too! All the cells are uniform width and height and the grid spans the full paper. ``lpyout`` extends this by allowing variable width and height cells, and allowing for you to specify the size of a graph with various grid creation utilities. Furthermore, in ``lpyout`` a graph may have a grid within a grid. We now come to the guiding principles of ``lpyout``:

- to provide various utilities for creating grids/modifying grids.
- to provide conversion of indices of a grid to the correct coordinates.
- to provide a ``Grid`` object corresponding to a tree with children that are either other ``Grid`` objects or ``Cell`` objects which are the leaves of the grid trees.
- to privde utilities to quickly visualize grids.

In order to construct grids, various simple class methods act as constructors for common grids and various stylings (often borrowed from CSS) can be used to tweak the grid to have the coordinates you need easily! Once the coordinates for the grid objects have been calculated, we use various properties and tools like ``grid_map`` to reduce boilerplate for rendering grids. In the following sections, we go over how to use these various tools to render a variety of grids.
