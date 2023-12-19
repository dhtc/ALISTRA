# ALISTRA
Analysis of LIneage-Specific TRAjectories

This package allows isolating trajecory branches corresonding to individual lineages, identifying lineage-specific dynamically expressed genes, classifying genes based on their expression pattern and plotting gene expression along multiple lineages.

# Tutorial
## Monocle object import and isolating lineages
1) After building trajectories with Monocle, import Monocle object:
> cds = import_monocle(cds)

2) Display nodes of the trajectory graph:
> node_plot(cds)

If the nodes are too dense to see, filter = T option can be used to skip non-terminal and non-branching nodes, and the node density can be set with option N. Larger N skips more nodes.

3) If necessary, connect nodes that you believe should be part of one branch based on biological assumptions, but were not joined by Monocle:
> cds <- connect_nodes(cds, "Y_790", "Y_550")

4) Isolate graph for a selected lineage by setting the start and end nodes. Nodes should be used as integers here.
> lineage = "lineage_name"
> 
> start = 1521
> 
> end = 247
> 
> cds<- isolate_graph(cds, start, end, lineage)

5) Select cells along the graph for the lineage:
> lineage = "lineage_name"
> 
> cds<- isolate_lineage(cds, lineage)

The fuction can also be configured to select cells in a smaller or larger radius around each node by changing the parameter N (default is 10).

If cells should only be selected from certain clusters, sel_clusters parameter can be used.

Finally, the function allows for multithreading by setting the cl parameter to number of threads.

6) Monocle object for each separate lineage can be isolated for plotting or downstream analysis:
> start = 1521
> 
> cds_sub = get_lineage_object(cds, "lineage_name", 2980)

Where start is the starting node in the lineage.

7) Finally, after all desired lineaged have been selected, they can be combined into one graph, and the rest of original graph branches built by Monocle will be ignored:
> start = 1521
>
> cds <- combine_lineages(cds, start)

start should be set to the common starting point of trajectories to recalculate pseudotime.

)8 repo, dhtc/meta-tracker


