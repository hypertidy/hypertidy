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
- [x] finish edge and arc-node workers


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

There are several required forms. It's not clear to me that the below is a sequence, for example arc-node is not necessarily a good pathway from 3 to 5, since 4 is an specialization of planar linear forms for polygons or networks, not an required intermediate. 

1 and 2 suffer from requiring an implicit or structural order for the sequence of coordinates within a path. 

1. Paths in multiple tables with a form of structure index, a *run-length* map. This is what sc_coord, sc_path, and sc_object provide. 
2. Relational paths, no structural index and no de-duplication, all that is needed is vertex, path, object. 
3. Relational paths normalized by vertex, requires a path_link_vertex table to link the path and de-duplicated vertices. 
4. Relational paths normalized by vertex and by path. It's probably never worth normalizing a polgonal path, but it is worth it for arc-node models, such as TopoJSON, OSM ways, and the data at the core of the maps package. 
5. Relational directed linear segments, first form treats segments in the way that 2 treat coordinates - no de-duplication, and so the path is record with the segment ID.  
6. Relational undirected linear segments, this second form de-duplicates segments, ignoring their orientation, and requires a new link table between segment and path (that is where the orientatoin could be stored, if it's needed). (This is what TopoJSON does, storing a 1 or -1 for orientation. 
7. Relational triangles, composed of segments. 
8. Relational triangles, forget the segments. 
9. Higher forms? 



path 
 - same for polygons and lines and points
 - involves normalization of vertices, but maybe it should not
 - object, path, coordinate 
 - combining paths is trivial, possibly is the lowest common denom for merging


path_topological
 - could involve vertex normalization
 - arc normalization? 
 - how to record/infer closed paths, probably is explicit?
 - object, path, coordinate, vertex
 - combining these is tough, need first to 
   -- expand all coords?
   -- normalize vertices of separete inputs, then merge?
  
: arc normalization is problematic I think, does it imply segment normalizatoin first?

: is part of the key here to keep links to the inputs as they were? 

segment / 1D primitive
 - true edge graph
 - definitely requires node inference and inclusion

triangles / 2D primitive
 - segment is truly a prerequisite
 - CGAL seems prone to duplicates and cross over segs



Inputs? 
  
  - lines and lines, needs noding result is 

