Postgres supply different indexing ways. Besides simple B-trees there a whole of bunch another accession methods.

- **Hash** - hashing based index. Unlike in B-trees, these indexes just use equality checking.  in many cases hash indexes could be more compact and efficient.  
- **GIST** (Generalized Search Tree) - generalized balanced search tree is used for data, which do not accept any ordering. As an example we could look at R-trees for indexing dots on plane with fast searching of neighbors possibility (k-NN search) and indexing interval's interception operations.
- **SP-GIST** (space-partitioned Generalized Search Tree) - generalized unbalanced index, which is based on dividing area of values on non-overlapping folded areas. For example, quadrant tree for data creation and prefix tree for text lines.
- **GIN** (Generalized Inverted Index) - this type of index is used for complex values, consisting of elements. General sphere of using is full-text searching, where we should search documents, which contains words defined in searching query. Another example of using could be case of searching values in arrays of data.
- RUM - GIN's extension for full-text searching. This index allows accelerate phrase search and return in time relevant ordered results. RUM is supplied as extenssion.
- **BRIN** (Block Range Index) - compact structure allowing find balance between index size and searching speed. It very efficient with big and clustered tables.
- Bloom - Bloom's filter based index. Such index with compact presentation allows quickly cut off unnecessary rows, but requires verification of the remaining.

Many types of indexes could be created not only for single column but also for multiple columns. Independently of type we can create indexes based on columns and based on arbitrary expressions, also create partial indexes just for special rows. Covering indexes wllows speed up queries due to the fact that all necessary data is retrieved from the index itself without necessary data are retrieved from the index itself without table access. 

Moreover, scheduler can use scanning with bit map, which allows join several indexes for accelerated access. 