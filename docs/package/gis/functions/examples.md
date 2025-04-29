# Examples

|   |   |
|---|---|
|[runoff](#runoff)|Implementation of a simple runoff model.|

## [runoff](./examples/runoff.lua)

Implementation of a simple runoff model. It uses a cellular data created from a tiff file (cabecadeboi.shp). The Neighborhood of a Cell is composed by its Moore neighbors that have lower height. There is an initial rain of 10mm in the highest cells. Each cell then sends its water equally to its neighbors.