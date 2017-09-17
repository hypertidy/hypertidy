# hypertidy
[ ... ]

## The hypertidy work plan


**vapour**
- [ ] check vapour on MacOS
- [ ] check license / copyright issues for vapour
- [ ] build sfcore
- [ ] put core raster logic in discrete

**NetCDF**
- [ ] fix `group_by` for tidync
- [ ] find a way to cut dimensions (dplyr::tile?)

**anglr**
- [ ] integrate TR's quadmesh helpers

**silicate**
- [ ] dynamic edges, record original start/end edge with throw-away Steiner points?
- [ ] inner cascade and semi cascade, names for the concept, activate to start in the middle, formal join-ramp
- [ ] 


- [x] restructure sc around the gibble concept
- [x] consolidate `silicate` (remove sc/scsf)
- [x] release `unjoin` and `gibble` for use by the sc family


# overall approach

The hypertidy approach to complex data structures aims to bring the goals of the tidyverse to *spatial data* with this single point of perspective: the only thing that makes **geo-spatial data** special is the system of coordinate transformations that provide a family of compromises for generating and working with a particular set of space-properties. All the other aspects that get special attention are completely shared by other domains such as graphics, model structures, grid domains and aspects of user-interactivity and ease of use. Further, the *tidy principles* dictate that the majority of data manipulation and analysis is best handled using *database principles and technologies*, and "geo-spatial" is no different. No special handling is required, and we believe strongly, current idioms and established practices involving special handling hinder innovation, education and understanding generally. Other fields have essentially solved all of the main problems in data analysis, handling and user-interaction but traditions in other fields are preventing the use of these solutions in optimal ways. 

This applies to drawings, GIS vector points, lines, areas, simple features, segment-based linear paths, triangulations and other forms of meshes, and we consider them all to be one of a *piecewise linear complex* or a *simplicial complex*, with (this bit is crucial) *further levels of organization within and between primitive components*. 

Recent legacy optimizations made in geo-spatial fields have seen a strong focus on the *path*, which is an ordered sequence of coordinates, and the path is implicit, defined by "joining the dots" between each coordinate. There is a *dual* to the path, which is an unordered set of *edges* (a.k.a. line segments) where each pair of coordinates traversed by an edge is reference implicitly *by name*. 

This provides a *set of forms* for complex structures that collectively allows generic transformation workflows. 

* 0. Bespoke formats. This is what we have, there are many. 
* 1. Structural vertex-instance set and path-geometry map. 
* 2. Normal form path topology. 
* 3. simplicial complex forms

The last two here include vertex-topology, in that each vertex is a unique coordinate and may be referenced multiple times. 1 is a special case for transition between path based forms
