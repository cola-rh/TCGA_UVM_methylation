cola Report for Hierarchical Partitioning - 'TCGA_UVM_methylation'
==================

**Date**: 2021-07-22 16:19:52 CEST, **cola version**: 1.9.4

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary



First the variable is renamed to `res_rh`.


```r
res_rh = rh
```



The partition hierarchy and all available functions which can be applied to `res_rh` object.


```r
res_rh
```

```
#> A 'HierarchicalPartition' object with 4 combinations of top-value methods and partitioning methods.
#>   On a matrix with 376006 rows and 80 columns.
#>   Performed in total 22400 partitions.
#>   There are 11 groups under the following parameters:
#>     - min_samples: 6
#>     - mean_silhouette_cutoff: 0.9
#>     - min_n_signatures: 1000 (signatures are selected based on:)
#>       - fdr_cutoff: 0.05
#>       - group_diff: 0.25
#> 
#> Hierarchy of the partition:
#>   0, 80 cols
#>   |-- 01, 24 cols, 4276 signatures
#>   |   |-- 011, 5 cols (b)
#>   |   |-- 012, 12 cols, 945 signatures (c)
#>   |   `-- 013, 7 cols (b)
#>   |-- 02, 35 cols, 4260 signatures
#>   |   |-- 021, 14 cols, 1491 signatures
#>   |   |   |-- 0211, 7 cols (b)
#>   |   |   |-- 0212, 5 cols (b)
#>   |   |   `-- 0213, 2 cols (b)
#>   |   |-- 022, 11 cols (b)
#>   |   `-- 023, 10 cols (b)
#>   |-- 03, 16 cols, 2201 signatures
#>   |   |-- 031, 11 cols (b)
#>   |   `-- 032, 5 cols (b)
#>   `-- 04, 5 cols (b)
#> Stop reason:
#>   b) Subgroup had too few columns.
#>   c) There were too few signatures.
#> 
#> Following methods can be applied to this 'HierarchicalPartition' object:
#>  [1] "all_leaves"            "all_nodes"             "cola_report"           "collect_classes"      
#>  [5] "colnames"              "compare_signatures"    "dimension_reduction"   "functional_enrichment"
#>  [9] "get_anno_col"          "get_anno"              "get_children_nodes"    "get_classes"          
#> [13] "get_matrix"            "get_signatures"        "is_leaf_node"          "max_depth"            
#> [17] "merge_node"            "ncol"                  "node_info"             "node_level"           
#> [21] "nrow"                  "rownames"              "show"                  "split_node"           
#> [25] "suggest_best_k"        "test_to_known_factors" "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single node by e.g. object["01"]
```

The call of `hierarchical_partition()` was:


```
#> hierarchical_partition(data = mat, top_n = 1000, top_value_method = c("SD", "ATC"), 
#>     partition_method = c("kmeans", "skmeans"), subset = 500, group_diff = 0.25, min_n_signatures = 1000, 
#>     filter_fun = function(mat) {
#>         s = rowSds(mat)
#>         order(-s)[1:30000]
#>     }, max_k = 8, scale_rows = FALSE, cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_rh)
dim(mat)
```

```
#> [1] 376006     80
```

All the methods that were tried:


```r
res_rh@param$combination_method
```

```
#> [[1]]
#> [1] "SD"     "kmeans"
#> 
#> [[2]]
#> [1] "ATC"    "kmeans"
#> 
#> [[3]]
#> [1] "SD"      "skmeans"
#> 
#> [[4]]
#> [1] "ATC"     "skmeans"
```

### Density distribution

The density distribution for each sample is visualized as one column in the following heatmap.
The clustering is based on the distance which is the Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 1)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)



Some values about the hierarchy:


```r
all_nodes(res_rh)
```

```
#>  [1] "0"    "01"   "011"  "012"  "013"  "02"   "021"  "0211" "0212" "0213" "022"  "023"  "03"  
#> [14] "031"  "032"  "04"
```

```r
all_leaves(res_rh)
```

```
#>  [1] "011"  "012"  "013"  "0211" "0212" "0213" "022"  "023"  "031"  "032"  "04"
```

```r
node_info(res_rh)
```

```
#>      id best_method depth best_k n_columns n_signatures p_signatures is_leaf
#> 1     0 ATC:skmeans     1      4        80        22227      0.05911   FALSE
#> 2    01 ATC:skmeans     2      3        24         4276      0.01137   FALSE
#> 3   011 not applied     3     NA         5           NA           NA    TRUE
#> 4   012   SD:kmeans     3      2        12          945      0.00251    TRUE
#> 5   013 not applied     3     NA         7           NA           NA    TRUE
#> 6    02 ATC:skmeans     2      3        35         4260      0.01133   FALSE
#> 7   021   SD:kmeans     3      3        14         1491      0.00397   FALSE
#> 8  0211 not applied     4     NA         7           NA           NA    TRUE
#> 9  0212 not applied     4     NA         5           NA           NA    TRUE
#> 10 0213 not applied     4     NA         2           NA           NA    TRUE
#> 11  022 not applied     3     NA        11           NA           NA    TRUE
#> 12  023 not applied     3     NA        10           NA           NA    TRUE
#> 13   03  ATC:kmeans     2      2        16         2201      0.00585   FALSE
#> 14  031 not applied     3     NA        11           NA           NA    TRUE
#> 15  032 not applied     3     NA         5           NA           NA    TRUE
#> 16   04 not applied     2     NA         5           NA           NA    TRUE
```

In the output from `node_info()`, there are the following columns:

- `id`: The node id.
- `best_method`: The best method selected.
- `depth`: Depth of the node in the hierarchy.
- `best_k`: Best number of groups of the partition on that node.
- `n_columns`: Number of columns in the submatrix.
- `n_signatures`: Number of signatures with the `best_k`.
- `p_signatures`: Proportion of hte signatures in total number of rows in the matrix.
- `is_leaf`: Whether the node is a leaf.

Labels of nodes are encoded in a special way. The number of digits
correspond to the depth of the node in the hierarchy and the value of the
digits correspond to the index of the subgroup in the current node, E.g. a label
of “012” means the node is the second subgroup of the partition which is the
first subgroup of the root node.

### Suggest the best k



Following table shows the best `k` (number of partitions) for each node in the
partition hierarchy. Clicking on the node name in the table goes to the
corresponding section for the partitioning on that node.

[The cola vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.



```r
suggest_best_k(res_rh)
```


|Node                |Best method                                         |Is leaf   |Best k |1-PAC |Mean silhouette |Concordance | #samples|   |
|:-------------------|:---------------------------------------------------|:---------|:------|:-----|:---------------|:-----------|--------:|:--|
|[Node0](#Node0)     |ATC:skmeans                                         |          |4      |1.00  |0.99            |0.99        |       80|** |
|[Node01](#Node01)   |ATC:skmeans                                         |          |3      |1.00  |0.98            |0.99        |       24|** |
|Node011-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        5|   |
|Node012-leaf        |SD:kmeans                                           |✓ (&#99;) |3      |0.94  |0.95            |0.98        |       12|*  |
|Node013-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        7|   |
|[Node02](#Node02)   |ATC:skmeans                                         |          |2      |1.00  |1.00            |1.00        |       35|** |
|[Node021](#Node021) |SD:kmeans                                           |          |3      |1.00  |0.99            |1.00        |       14|** |
|Node0211-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        7|   |
|Node0212-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        5|   |
|Node0213-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        2|   |
|Node022-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |       11|   |
|Node023-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |       10|   |
|[Node03](#Node03)   |ATC:kmeans                                          |          |2      |1.00  |1.00            |1.00        |       16|** |
|Node031-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |       11|   |
|Node032-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        5|   |
|Node04-leaf         |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        5|   |


Stop reason: b) Subgroup had too few columns. c) There were too few signatures. 

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9


### Partition hierarchy

The nodes of the hierarchy can be merged by setting the `merge_node` parameters. Here we 
control the hierarchy with the `min_n_signatures` parameter. The value of `min_n_signatures` is
from `node_info()`.





<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-classes-from-hierarchical-partition' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-hierarchical-partition'>
<ul>
<li><a href='#tab-collect-classes-from-hierarchical-partition-1'>n_signatures ≥ 1491</a></li>
<li><a href='#tab-collect-classes-from-hierarchical-partition-2'>n_signatures ≥ 2201</a></li>
<li><a href='#tab-collect-classes-from-hierarchical-partition-3'>n_signatures ≥ 4260</a></li>
<li><a href='#tab-collect-classes-from-hierarchical-partition-4'>n_signatures ≥ 4276</a></li>
<li><a href='#tab-collect-classes-from-hierarchical-partition-5'>n_signatures ≥ 22227</a></li>
</ul>
<div id='tab-collect-classes-from-hierarchical-partition-1'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 1491))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-1-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-1"/></p>

</div>
<div id='tab-collect-classes-from-hierarchical-partition-2'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 2201))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-2-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-2"/></p>

</div>
<div id='tab-collect-classes-from-hierarchical-partition-3'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 4260))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-3-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-3"/></p>

</div>
<div id='tab-collect-classes-from-hierarchical-partition-4'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 4276))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-4-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-4"/></p>

</div>
<div id='tab-collect-classes-from-hierarchical-partition-5'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 22227))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-5-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-5"/></p>

</div>
</div>

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it).


<script>
$( function() {
	$( '#tabs-get-classes-from-hierarchical-partition' ).tabs();
} );
</script>
<div id='tabs-get-classes-from-hierarchical-partition'>
<ul>
<li><a href='#tab-get-classes-from-hierarchical-partition-1'>n_signatures ≥ 1491</a></li>
<li><a href='#tab-get-classes-from-hierarchical-partition-2'>n_signatures ≥ 2201</a></li>
<li><a href='#tab-get-classes-from-hierarchical-partition-3'>n_signatures ≥ 4260</a></li>
<li><a href='#tab-get-classes-from-hierarchical-partition-4'>n_signatures ≥ 4276</a></li>
<li><a href='#tab-get-classes-from-hierarchical-partition-5'>n_signatures ≥ 22227</a></li>
</ul>

<div id='tab-get-classes-from-hierarchical-partition-1'>
<p><a id='tab-get-classes-from-hierarchical-partition-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 1491))
</code></pre>

<pre><code>#&gt; TCGA.V4.A9EX.01 TCGA.V4.A9E5.01 TCGA.V4.A9EZ.01 TCGA.WC.A885.01 TCGA.V4.A9F3.01 TCGA.V4.A9EU.01 
#&gt;           &quot;011&quot;            &quot;04&quot;           &quot;023&quot;          &quot;0211&quot;           &quot;012&quot;           &quot;011&quot; 
#&gt; TCGA.V4.A9ET.01 TCGA.V4.A9F7.01 TCGA.V4.A9F1.01 TCGA.V4.A9F4.01 TCGA.YZ.A980.01 TCGA.VD.A8KJ.01 
#&gt;          &quot;0212&quot;           &quot;022&quot;           &quot;012&quot;          &quot;0212&quot;           &quot;031&quot;           &quot;022&quot; 
#&gt; TCGA.V3.A9ZX.01 TCGA.WC.AA9A.01 TCGA.VD.AA8T.01 TCGA.V4.A9EW.01 TCGA.WC.A880.01 TCGA.WC.A881.01 
#&gt;           &quot;013&quot;           &quot;031&quot;           &quot;032&quot;           &quot;023&quot;           &quot;022&quot;          &quot;0212&quot; 
#&gt; TCGA.V3.A9ZY.01 TCGA.WC.AA9E.01 TCGA.V4.A9EV.01 TCGA.V4.A9E9.01 TCGA.V4.A9E8.01 TCGA.VD.A8KB.01 
#&gt;           &quot;023&quot;          &quot;0212&quot;           &quot;012&quot;          &quot;0211&quot;           &quot;031&quot;          &quot;0212&quot; 
#&gt; TCGA.VD.A8KL.01 TCGA.VD.A8KG.01 TCGA.VD.AA8M.01 TCGA.WC.A882.01 TCGA.V4.A9EO.01 TCGA.VD.A8KI.01 
#&gt;           &quot;032&quot;          &quot;0211&quot;           &quot;022&quot;            &quot;04&quot;           &quot;031&quot;           &quot;013&quot; 
#&gt; TCGA.V4.A9F2.01 TCGA.V4.A9EQ.01 TCGA.VD.A8K8.01 TCGA.V4.A9EL.01 TCGA.V4.A9EI.01 TCGA.VD.AA8S.01 
#&gt;            &quot;04&quot;           &quot;012&quot;           &quot;012&quot;           &quot;013&quot;           &quot;011&quot;           &quot;022&quot; 
#&gt; TCGA.V4.A9EC.01 TCGA.V4.A9ED.01 TCGA.V4.A9ES.01 TCGA.YZ.A985.01 TCGA.V4.A9F0.01 TCGA.V4.A9E7.01 
#&gt;           &quot;022&quot;           &quot;031&quot;           &quot;031&quot;           &quot;032&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.VD.A8KN.01 TCGA.VD.A8KK.01 TCGA.V4.A9EM.01 TCGA.VD.AA8Q.01 TCGA.VD.A8K9.01 TCGA.WC.A888.01 
#&gt;           &quot;031&quot;           &quot;031&quot;            &quot;04&quot;           &quot;022&quot;          &quot;0211&quot;           &quot;031&quot; 
#&gt; TCGA.VD.AA8R.01 TCGA.VD.A8KH.01 TCGA.RZ.AB0B.01 TCGA.V4.A9EJ.01 TCGA.VD.A8K7.01 TCGA.VD.AA8O.01 
#&gt;           &quot;023&quot;           &quot;023&quot;           &quot;013&quot;          &quot;0211&quot;           &quot;023&quot;           &quot;012&quot; 
#&gt; TCGA.VD.A8KA.01 TCGA.V4.A9EK.01 TCGA.V4.A9F8.01 TCGA.YZ.A984.01 TCGA.VD.A8KD.01 TCGA.YZ.A982.01 
#&gt;          &quot;0211&quot;          &quot;0213&quot;           &quot;031&quot;           &quot;032&quot;           &quot;012&quot;          &quot;0213&quot; 
#&gt; TCGA.WC.A88A.01 TCGA.WC.A87W.01 TCGA.V4.A9EH.01 TCGA.WC.A87U.01 TCGA.YZ.A983.01 TCGA.V4.A9EY.01 
#&gt;           &quot;011&quot;            &quot;04&quot;           &quot;023&quot;           &quot;023&quot;           &quot;022&quot;           &quot;022&quot; 
#&gt; TCGA.WC.A87T.01 TCGA.VD.AA8N.01 TCGA.VD.A8KM.01 TCGA.VD.AA8P.01 TCGA.V4.A9EF.01 TCGA.V4.A9EE.01 
#&gt;           &quot;023&quot;           &quot;013&quot;           &quot;012&quot;           &quot;032&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.WC.A87Y.01 TCGA.VD.A8KE.01 TCGA.VD.A8KF.01 TCGA.VD.A8KO.01 TCGA.WC.A883.01 TCGA.V4.A9EA.01 
#&gt;           &quot;012&quot;           &quot;022&quot;           &quot;031&quot;           &quot;023&quot;           &quot;011&quot;          &quot;0211&quot; 
#&gt; TCGA.WC.A884.01 TCGA.V4.A9F5.01 
#&gt;           &quot;022&quot;           &quot;012&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-1-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-1-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-get-classes-from-hierarchical-partition-2'>
<p><a id='tab-get-classes-from-hierarchical-partition-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 2201))
</code></pre>

<pre><code>#&gt; TCGA.V4.A9EX.01 TCGA.V4.A9E5.01 TCGA.V4.A9EZ.01 TCGA.WC.A885.01 TCGA.V4.A9F3.01 TCGA.V4.A9EU.01 
#&gt;           &quot;011&quot;            &quot;04&quot;           &quot;023&quot;           &quot;021&quot;           &quot;012&quot;           &quot;011&quot; 
#&gt; TCGA.V4.A9ET.01 TCGA.V4.A9F7.01 TCGA.V4.A9F1.01 TCGA.V4.A9F4.01 TCGA.YZ.A980.01 TCGA.VD.A8KJ.01 
#&gt;           &quot;021&quot;           &quot;022&quot;           &quot;012&quot;           &quot;021&quot;           &quot;031&quot;           &quot;022&quot; 
#&gt; TCGA.V3.A9ZX.01 TCGA.WC.AA9A.01 TCGA.VD.AA8T.01 TCGA.V4.A9EW.01 TCGA.WC.A880.01 TCGA.WC.A881.01 
#&gt;           &quot;013&quot;           &quot;031&quot;           &quot;032&quot;           &quot;023&quot;           &quot;022&quot;           &quot;021&quot; 
#&gt; TCGA.V3.A9ZY.01 TCGA.WC.AA9E.01 TCGA.V4.A9EV.01 TCGA.V4.A9E9.01 TCGA.V4.A9E8.01 TCGA.VD.A8KB.01 
#&gt;           &quot;023&quot;           &quot;021&quot;           &quot;012&quot;           &quot;021&quot;           &quot;031&quot;           &quot;021&quot; 
#&gt; TCGA.VD.A8KL.01 TCGA.VD.A8KG.01 TCGA.VD.AA8M.01 TCGA.WC.A882.01 TCGA.V4.A9EO.01 TCGA.VD.A8KI.01 
#&gt;           &quot;032&quot;           &quot;021&quot;           &quot;022&quot;            &quot;04&quot;           &quot;031&quot;           &quot;013&quot; 
#&gt; TCGA.V4.A9F2.01 TCGA.V4.A9EQ.01 TCGA.VD.A8K8.01 TCGA.V4.A9EL.01 TCGA.V4.A9EI.01 TCGA.VD.AA8S.01 
#&gt;            &quot;04&quot;           &quot;012&quot;           &quot;012&quot;           &quot;013&quot;           &quot;011&quot;           &quot;022&quot; 
#&gt; TCGA.V4.A9EC.01 TCGA.V4.A9ED.01 TCGA.V4.A9ES.01 TCGA.YZ.A985.01 TCGA.V4.A9F0.01 TCGA.V4.A9E7.01 
#&gt;           &quot;022&quot;           &quot;031&quot;           &quot;031&quot;           &quot;032&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.VD.A8KN.01 TCGA.VD.A8KK.01 TCGA.V4.A9EM.01 TCGA.VD.AA8Q.01 TCGA.VD.A8K9.01 TCGA.WC.A888.01 
#&gt;           &quot;031&quot;           &quot;031&quot;            &quot;04&quot;           &quot;022&quot;           &quot;021&quot;           &quot;031&quot; 
#&gt; TCGA.VD.AA8R.01 TCGA.VD.A8KH.01 TCGA.RZ.AB0B.01 TCGA.V4.A9EJ.01 TCGA.VD.A8K7.01 TCGA.VD.AA8O.01 
#&gt;           &quot;023&quot;           &quot;023&quot;           &quot;013&quot;           &quot;021&quot;           &quot;023&quot;           &quot;012&quot; 
#&gt; TCGA.VD.A8KA.01 TCGA.V4.A9EK.01 TCGA.V4.A9F8.01 TCGA.YZ.A984.01 TCGA.VD.A8KD.01 TCGA.YZ.A982.01 
#&gt;           &quot;021&quot;           &quot;021&quot;           &quot;031&quot;           &quot;032&quot;           &quot;012&quot;           &quot;021&quot; 
#&gt; TCGA.WC.A88A.01 TCGA.WC.A87W.01 TCGA.V4.A9EH.01 TCGA.WC.A87U.01 TCGA.YZ.A983.01 TCGA.V4.A9EY.01 
#&gt;           &quot;011&quot;            &quot;04&quot;           &quot;023&quot;           &quot;023&quot;           &quot;022&quot;           &quot;022&quot; 
#&gt; TCGA.WC.A87T.01 TCGA.VD.AA8N.01 TCGA.VD.A8KM.01 TCGA.VD.AA8P.01 TCGA.V4.A9EF.01 TCGA.V4.A9EE.01 
#&gt;           &quot;023&quot;           &quot;013&quot;           &quot;012&quot;           &quot;032&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.WC.A87Y.01 TCGA.VD.A8KE.01 TCGA.VD.A8KF.01 TCGA.VD.A8KO.01 TCGA.WC.A883.01 TCGA.V4.A9EA.01 
#&gt;           &quot;012&quot;           &quot;022&quot;           &quot;031&quot;           &quot;023&quot;           &quot;011&quot;           &quot;021&quot; 
#&gt; TCGA.WC.A884.01 TCGA.V4.A9F5.01 
#&gt;           &quot;022&quot;           &quot;012&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-2-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-2-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-get-classes-from-hierarchical-partition-3'>
<p><a id='tab-get-classes-from-hierarchical-partition-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 4260))
</code></pre>

<pre><code>#&gt; TCGA.V4.A9EX.01 TCGA.V4.A9E5.01 TCGA.V4.A9EZ.01 TCGA.WC.A885.01 TCGA.V4.A9F3.01 TCGA.V4.A9EU.01 
#&gt;           &quot;011&quot;            &quot;04&quot;           &quot;023&quot;           &quot;021&quot;           &quot;012&quot;           &quot;011&quot; 
#&gt; TCGA.V4.A9ET.01 TCGA.V4.A9F7.01 TCGA.V4.A9F1.01 TCGA.V4.A9F4.01 TCGA.YZ.A980.01 TCGA.VD.A8KJ.01 
#&gt;           &quot;021&quot;           &quot;022&quot;           &quot;012&quot;           &quot;021&quot;            &quot;03&quot;           &quot;022&quot; 
#&gt; TCGA.V3.A9ZX.01 TCGA.WC.AA9A.01 TCGA.VD.AA8T.01 TCGA.V4.A9EW.01 TCGA.WC.A880.01 TCGA.WC.A881.01 
#&gt;           &quot;013&quot;            &quot;03&quot;            &quot;03&quot;           &quot;023&quot;           &quot;022&quot;           &quot;021&quot; 
#&gt; TCGA.V3.A9ZY.01 TCGA.WC.AA9E.01 TCGA.V4.A9EV.01 TCGA.V4.A9E9.01 TCGA.V4.A9E8.01 TCGA.VD.A8KB.01 
#&gt;           &quot;023&quot;           &quot;021&quot;           &quot;012&quot;           &quot;021&quot;            &quot;03&quot;           &quot;021&quot; 
#&gt; TCGA.VD.A8KL.01 TCGA.VD.A8KG.01 TCGA.VD.AA8M.01 TCGA.WC.A882.01 TCGA.V4.A9EO.01 TCGA.VD.A8KI.01 
#&gt;            &quot;03&quot;           &quot;021&quot;           &quot;022&quot;            &quot;04&quot;            &quot;03&quot;           &quot;013&quot; 
#&gt; TCGA.V4.A9F2.01 TCGA.V4.A9EQ.01 TCGA.VD.A8K8.01 TCGA.V4.A9EL.01 TCGA.V4.A9EI.01 TCGA.VD.AA8S.01 
#&gt;            &quot;04&quot;           &quot;012&quot;           &quot;012&quot;           &quot;013&quot;           &quot;011&quot;           &quot;022&quot; 
#&gt; TCGA.V4.A9EC.01 TCGA.V4.A9ED.01 TCGA.V4.A9ES.01 TCGA.YZ.A985.01 TCGA.V4.A9F0.01 TCGA.V4.A9E7.01 
#&gt;           &quot;022&quot;            &quot;03&quot;            &quot;03&quot;            &quot;03&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.VD.A8KN.01 TCGA.VD.A8KK.01 TCGA.V4.A9EM.01 TCGA.VD.AA8Q.01 TCGA.VD.A8K9.01 TCGA.WC.A888.01 
#&gt;            &quot;03&quot;            &quot;03&quot;            &quot;04&quot;           &quot;022&quot;           &quot;021&quot;            &quot;03&quot; 
#&gt; TCGA.VD.AA8R.01 TCGA.VD.A8KH.01 TCGA.RZ.AB0B.01 TCGA.V4.A9EJ.01 TCGA.VD.A8K7.01 TCGA.VD.AA8O.01 
#&gt;           &quot;023&quot;           &quot;023&quot;           &quot;013&quot;           &quot;021&quot;           &quot;023&quot;           &quot;012&quot; 
#&gt; TCGA.VD.A8KA.01 TCGA.V4.A9EK.01 TCGA.V4.A9F8.01 TCGA.YZ.A984.01 TCGA.VD.A8KD.01 TCGA.YZ.A982.01 
#&gt;           &quot;021&quot;           &quot;021&quot;            &quot;03&quot;            &quot;03&quot;           &quot;012&quot;           &quot;021&quot; 
#&gt; TCGA.WC.A88A.01 TCGA.WC.A87W.01 TCGA.V4.A9EH.01 TCGA.WC.A87U.01 TCGA.YZ.A983.01 TCGA.V4.A9EY.01 
#&gt;           &quot;011&quot;            &quot;04&quot;           &quot;023&quot;           &quot;023&quot;           &quot;022&quot;           &quot;022&quot; 
#&gt; TCGA.WC.A87T.01 TCGA.VD.AA8N.01 TCGA.VD.A8KM.01 TCGA.VD.AA8P.01 TCGA.V4.A9EF.01 TCGA.V4.A9EE.01 
#&gt;           &quot;023&quot;           &quot;013&quot;           &quot;012&quot;            &quot;03&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.WC.A87Y.01 TCGA.VD.A8KE.01 TCGA.VD.A8KF.01 TCGA.VD.A8KO.01 TCGA.WC.A883.01 TCGA.V4.A9EA.01 
#&gt;           &quot;012&quot;           &quot;022&quot;            &quot;03&quot;           &quot;023&quot;           &quot;011&quot;           &quot;021&quot; 
#&gt; TCGA.WC.A884.01 TCGA.V4.A9F5.01 
#&gt;           &quot;022&quot;           &quot;012&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-3-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-3-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-get-classes-from-hierarchical-partition-4'>
<p><a id='tab-get-classes-from-hierarchical-partition-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 4276))
</code></pre>

<pre><code>#&gt; TCGA.V4.A9EX.01 TCGA.V4.A9E5.01 TCGA.V4.A9EZ.01 TCGA.WC.A885.01 TCGA.V4.A9F3.01 TCGA.V4.A9EU.01 
#&gt;           &quot;011&quot;            &quot;04&quot;            &quot;02&quot;            &quot;02&quot;           &quot;012&quot;           &quot;011&quot; 
#&gt; TCGA.V4.A9ET.01 TCGA.V4.A9F7.01 TCGA.V4.A9F1.01 TCGA.V4.A9F4.01 TCGA.YZ.A980.01 TCGA.VD.A8KJ.01 
#&gt;            &quot;02&quot;            &quot;02&quot;           &quot;012&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot; 
#&gt; TCGA.V3.A9ZX.01 TCGA.WC.AA9A.01 TCGA.VD.AA8T.01 TCGA.V4.A9EW.01 TCGA.WC.A880.01 TCGA.WC.A881.01 
#&gt;           &quot;013&quot;            &quot;03&quot;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.V3.A9ZY.01 TCGA.WC.AA9E.01 TCGA.V4.A9EV.01 TCGA.V4.A9E9.01 TCGA.V4.A9E8.01 TCGA.VD.A8KB.01 
#&gt;            &quot;02&quot;            &quot;02&quot;           &quot;012&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot; 
#&gt; TCGA.VD.A8KL.01 TCGA.VD.A8KG.01 TCGA.VD.AA8M.01 TCGA.WC.A882.01 TCGA.V4.A9EO.01 TCGA.VD.A8KI.01 
#&gt;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;04&quot;            &quot;03&quot;           &quot;013&quot; 
#&gt; TCGA.V4.A9F2.01 TCGA.V4.A9EQ.01 TCGA.VD.A8K8.01 TCGA.V4.A9EL.01 TCGA.V4.A9EI.01 TCGA.VD.AA8S.01 
#&gt;            &quot;04&quot;           &quot;012&quot;           &quot;012&quot;           &quot;013&quot;           &quot;011&quot;            &quot;02&quot; 
#&gt; TCGA.V4.A9EC.01 TCGA.V4.A9ED.01 TCGA.V4.A9ES.01 TCGA.YZ.A985.01 TCGA.V4.A9F0.01 TCGA.V4.A9E7.01 
#&gt;            &quot;02&quot;            &quot;03&quot;            &quot;03&quot;            &quot;03&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.VD.A8KN.01 TCGA.VD.A8KK.01 TCGA.V4.A9EM.01 TCGA.VD.AA8Q.01 TCGA.VD.A8K9.01 TCGA.WC.A888.01 
#&gt;            &quot;03&quot;            &quot;03&quot;            &quot;04&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot; 
#&gt; TCGA.VD.AA8R.01 TCGA.VD.A8KH.01 TCGA.RZ.AB0B.01 TCGA.V4.A9EJ.01 TCGA.VD.A8K7.01 TCGA.VD.AA8O.01 
#&gt;            &quot;02&quot;            &quot;02&quot;           &quot;013&quot;            &quot;02&quot;            &quot;02&quot;           &quot;012&quot; 
#&gt; TCGA.VD.A8KA.01 TCGA.V4.A9EK.01 TCGA.V4.A9F8.01 TCGA.YZ.A984.01 TCGA.VD.A8KD.01 TCGA.YZ.A982.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;03&quot;           &quot;012&quot;            &quot;02&quot; 
#&gt; TCGA.WC.A88A.01 TCGA.WC.A87W.01 TCGA.V4.A9EH.01 TCGA.WC.A87U.01 TCGA.YZ.A983.01 TCGA.V4.A9EY.01 
#&gt;           &quot;011&quot;            &quot;04&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.WC.A87T.01 TCGA.VD.AA8N.01 TCGA.VD.A8KM.01 TCGA.VD.AA8P.01 TCGA.V4.A9EF.01 TCGA.V4.A9EE.01 
#&gt;            &quot;02&quot;           &quot;013&quot;           &quot;012&quot;            &quot;03&quot;           &quot;012&quot;           &quot;013&quot; 
#&gt; TCGA.WC.A87Y.01 TCGA.VD.A8KE.01 TCGA.VD.A8KF.01 TCGA.VD.A8KO.01 TCGA.WC.A883.01 TCGA.V4.A9EA.01 
#&gt;           &quot;012&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot;           &quot;011&quot;            &quot;02&quot; 
#&gt; TCGA.WC.A884.01 TCGA.V4.A9F5.01 
#&gt;            &quot;02&quot;           &quot;012&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-4-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-4-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-get-classes-from-hierarchical-partition-5'>
<p><a id='tab-get-classes-from-hierarchical-partition-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 22227))
</code></pre>

<pre><code>#&gt; TCGA.V4.A9EX.01 TCGA.V4.A9E5.01 TCGA.V4.A9EZ.01 TCGA.WC.A885.01 TCGA.V4.A9F3.01 TCGA.V4.A9EU.01 
#&gt;            &quot;01&quot;            &quot;04&quot;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot;            &quot;01&quot; 
#&gt; TCGA.V4.A9ET.01 TCGA.V4.A9F7.01 TCGA.V4.A9F1.01 TCGA.V4.A9F4.01 TCGA.YZ.A980.01 TCGA.VD.A8KJ.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot; 
#&gt; TCGA.V3.A9ZX.01 TCGA.WC.AA9A.01 TCGA.VD.AA8T.01 TCGA.V4.A9EW.01 TCGA.WC.A880.01 TCGA.WC.A881.01 
#&gt;            &quot;01&quot;            &quot;03&quot;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.V3.A9ZY.01 TCGA.WC.AA9E.01 TCGA.V4.A9EV.01 TCGA.V4.A9E9.01 TCGA.V4.A9E8.01 TCGA.VD.A8KB.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot; 
#&gt; TCGA.VD.A8KL.01 TCGA.VD.A8KG.01 TCGA.VD.AA8M.01 TCGA.WC.A882.01 TCGA.V4.A9EO.01 TCGA.VD.A8KI.01 
#&gt;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;04&quot;            &quot;03&quot;            &quot;01&quot; 
#&gt; TCGA.V4.A9F2.01 TCGA.V4.A9EQ.01 TCGA.VD.A8K8.01 TCGA.V4.A9EL.01 TCGA.V4.A9EI.01 TCGA.VD.AA8S.01 
#&gt;            &quot;04&quot;            &quot;01&quot;            &quot;01&quot;            &quot;01&quot;            &quot;01&quot;            &quot;02&quot; 
#&gt; TCGA.V4.A9EC.01 TCGA.V4.A9ED.01 TCGA.V4.A9ES.01 TCGA.YZ.A985.01 TCGA.V4.A9F0.01 TCGA.V4.A9E7.01 
#&gt;            &quot;02&quot;            &quot;03&quot;            &quot;03&quot;            &quot;03&quot;            &quot;01&quot;            &quot;01&quot; 
#&gt; TCGA.VD.A8KN.01 TCGA.VD.A8KK.01 TCGA.V4.A9EM.01 TCGA.VD.AA8Q.01 TCGA.VD.A8K9.01 TCGA.WC.A888.01 
#&gt;            &quot;03&quot;            &quot;03&quot;            &quot;04&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot; 
#&gt; TCGA.VD.AA8R.01 TCGA.VD.A8KH.01 TCGA.RZ.AB0B.01 TCGA.V4.A9EJ.01 TCGA.VD.A8K7.01 TCGA.VD.AA8O.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot; 
#&gt; TCGA.VD.A8KA.01 TCGA.V4.A9EK.01 TCGA.V4.A9F8.01 TCGA.YZ.A984.01 TCGA.VD.A8KD.01 TCGA.YZ.A982.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;03&quot;            &quot;01&quot;            &quot;02&quot; 
#&gt; TCGA.WC.A88A.01 TCGA.WC.A87W.01 TCGA.V4.A9EH.01 TCGA.WC.A87U.01 TCGA.YZ.A983.01 TCGA.V4.A9EY.01 
#&gt;            &quot;01&quot;            &quot;04&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.WC.A87T.01 TCGA.VD.AA8N.01 TCGA.VD.A8KM.01 TCGA.VD.AA8P.01 TCGA.V4.A9EF.01 TCGA.V4.A9EE.01 
#&gt;            &quot;02&quot;            &quot;01&quot;            &quot;01&quot;            &quot;03&quot;            &quot;01&quot;            &quot;01&quot; 
#&gt; TCGA.WC.A87Y.01 TCGA.VD.A8KE.01 TCGA.VD.A8KF.01 TCGA.VD.A8KO.01 TCGA.WC.A883.01 TCGA.V4.A9EA.01 
#&gt;            &quot;01&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot; 
#&gt; TCGA.WC.A884.01 TCGA.V4.A9F5.01 
#&gt;            &quot;02&quot;            &quot;01&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-5-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-5-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>



### Top rows heatmap

Heatmaps of the top rows:





```r
top_rows_heatmap(res_rh)
```

![plot of chunk top-rows-heatmap](figure_cola/top-rows-heatmap-1.png)

```
#> Error in h(simpleError(msg, call)) : 
#>   error in evaluating the argument 'object' in selecting a method for function 'draw': no applicable method for 'height' applied to an object of class "list"
```

Top rows on each node:


```r
top_rows_overlap(res_rh, method = "upset")
```

![plot of chunk top-rows-overlap](figure_cola/top-rows-overlap-1.png)


### UMAP plot

UMAP plot which shows how samples are separated.




<script>
$( function() {
	$( '#tabs-dimension-reduction-by-depth' ).tabs();
} );
</script>
<div id='tabs-dimension-reduction-by-depth'>
<ul>
<li><a href='#tab-dimension-reduction-by-depth-1'>n_signatures ≥ 1491</a></li>
<li><a href='#tab-dimension-reduction-by-depth-2'>n_signatures ≥ 2201</a></li>
<li><a href='#tab-dimension-reduction-by-depth-3'>n_signatures ≥ 4260</a></li>
<li><a href='#tab-dimension-reduction-by-depth-4'>n_signatures ≥ 4276</a></li>
<li><a href='#tab-dimension-reduction-by-depth-5'>n_signatures ≥ 22227</a></li>
</ul>
<div id='tab-dimension-reduction-by-depth-1'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 1491),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 1491),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-1-1.png" title="plot of chunk tab-dimension-reduction-by-depth-1" alt="plot of chunk tab-dimension-reduction-by-depth-1" width="100%" /></p>

</div>
<div id='tab-dimension-reduction-by-depth-2'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 2201),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 2201),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-2-1.png" title="plot of chunk tab-dimension-reduction-by-depth-2" alt="plot of chunk tab-dimension-reduction-by-depth-2" width="100%" /></p>

</div>
<div id='tab-dimension-reduction-by-depth-3'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 4260),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 4260),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-3-1.png" title="plot of chunk tab-dimension-reduction-by-depth-3" alt="plot of chunk tab-dimension-reduction-by-depth-3" width="100%" /></p>

</div>
<div id='tab-dimension-reduction-by-depth-4'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 4276),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 4276),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-4-1.png" title="plot of chunk tab-dimension-reduction-by-depth-4" alt="plot of chunk tab-dimension-reduction-by-depth-4" width="100%" /></p>

</div>
<div id='tab-dimension-reduction-by-depth-5'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 22227),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 22227),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-5-1.png" title="plot of chunk tab-dimension-reduction-by-depth-5" alt="plot of chunk tab-dimension-reduction-by-depth-5" width="100%" /></p>

</div>
</div>




### Signature heatmap

Signatures on the heatmap are the union of all signatures found on every node
on the hierarchy. The number of k-means on rows are automatically selected by the function.




<script>
$( function() {
	$( '#tabs-get-signatures-from-hierarchical-partition' ).tabs();
} );
</script>
<div id='tabs-get-signatures-from-hierarchical-partition'>
<ul>
<li><a href='#tab-get-signatures-from-hierarchical-partition-1'>n_signatures ≥ 1491</a></li>
<li><a href='#tab-get-signatures-from-hierarchical-partition-2'>n_signatures ≥ 2201</a></li>
<li><a href='#tab-get-signatures-from-hierarchical-partition-3'>n_signatures ≥ 4260</a></li>
<li><a href='#tab-get-signatures-from-hierarchical-partition-4'>n_signatures ≥ 4276</a></li>
<li><a href='#tab-get-signatures-from-hierarchical-partition-5'>n_signatures ≥ 22227</a></li>
</ul>
<div id='tab-get-signatures-from-hierarchical-partition-1'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 1491))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-1-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-1"/></p>

</div>
<div id='tab-get-signatures-from-hierarchical-partition-2'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 2201))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-2-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-2"/></p>

</div>
<div id='tab-get-signatures-from-hierarchical-partition-3'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 4260))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-3-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-3"/></p>

</div>
<div id='tab-get-signatures-from-hierarchical-partition-4'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 4276))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-4-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-4"/></p>

</div>
<div id='tab-get-signatures-from-hierarchical-partition-5'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 22227))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-5-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-5"/></p>

</div>
</div>




Compare signatures from different nodes:


```r
compare_signatures(res_rh, verbose = FALSE)
```

![plot of chunk unnamed-chunk-24](figure_cola/unnamed-chunk-24-1.png)

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs. Note it only works on every node and the final signatures
are the union of all signatures of all nodes.


```r
# code only for demonstration
# e.g. to show the top 500 most significant rows on each node.
tb = get_signature(res_rh, top_signatures = 500)
```


## Results for each node


---------------------------------------------------




### Node0


Child nodes: 
                [Node01](#Node01)
        ,
                [Node02](#Node02)
        ,
                [Node03](#Node03)
        ,
                Node04-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["0"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 80 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-0-collect-plots](figure_cola/node-0-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-0-select-partition-number](figure_cola/node-0-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5068 0.494   0.494
#> 3 3 1.000           0.985       0.995         0.2479 0.861   0.721
#> 4 4 1.000           0.986       0.992         0.0885 0.949   0.862
#> 5 5 0.827           0.714       0.873         0.0750 0.969   0.903
#> 6 6 0.826           0.797       0.878         0.0417 0.917   0.720
#> 7 7 0.833           0.785       0.881         0.0257 0.966   0.852
#> 8 8 0.809           0.750       0.874         0.0109 0.984   0.920
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-0-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-0-get-classes'>
<ul>
<li><a href='#tab-node-0-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-0-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-0-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-0-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-0-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-0-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-0-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-0-get-classes-1'>
<p><a id='tab-node-0-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1 p2
#&gt; TCGA.V4.A9EX.01     1       0          1  1  0
#&gt; TCGA.V4.A9E5.01     2       0          1  0  1
#&gt; TCGA.V4.A9EZ.01     2       0          1  0  1
#&gt; TCGA.WC.A885.01     2       0          1  0  1
#&gt; TCGA.V4.A9F3.01     1       0          1  1  0
#&gt; TCGA.V4.A9EU.01     1       0          1  1  0
#&gt; TCGA.V4.A9ET.01     2       0          1  0  1
#&gt; TCGA.V4.A9F7.01     2       0          1  0  1
#&gt; TCGA.V4.A9F1.01     1       0          1  1  0
#&gt; TCGA.V4.A9F4.01     2       0          1  0  1
#&gt; TCGA.YZ.A980.01     1       0          1  1  0
#&gt; TCGA.VD.A8KJ.01     2       0          1  0  1
#&gt; TCGA.V3.A9ZX.01     1       0          1  1  0
#&gt; TCGA.WC.AA9A.01     1       0          1  1  0
#&gt; TCGA.VD.AA8T.01     1       0          1  1  0
#&gt; TCGA.V4.A9EW.01     2       0          1  0  1
#&gt; TCGA.WC.A880.01     2       0          1  0  1
#&gt; TCGA.WC.A881.01     2       0          1  0  1
#&gt; TCGA.V3.A9ZY.01     2       0          1  0  1
#&gt; TCGA.WC.AA9E.01     2       0          1  0  1
#&gt; TCGA.V4.A9EV.01     1       0          1  1  0
#&gt; TCGA.V4.A9E9.01     2       0          1  0  1
#&gt; TCGA.V4.A9E8.01     1       0          1  1  0
#&gt; TCGA.VD.A8KB.01     2       0          1  0  1
#&gt; TCGA.VD.A8KL.01     1       0          1  1  0
#&gt; TCGA.VD.A8KG.01     2       0          1  0  1
#&gt; TCGA.VD.AA8M.01     2       0          1  0  1
#&gt; TCGA.WC.A882.01     2       0          1  0  1
#&gt; TCGA.V4.A9EO.01     1       0          1  1  0
#&gt; TCGA.VD.A8KI.01     1       0          1  1  0
#&gt; TCGA.V4.A9F2.01     2       0          1  0  1
#&gt; TCGA.V4.A9EQ.01     1       0          1  1  0
#&gt; TCGA.VD.A8K8.01     1       0          1  1  0
#&gt; TCGA.V4.A9EL.01     1       0          1  1  0
#&gt; TCGA.V4.A9EI.01     1       0          1  1  0
#&gt; TCGA.VD.AA8S.01     2       0          1  0  1
#&gt; TCGA.V4.A9EC.01     2       0          1  0  1
#&gt; TCGA.V4.A9ED.01     1       0          1  1  0
#&gt; TCGA.V4.A9ES.01     1       0          1  1  0
#&gt; TCGA.YZ.A985.01     1       0          1  1  0
#&gt; TCGA.V4.A9F0.01     1       0          1  1  0
#&gt; TCGA.V4.A9E7.01     1       0          1  1  0
#&gt; TCGA.VD.A8KN.01     1       0          1  1  0
#&gt; TCGA.VD.A8KK.01     1       0          1  1  0
#&gt; TCGA.V4.A9EM.01     2       0          1  0  1
#&gt; TCGA.VD.AA8Q.01     2       0          1  0  1
#&gt; TCGA.VD.A8K9.01     2       0          1  0  1
#&gt; TCGA.WC.A888.01     1       0          1  1  0
#&gt; TCGA.VD.AA8R.01     2       0          1  0  1
#&gt; TCGA.VD.A8KH.01     2       0          1  0  1
#&gt; TCGA.RZ.AB0B.01     1       0          1  1  0
#&gt; TCGA.V4.A9EJ.01     2       0          1  0  1
#&gt; TCGA.VD.A8K7.01     2       0          1  0  1
#&gt; TCGA.VD.AA8O.01     1       0          1  1  0
#&gt; TCGA.VD.A8KA.01     2       0          1  0  1
#&gt; TCGA.V4.A9EK.01     2       0          1  0  1
#&gt; TCGA.V4.A9F8.01     1       0          1  1  0
#&gt; TCGA.YZ.A984.01     1       0          1  1  0
#&gt; TCGA.VD.A8KD.01     1       0          1  1  0
#&gt; TCGA.YZ.A982.01     2       0          1  0  1
#&gt; TCGA.WC.A88A.01     1       0          1  1  0
#&gt; TCGA.WC.A87W.01     2       0          1  0  1
#&gt; TCGA.V4.A9EH.01     2       0          1  0  1
#&gt; TCGA.WC.A87U.01     2       0          1  0  1
#&gt; TCGA.YZ.A983.01     2       0          1  0  1
#&gt; TCGA.V4.A9EY.01     2       0          1  0  1
#&gt; TCGA.WC.A87T.01     2       0          1  0  1
#&gt; TCGA.VD.AA8N.01     1       0          1  1  0
#&gt; TCGA.VD.A8KM.01     1       0          1  1  0
#&gt; TCGA.VD.AA8P.01     1       0          1  1  0
#&gt; TCGA.V4.A9EF.01     1       0          1  1  0
#&gt; TCGA.V4.A9EE.01     1       0          1  1  0
#&gt; TCGA.WC.A87Y.01     1       0          1  1  0
#&gt; TCGA.VD.A8KE.01     2       0          1  0  1
#&gt; TCGA.VD.A8KF.01     1       0          1  1  0
#&gt; TCGA.VD.A8KO.01     2       0          1  0  1
#&gt; TCGA.WC.A883.01     1       0          1  1  0
#&gt; TCGA.V4.A9EA.01     2       0          1  0  1
#&gt; TCGA.WC.A884.01     2       0          1  0  1
#&gt; TCGA.V4.A9F5.01     1       0          1  1  0
</code></pre>

<script>
$('#tab-node-0-get-classes-1-a').parent().next().next().hide();
$('#tab-node-0-get-classes-1-a').click(function(){
  $('#tab-node-0-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-2'>
<p><a id='tab-node-0-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1  p2   p3
#&gt; TCGA.V4.A9EX.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9E5.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EZ.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A885.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9F3.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9EU.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9ET.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9F7.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9F1.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9F4.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.YZ.A980.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KJ.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V3.A9ZX.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.WC.AA9A.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.AA8T.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.V4.A9EW.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A880.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A881.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V3.A9ZY.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.AA9E.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EV.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9E9.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9E8.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KB.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.A8KL.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KG.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.AA8M.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A882.01     3   0.613      0.333 0.00 0.4 0.60
#&gt; TCGA.V4.A9EO.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KI.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9F2.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EQ.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.A8K8.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9EL.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9EI.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.AA8S.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EC.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9ED.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.V4.A9ES.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.YZ.A985.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.V4.A9F0.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9E7.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.A8KN.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KK.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.V4.A9EM.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.AA8Q.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.A8K9.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A888.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.AA8R.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.A8KH.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.RZ.AB0B.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9EJ.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.A8K7.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.AA8O.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.A8KA.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EK.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9F8.01     3   0.153      0.931 0.04 0.0 0.96
#&gt; TCGA.YZ.A984.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KD.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.YZ.A982.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A88A.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.WC.A87W.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EH.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A87U.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.YZ.A983.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9EY.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A87T.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.AA8N.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.A8KM.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.AA8P.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.V4.A9EF.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9EE.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.WC.A87Y.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.VD.A8KE.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.VD.A8KF.01     3   0.000      0.968 0.00 0.0 1.00
#&gt; TCGA.VD.A8KO.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A883.01     1   0.000      1.000 1.00 0.0 0.00
#&gt; TCGA.V4.A9EA.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.WC.A884.01     2   0.000      1.000 0.00 1.0 0.00
#&gt; TCGA.V4.A9F5.01     1   0.000      1.000 1.00 0.0 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-2-a').parent().next().next().hide();
$('#tab-node-0-get-classes-2-a').click(function(){
  $('#tab-node-0-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-3'>
<p><a id='tab-node-0-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1   p2 p3   p4
#&gt; TCGA.V4.A9EX.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9E5.01     4   0.000      1.000  0 0.00  0 1.00
#&gt; TCGA.V4.A9EZ.01     2   0.265      0.885  0 0.88  0 0.12
#&gt; TCGA.WC.A885.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9F3.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9EU.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9ET.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9F7.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9F1.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9F4.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.YZ.A980.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KJ.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V3.A9ZX.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.WC.AA9A.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.AA8T.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.V4.A9EW.01     2   0.265      0.885  0 0.88  0 0.12
#&gt; TCGA.WC.A880.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.A881.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V3.A9ZY.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.AA9E.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9EV.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9E9.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9E8.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KB.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.VD.A8KL.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KG.01     2   0.265      0.885  0 0.88  0 0.12
#&gt; TCGA.VD.AA8M.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.A882.01     4   0.000      1.000  0 0.00  0 1.00
#&gt; TCGA.V4.A9EO.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KI.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9F2.01     4   0.000      1.000  0 0.00  0 1.00
#&gt; TCGA.V4.A9EQ.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.A8K8.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9EL.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9EI.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.AA8S.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9EC.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9ED.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.V4.A9ES.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.YZ.A985.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.V4.A9F0.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9E7.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.A8KN.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KK.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.V4.A9EM.01     4   0.000      1.000  0 0.00  0 1.00
#&gt; TCGA.VD.AA8Q.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.VD.A8K9.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.A888.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.AA8R.01     2   0.164      0.939  0 0.94  0 0.06
#&gt; TCGA.VD.A8KH.01     2   0.265      0.885  0 0.88  0 0.12
#&gt; TCGA.RZ.AB0B.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9EJ.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.VD.A8K7.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.VD.AA8O.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.A8KA.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9EK.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9F8.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.YZ.A984.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KD.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.YZ.A982.01     2   0.121      0.955  0 0.96  0 0.04
#&gt; TCGA.WC.A88A.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.WC.A87W.01     4   0.000      1.000  0 0.00  0 1.00
#&gt; TCGA.V4.A9EH.01     2   0.164      0.939  0 0.94  0 0.06
#&gt; TCGA.WC.A87U.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.YZ.A983.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9EY.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.A87T.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.VD.AA8N.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.A8KM.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.AA8P.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.V4.A9EF.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9EE.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.WC.A87Y.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.VD.A8KE.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.VD.A8KF.01     3   0.000      1.000  0 0.00  1 0.00
#&gt; TCGA.VD.A8KO.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.A883.01     1   0.000      1.000  1 0.00  0 0.00
#&gt; TCGA.V4.A9EA.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.WC.A884.01     2   0.000      0.981  0 1.00  0 0.00
#&gt; TCGA.V4.A9F5.01     1   0.000      1.000  1 0.00  0 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-3-a').parent().next().next().hide();
$('#tab-node-0-get-classes-3-a').click(function(){
  $('#tab-node-0-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-4'>
<p><a id='tab-node-0-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5
#&gt; TCGA.V4.A9EX.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E5.01     4  0.0000    0.90402 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.V4.A9EZ.01     2  0.6530    0.25885 0.00 0.44 0.00 0.20 0.36
#&gt; TCGA.WC.A885.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     1  0.4307   -0.00506 0.50 0.00 0.00 0.00 0.50
#&gt; TCGA.V4.A9EU.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     2  0.0609    0.87886 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.V4.A9F7.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F1.01     1  0.4302    0.06266 0.52 0.00 0.00 0.00 0.48
#&gt; TCGA.V4.A9F4.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A980.01     3  0.0609    0.89735 0.00 0.00 0.98 0.00 0.02
#&gt; TCGA.VD.A8KJ.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.AA9A.01     3  0.2020    0.85960 0.00 0.00 0.90 0.00 0.10
#&gt; TCGA.VD.AA8T.01     3  0.1732    0.88307 0.00 0.00 0.92 0.00 0.08
#&gt; TCGA.V4.A9EW.01     2  0.6530    0.25885 0.00 0.44 0.00 0.20 0.36
#&gt; TCGA.WC.A880.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     2  0.2280    0.82460 0.00 0.88 0.00 0.00 0.12
#&gt; TCGA.V3.A9ZY.01     2  0.3274    0.74774 0.00 0.78 0.00 0.00 0.22
#&gt; TCGA.WC.AA9E.01     2  0.0609    0.87921 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.V4.A9EV.01     1  0.3796    0.50263 0.70 0.00 0.00 0.00 0.30
#&gt; TCGA.V4.A9E9.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E8.01     3  0.0609    0.89735 0.00 0.00 0.98 0.00 0.02
#&gt; TCGA.VD.A8KB.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KL.01     3  0.0609    0.90180 0.00 0.00 0.98 0.00 0.02
#&gt; TCGA.VD.A8KG.01     5  0.6632   -0.39028 0.00 0.38 0.00 0.22 0.40
#&gt; TCGA.VD.AA8M.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A882.01     4  0.2280    0.92917 0.00 0.00 0.00 0.88 0.12
#&gt; TCGA.V4.A9EO.01     3  0.0000    0.90079 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KI.01     1  0.0609    0.82310 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9F2.01     4  0.2516    0.92711 0.00 0.00 0.00 0.86 0.14
#&gt; TCGA.V4.A9EQ.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     1  0.4302    0.06266 0.52 0.00 0.00 0.00 0.48
#&gt; TCGA.V4.A9EL.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EI.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ED.01     3  0.0000    0.90079 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9ES.01     3  0.0609    0.89922 0.00 0.00 0.98 0.00 0.02
#&gt; TCGA.YZ.A985.01     3  0.0000    0.90079 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9F0.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E7.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KN.01     3  0.1043    0.89769 0.00 0.00 0.96 0.00 0.04
#&gt; TCGA.VD.A8KK.01     3  0.1043    0.89769 0.00 0.00 0.96 0.00 0.04
#&gt; TCGA.V4.A9EM.01     4  0.1410    0.87906 0.00 0.00 0.00 0.94 0.06
#&gt; TCGA.VD.AA8Q.01     2  0.1043    0.86968 0.00 0.96 0.00 0.00 0.04
#&gt; TCGA.VD.A8K9.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A888.01     5  0.5425   -0.31908 0.06 0.00 0.42 0.00 0.52
#&gt; TCGA.VD.AA8R.01     2  0.5579    0.54115 0.00 0.60 0.00 0.10 0.30
#&gt; TCGA.VD.A8KH.01     2  0.6498    0.29349 0.00 0.46 0.00 0.20 0.34
#&gt; TCGA.RZ.AB0B.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8O.01     1  0.2516    0.72400 0.86 0.00 0.00 0.00 0.14
#&gt; TCGA.VD.A8KA.01     2  0.2732    0.79758 0.00 0.84 0.00 0.00 0.16
#&gt; TCGA.V4.A9EK.01     2  0.3796    0.68077 0.00 0.70 0.00 0.00 0.30
#&gt; TCGA.V4.A9F8.01     3  0.5425    0.29734 0.06 0.00 0.52 0.00 0.42
#&gt; TCGA.YZ.A984.01     3  0.0000    0.90079 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KD.01     5  0.4307   -0.28045 0.50 0.00 0.00 0.00 0.50
#&gt; TCGA.YZ.A982.01     2  0.3983    0.63914 0.00 0.66 0.00 0.00 0.34
#&gt; TCGA.WC.A88A.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87W.01     4  0.2732    0.91632 0.00 0.00 0.00 0.84 0.16
#&gt; TCGA.V4.A9EH.01     2  0.5659    0.51691 0.00 0.58 0.00 0.10 0.32
#&gt; TCGA.WC.A87U.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A983.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87T.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8N.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KM.01     5  0.5173   -0.18442 0.46 0.00 0.04 0.00 0.50
#&gt; TCGA.VD.AA8P.01     3  0.2020    0.87135 0.00 0.00 0.90 0.00 0.10
#&gt; TCGA.V4.A9EF.01     1  0.2929    0.67662 0.82 0.00 0.00 0.00 0.18
#&gt; TCGA.V4.A9EE.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87Y.01     1  0.4307   -0.00506 0.50 0.00 0.00 0.00 0.50
#&gt; TCGA.VD.A8KE.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KF.01     3  0.4227    0.44671 0.00 0.00 0.58 0.00 0.42
#&gt; TCGA.VD.A8KO.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2  0.0000    0.88843 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F5.01     1  0.0000    0.83564 1.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-4-a').parent().next().next().hide();
$('#tab-node-0-get-classes-4-a').click(function(){
  $('#tab-node-0-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-5'>
<p><a id='tab-node-0-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.V4.A9EX.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E5.01     4  0.3819      0.809 0.00 0.00 0.00 0.70 0.02 0.28
#&gt; TCGA.V4.A9EZ.01     6  0.2454      0.684 0.00 0.16 0.00 0.00 0.00 0.84
#&gt; TCGA.WC.A885.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     5  0.3409      0.870 0.30 0.00 0.00 0.00 0.70 0.00
#&gt; TCGA.V4.A9EU.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     2  0.0547      0.909 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9F7.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F1.01     5  0.3647      0.805 0.36 0.00 0.00 0.00 0.64 0.00
#&gt; TCGA.V4.A9F4.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A980.01     3  0.2474      0.842 0.00 0.00 0.88 0.00 0.08 0.04
#&gt; TCGA.VD.A8KJ.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.AA9A.01     3  0.3258      0.825 0.00 0.00 0.84 0.02 0.10 0.04
#&gt; TCGA.VD.AA8T.01     3  0.1480      0.875 0.00 0.00 0.94 0.02 0.04 0.00
#&gt; TCGA.V4.A9EW.01     6  0.3156      0.698 0.00 0.18 0.00 0.02 0.00 0.80
#&gt; TCGA.WC.A880.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     2  0.2454      0.722 0.00 0.84 0.00 0.00 0.00 0.16
#&gt; TCGA.V3.A9ZY.01     2  0.3851     -0.231 0.00 0.54 0.00 0.00 0.00 0.46
#&gt; TCGA.WC.AA9E.01     2  0.0937      0.891 0.00 0.96 0.00 0.00 0.00 0.04
#&gt; TCGA.V4.A9EV.01     1  0.3756     -0.129 0.60 0.00 0.00 0.00 0.40 0.00
#&gt; TCGA.V4.A9E9.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E8.01     3  0.4088      0.774 0.00 0.00 0.78 0.02 0.10 0.10
#&gt; TCGA.VD.A8KB.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KL.01     3  0.0547      0.879 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.VD.A8KG.01     6  0.4879      0.474 0.00 0.12 0.00 0.12 0.04 0.72
#&gt; TCGA.VD.AA8M.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A882.01     4  0.3647      0.822 0.00 0.00 0.00 0.64 0.00 0.36
#&gt; TCGA.V4.A9EO.01     3  0.0547      0.879 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.VD.A8KI.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F2.01     4  0.3706      0.817 0.00 0.00 0.00 0.62 0.00 0.38
#&gt; TCGA.V4.A9EQ.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     5  0.3578      0.835 0.34 0.00 0.00 0.00 0.66 0.00
#&gt; TCGA.V4.A9EL.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EI.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ED.01     3  0.0547      0.883 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.V4.A9ES.01     3  0.1092      0.879 0.00 0.00 0.96 0.02 0.02 0.00
#&gt; TCGA.YZ.A985.01     3  0.0547      0.879 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.V4.A9F0.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E7.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KN.01     3  0.0547      0.883 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.VD.A8KK.01     3  0.0547      0.883 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.V4.A9EM.01     4  0.3660      0.586 0.00 0.00 0.00 0.78 0.16 0.06
#&gt; TCGA.VD.AA8Q.01     2  0.0547      0.908 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.VD.A8K9.01     2  0.0547      0.909 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.WC.A888.01     5  0.3711      0.371 0.02 0.00 0.26 0.00 0.72 0.00
#&gt; TCGA.VD.AA8R.01     6  0.3647      0.671 0.00 0.36 0.00 0.00 0.00 0.64
#&gt; TCGA.VD.A8KH.01     6  0.2793      0.715 0.00 0.20 0.00 0.00 0.00 0.80
#&gt; TCGA.RZ.AB0B.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8O.01     1  0.2631      0.674 0.82 0.00 0.00 0.00 0.18 0.00
#&gt; TCGA.VD.A8KA.01     2  0.3309      0.465 0.00 0.72 0.00 0.00 0.00 0.28
#&gt; TCGA.V4.A9EK.01     2  0.6274     -0.319 0.00 0.48 0.00 0.08 0.08 0.36
#&gt; TCGA.V4.A9F8.01     3  0.4246      0.414 0.00 0.00 0.58 0.02 0.40 0.00
#&gt; TCGA.YZ.A984.01     3  0.1092      0.874 0.00 0.00 0.96 0.00 0.02 0.02
#&gt; TCGA.VD.A8KD.01     5  0.3409      0.870 0.30 0.00 0.00 0.00 0.70 0.00
#&gt; TCGA.YZ.A982.01     6  0.6326      0.537 0.00 0.30 0.00 0.10 0.08 0.52
#&gt; TCGA.WC.A88A.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87W.01     4  0.3756      0.799 0.00 0.00 0.00 0.60 0.00 0.40
#&gt; TCGA.V4.A9EH.01     6  0.3578      0.688 0.00 0.34 0.00 0.00 0.00 0.66
#&gt; TCGA.WC.A87U.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A983.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87T.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8N.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KM.01     5  0.3309      0.869 0.28 0.00 0.00 0.00 0.72 0.00
#&gt; TCGA.VD.AA8P.01     3  0.1480      0.875 0.00 0.00 0.94 0.02 0.04 0.00
#&gt; TCGA.V4.A9EF.01     1  0.2454      0.711 0.84 0.00 0.00 0.00 0.16 0.00
#&gt; TCGA.V4.A9EE.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87Y.01     5  0.3309      0.869 0.28 0.00 0.00 0.00 0.72 0.00
#&gt; TCGA.VD.A8KE.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KF.01     3  0.4328      0.251 0.00 0.00 0.52 0.02 0.46 0.00
#&gt; TCGA.VD.A8KO.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2  0.0000      0.926 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F5.01     1  0.0000      0.937 1.00 0.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-5-a').parent().next().next().hide();
$('#tab-node-0-get-classes-5-a').click(function(){
  $('#tab-node-0-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-6'>
<p><a id='tab-node-0-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.V4.A9EX.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E5.01     4  0.4763      0.621 0.00 0.00 0.00 0.62 0.00 0.18 0.20
#&gt; TCGA.V4.A9EZ.01     6  0.1363      0.450 0.00 0.04 0.00 0.00 0.00 0.94 0.02
#&gt; TCGA.WC.A885.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     5  0.1671      0.795 0.10 0.00 0.00 0.00 0.90 0.00 0.00
#&gt; TCGA.V4.A9EU.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     2  0.0504      0.957 0.00 0.98 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9F7.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F1.01     5  0.2708      0.690 0.22 0.00 0.00 0.00 0.78 0.00 0.00
#&gt; TCGA.V4.A9F4.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A980.01     3  0.4763      0.597 0.00 0.00 0.62 0.00 0.20 0.00 0.18
#&gt; TCGA.VD.A8KJ.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.AA9A.01     3  0.5115      0.250 0.00 0.00 0.48 0.00 0.38 0.00 0.14
#&gt; TCGA.VD.AA8T.01     3  0.2572      0.727 0.00 0.00 0.80 0.00 0.20 0.00 0.00
#&gt; TCGA.V4.A9EW.01     6  0.1166      0.487 0.00 0.06 0.00 0.00 0.00 0.94 0.00
#&gt; TCGA.WC.A880.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     2  0.2313      0.840 0.00 0.88 0.00 0.00 0.00 0.06 0.06
#&gt; TCGA.V3.A9ZY.01     6  0.3496      0.427 0.00 0.42 0.00 0.00 0.00 0.58 0.00
#&gt; TCGA.WC.AA9E.01     2  0.1166      0.917 0.00 0.94 0.00 0.00 0.00 0.00 0.06
#&gt; TCGA.V4.A9EV.01     1  0.3294      0.490 0.66 0.00 0.00 0.00 0.34 0.00 0.00
#&gt; TCGA.V4.A9E9.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E8.01     3  0.4175      0.542 0.00 0.00 0.58 0.00 0.04 0.00 0.38
#&gt; TCGA.VD.A8KB.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KL.01     3  0.0504      0.839 0.00 0.00 0.98 0.00 0.02 0.00 0.00
#&gt; TCGA.VD.A8KG.01     6  0.4536      0.320 0.00 0.06 0.00 0.08 0.00 0.72 0.14
#&gt; TCGA.VD.AA8M.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A882.01     4  0.3496      0.673 0.00 0.00 0.00 0.58 0.00 0.42 0.00
#&gt; TCGA.V4.A9EO.01     3  0.0504      0.838 0.00 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.VD.A8KI.01     1  0.1166      0.911 0.94 0.00 0.00 0.00 0.06 0.00 0.00
#&gt; TCGA.V4.A9F2.01     4  0.3985      0.654 0.00 0.00 0.00 0.52 0.00 0.46 0.02
#&gt; TCGA.V4.A9EQ.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     5  0.2081      0.770 0.14 0.00 0.00 0.00 0.86 0.00 0.00
#&gt; TCGA.V4.A9EL.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EI.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ED.01     3  0.1006      0.839 0.00 0.00 0.96 0.00 0.02 0.00 0.02
#&gt; TCGA.V4.A9ES.01     3  0.1928      0.836 0.00 0.00 0.90 0.00 0.08 0.00 0.02
#&gt; TCGA.YZ.A985.01     3  0.0504      0.838 0.00 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9F0.01     1  0.0504      0.934 0.98 0.00 0.00 0.00 0.02 0.00 0.00
#&gt; TCGA.V4.A9E7.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KN.01     3  0.1433      0.825 0.00 0.00 0.92 0.00 0.08 0.00 0.00
#&gt; TCGA.VD.A8KK.01     3  0.1166      0.832 0.00 0.00 0.94 0.00 0.06 0.00 0.00
#&gt; TCGA.V4.A9EM.01     4  0.3011      0.476 0.00 0.00 0.00 0.82 0.06 0.00 0.12
#&gt; TCGA.VD.AA8Q.01     2  0.0504      0.957 0.00 0.98 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.VD.A8K9.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A888.01     5  0.1166      0.711 0.00 0.00 0.06 0.00 0.94 0.00 0.00
#&gt; TCGA.VD.AA8R.01     6  0.2708      0.561 0.00 0.22 0.00 0.00 0.00 0.78 0.00
#&gt; TCGA.VD.A8KH.01     6  0.1433      0.505 0.00 0.08 0.00 0.00 0.00 0.92 0.00
#&gt; TCGA.RZ.AB0B.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     2  0.0504      0.957 0.00 0.98 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.VD.AA8O.01     1  0.2572      0.747 0.80 0.00 0.00 0.00 0.20 0.00 0.00
#&gt; TCGA.VD.A8KA.01     2  0.3637      0.514 0.00 0.72 0.00 0.00 0.00 0.24 0.04
#&gt; TCGA.V4.A9EK.01     6  0.6022      0.354 0.00 0.30 0.00 0.02 0.00 0.36 0.32
#&gt; TCGA.V4.A9F8.01     5  0.3909      0.216 0.02 0.00 0.40 0.00 0.58 0.00 0.00
#&gt; TCGA.YZ.A984.01     3  0.1166      0.827 0.00 0.00 0.94 0.00 0.00 0.00 0.06
#&gt; TCGA.VD.A8KD.01     5  0.1671      0.795 0.10 0.00 0.00 0.00 0.90 0.00 0.00
#&gt; TCGA.YZ.A982.01     6  0.6046      0.334 0.00 0.20 0.00 0.04 0.00 0.44 0.32
#&gt; TCGA.WC.A88A.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87W.01     4  0.3994      0.641 0.00 0.00 0.00 0.50 0.00 0.48 0.02
#&gt; TCGA.V4.A9EH.01     6  0.2708      0.564 0.00 0.22 0.00 0.00 0.00 0.78 0.00
#&gt; TCGA.WC.A87U.01     2  0.0504      0.957 0.00 0.98 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.YZ.A983.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87T.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8N.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KM.01     5  0.1671      0.795 0.10 0.00 0.00 0.00 0.90 0.00 0.00
#&gt; TCGA.VD.AA8P.01     3  0.1671      0.822 0.00 0.00 0.90 0.00 0.10 0.00 0.00
#&gt; TCGA.V4.A9EF.01     1  0.2422      0.788 0.82 0.00 0.00 0.00 0.18 0.00 0.00
#&gt; TCGA.V4.A9EE.01     1  0.1166      0.909 0.94 0.00 0.00 0.00 0.06 0.00 0.00
#&gt; TCGA.WC.A87Y.01     5  0.1671      0.795 0.10 0.00 0.00 0.00 0.90 0.00 0.00
#&gt; TCGA.VD.A8KE.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KF.01     5  0.3562     -0.132 0.00 0.00 0.50 0.00 0.50 0.00 0.00
#&gt; TCGA.VD.A8KO.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1  0.0000      0.943 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2  0.0000      0.973 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F5.01     1  0.0504      0.934 0.98 0.00 0.00 0.00 0.02 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-6-a').parent().next().next().hide();
$('#tab-node-0-get-classes-6-a').click(function(){
  $('#tab-node-0-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-7'>
<p><a id='tab-node-0-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7   p8
#&gt; TCGA.V4.A9EX.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E5.01     4  0.3131     0.1497 0.00 0.00 0.00 0.84 0.04 0.06 0.04 0.02
#&gt; TCGA.V4.A9EZ.01     6  0.0941     0.5473 0.00 0.02 0.00 0.02 0.00 0.96 0.00 0.00
#&gt; TCGA.WC.A885.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     5  0.1804     0.8140 0.08 0.00 0.00 0.00 0.90 0.00 0.00 0.02
#&gt; TCGA.V4.A9EU.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     2  0.0808     0.9411 0.00 0.96 0.00 0.00 0.00 0.00 0.00 0.04
#&gt; TCGA.V4.A9F7.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F1.01     5  0.2534     0.7152 0.22 0.00 0.00 0.00 0.78 0.00 0.00 0.00
#&gt; TCGA.V4.A9F4.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A980.01     3  0.5591     0.4750 0.00 0.00 0.56 0.04 0.26 0.00 0.04 0.10
#&gt; TCGA.VD.A8KJ.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.AA9A.01     3  0.5999     0.4200 0.00 0.00 0.50 0.02 0.30 0.02 0.04 0.12
#&gt; TCGA.VD.AA8T.01     3  0.2807     0.7627 0.00 0.00 0.84 0.00 0.10 0.00 0.04 0.02
#&gt; TCGA.V4.A9EW.01     6  0.0808     0.5789 0.00 0.04 0.00 0.00 0.00 0.96 0.00 0.00
#&gt; TCGA.WC.A880.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     2  0.2862     0.7749 0.00 0.82 0.00 0.00 0.00 0.10 0.00 0.08
#&gt; TCGA.V3.A9ZY.01     6  0.3729     0.1740 0.00 0.46 0.00 0.00 0.00 0.52 0.00 0.02
#&gt; TCGA.WC.AA9E.01     2  0.2025     0.8562 0.00 0.88 0.00 0.00 0.00 0.02 0.00 0.10
#&gt; TCGA.V4.A9EV.01     1  0.3299     0.1999 0.56 0.00 0.00 0.00 0.44 0.00 0.00 0.00
#&gt; TCGA.V4.A9E9.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E8.01     8  0.6775    -0.2605 0.00 0.00 0.34 0.06 0.10 0.00 0.14 0.36
#&gt; TCGA.VD.A8KB.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KL.01     3  0.1275     0.8035 0.00 0.00 0.94 0.00 0.00 0.00 0.04 0.02
#&gt; TCGA.VD.A8KG.01     6  0.3601     0.3268 0.00 0.02 0.00 0.06 0.00 0.76 0.00 0.16
#&gt; TCGA.VD.AA8M.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A882.01     4  0.4642     0.6691 0.00 0.00 0.00 0.60 0.00 0.30 0.06 0.04
#&gt; TCGA.V4.A9EO.01     3  0.2204     0.7746 0.00 0.00 0.90 0.02 0.02 0.00 0.04 0.02
#&gt; TCGA.VD.A8KI.01     1  0.1765     0.8162 0.88 0.00 0.00 0.00 0.12 0.00 0.00 0.00
#&gt; TCGA.V4.A9F2.01     4  0.3907     0.7166 0.00 0.00 0.00 0.58 0.00 0.38 0.00 0.04
#&gt; TCGA.V4.A9EQ.01     1  0.0471     0.8989 0.98 0.00 0.00 0.00 0.02 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     5  0.2114     0.7879 0.16 0.00 0.00 0.00 0.84 0.00 0.00 0.00
#&gt; TCGA.V4.A9EL.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EI.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ED.01     3  0.0471     0.8055 0.00 0.00 0.98 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9ES.01     3  0.2204     0.8011 0.00 0.00 0.90 0.02 0.04 0.00 0.02 0.02
#&gt; TCGA.YZ.A985.01     3  0.1275     0.8008 0.00 0.00 0.94 0.00 0.04 0.00 0.00 0.02
#&gt; TCGA.V4.A9F0.01     1  0.1275     0.8774 0.94 0.00 0.00 0.00 0.04 0.00 0.02 0.00
#&gt; TCGA.V4.A9E7.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KN.01     3  0.1741     0.8053 0.00 0.00 0.92 0.00 0.04 0.00 0.02 0.02
#&gt; TCGA.VD.A8KK.01     3  0.2071     0.8000 0.00 0.00 0.90 0.00 0.04 0.00 0.02 0.04
#&gt; TCGA.V4.A9EM.01     7  0.2267     0.0000 0.00 0.00 0.00 0.18 0.00 0.00 0.82 0.00
#&gt; TCGA.VD.AA8Q.01     2  0.0941     0.9391 0.00 0.96 0.00 0.00 0.00 0.02 0.00 0.02
#&gt; TCGA.VD.A8K9.01     2  0.0471     0.9573 0.00 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.WC.A888.01     5  0.2020     0.7416 0.02 0.00 0.06 0.00 0.90 0.00 0.00 0.02
#&gt; TCGA.VD.AA8R.01     6  0.2719     0.5777 0.00 0.18 0.00 0.00 0.00 0.80 0.00 0.02
#&gt; TCGA.VD.A8KH.01     6  0.1874     0.5262 0.00 0.02 0.00 0.02 0.00 0.92 0.02 0.02
#&gt; TCGA.RZ.AB0B.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8O.01     1  0.4375     0.5269 0.66 0.00 0.02 0.00 0.26 0.00 0.04 0.02
#&gt; TCGA.VD.A8KA.01     2  0.2818     0.7709 0.00 0.82 0.00 0.00 0.00 0.12 0.00 0.06
#&gt; TCGA.V4.A9EK.01     8  0.5450     0.3178 0.00 0.24 0.00 0.04 0.00 0.20 0.00 0.52
#&gt; TCGA.V4.A9F8.01     5  0.4358     0.0982 0.00 0.00 0.40 0.00 0.54 0.00 0.04 0.02
#&gt; TCGA.YZ.A984.01     3  0.2532     0.7631 0.00 0.00 0.88 0.02 0.04 0.00 0.04 0.02
#&gt; TCGA.VD.A8KD.01     5  0.1765     0.8179 0.12 0.00 0.00 0.00 0.88 0.00 0.00 0.00
#&gt; TCGA.YZ.A982.01     8  0.5469     0.2984 0.00 0.16 0.00 0.06 0.00 0.24 0.00 0.54
#&gt; TCGA.WC.A88A.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87W.01     4  0.3971     0.6896 0.00 0.00 0.00 0.54 0.00 0.42 0.00 0.04
#&gt; TCGA.V4.A9EH.01     6  0.2719     0.5819 0.00 0.18 0.00 0.00 0.00 0.80 0.00 0.02
#&gt; TCGA.WC.A87U.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A983.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87T.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8N.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KM.01     5  0.1804     0.8140 0.08 0.00 0.00 0.00 0.90 0.00 0.00 0.02
#&gt; TCGA.VD.AA8P.01     3  0.1741     0.8060 0.00 0.00 0.92 0.00 0.04 0.00 0.02 0.02
#&gt; TCGA.V4.A9EF.01     1  0.5024     0.5151 0.64 0.00 0.10 0.00 0.20 0.00 0.04 0.02
#&gt; TCGA.V4.A9EE.01     1  0.1563     0.8469 0.90 0.00 0.00 0.00 0.10 0.00 0.00 0.00
#&gt; TCGA.WC.A87Y.01     5  0.1563     0.8224 0.10 0.00 0.00 0.00 0.90 0.00 0.00 0.00
#&gt; TCGA.VD.A8KE.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KF.01     3  0.3943     0.3041 0.00 0.00 0.56 0.00 0.40 0.00 0.00 0.04
#&gt; TCGA.VD.A8KO.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1  0.0000     0.9061 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2  0.0000     0.9734 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F5.01     1  0.0471     0.8989 0.98 0.00 0.00 0.00 0.02 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-7-a').parent().next().next().hide();
$('#tab-node-0-get-classes-7-a').click(function(){
  $('#tab-node-0-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-0-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-0-consensus-heatmap'>
<ul>
<li><a href='#tab-node-0-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-0-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-0-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-0-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-0-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-0-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-0-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-0-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-0-membership-heatmap'>
<ul>
<li><a href='#tab-node-0-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-0-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-0-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-0-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-0-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-0-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-0-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-1-1.png" alt="plot of chunk tab-node-0-membership-heatmap-1"/></p>

</div>
<div id='tab-node-0-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-2-1.png" alt="plot of chunk tab-node-0-membership-heatmap-2"/></p>

</div>
<div id='tab-node-0-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-3-1.png" alt="plot of chunk tab-node-0-membership-heatmap-3"/></p>

</div>
<div id='tab-node-0-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-4-1.png" alt="plot of chunk tab-node-0-membership-heatmap-4"/></p>

</div>
<div id='tab-node-0-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-5-1.png" alt="plot of chunk tab-node-0-membership-heatmap-5"/></p>

</div>
<div id='tab-node-0-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-6-1.png" alt="plot of chunk tab-node-0-membership-heatmap-6"/></p>

</div>
<div id='tab-node-0-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-7-1.png" alt="plot of chunk tab-node-0-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-0-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-0-get-signatures'>
<ul>
<li><a href='#tab-node-0-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-0-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-0-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-0-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-0-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-0-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-0-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-1-1.png" alt="plot of chunk tab-node-0-get-signatures-1"/></p>

</div>
<div id='tab-node-0-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-2-1.png" alt="plot of chunk tab-node-0-get-signatures-2"/></p>

</div>
<div id='tab-node-0-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-3-1.png" alt="plot of chunk tab-node-0-get-signatures-3"/></p>

</div>
<div id='tab-node-0-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-4-1.png" alt="plot of chunk tab-node-0-get-signatures-4"/></p>

</div>
<div id='tab-node-0-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-5-1.png" alt="plot of chunk tab-node-0-get-signatures-5"/></p>

</div>
<div id='tab-node-0-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-6-1.png" alt="plot of chunk tab-node-0-get-signatures-6"/></p>

</div>
<div id='tab-node-0-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-7-1.png" alt="plot of chunk tab-node-0-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-0-signature_compare](figure_cola/node-0-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-0-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-0-dimension-reduction'>
<ul>
<li><a href='#tab-node-0-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-0-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-0-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-0-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-0-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-0-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-0-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-1-1.png" alt="plot of chunk tab-node-0-dimension-reduction-1"/></p>

</div>
<div id='tab-node-0-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-2-1.png" alt="plot of chunk tab-node-0-dimension-reduction-2"/></p>

</div>
<div id='tab-node-0-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-3-1.png" alt="plot of chunk tab-node-0-dimension-reduction-3"/></p>

</div>
<div id='tab-node-0-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-4-1.png" alt="plot of chunk tab-node-0-dimension-reduction-4"/></p>

</div>
<div id='tab-node-0-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-5-1.png" alt="plot of chunk tab-node-0-dimension-reduction-5"/></p>

</div>
<div id='tab-node-0-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-6-1.png" alt="plot of chunk tab-node-0-dimension-reduction-6"/></p>

</div>
<div id='tab-node-0-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-7-1.png" alt="plot of chunk tab-node-0-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-0-collect-classes](figure_cola/node-0-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### Node01


Parent node: [Node0](#Node0).
Child nodes: 
                Node011-leaf
        ,
                Node012-leaf
        ,
                Node013-leaf
        ,
                [Node021](#Node021)
        ,
                Node022-leaf
        ,
                Node023-leaf
        ,
                Node031-leaf
        ,
                Node032-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["01"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 24 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-01-collect-plots](figure_cola/node-01-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-01-select-partition-number](figure_cola/node-01-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.3449 0.656   0.656
#> 3 3 1.000           0.977       0.988         0.8588 0.696   0.536
#> 4 4 0.848           0.825       0.937         0.0330 0.978   0.938
#> 5 5 0.762           0.743       0.906         0.0277 0.982   0.945
#> 6 6 0.766           0.707       0.887         0.0419 1.000   1.000
#> 7 7 0.775           0.649       0.875         0.0372 0.946   0.826
#> 8 8 0.772           0.532       0.858         0.0393 0.986   0.944
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-01-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-01-get-classes'>
<ul>
<li><a href='#tab-node-01-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-01-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-01-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-01-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-01-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-01-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-01-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-01-get-classes-1'>
<p><a id='tab-node-01-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1 p2
#&gt; TCGA.V4.A9EX.01     1       0          1  1  0
#&gt; TCGA.V4.A9F3.01     2       0          1  0  1
#&gt; TCGA.V4.A9EU.01     1       0          1  1  0
#&gt; TCGA.V4.A9F1.01     2       0          1  0  1
#&gt; TCGA.V3.A9ZX.01     2       0          1  0  1
#&gt; TCGA.V4.A9EV.01     2       0          1  0  1
#&gt; TCGA.VD.A8KI.01     2       0          1  0  1
#&gt; TCGA.V4.A9EQ.01     2       0          1  0  1
#&gt; TCGA.VD.A8K8.01     2       0          1  0  1
#&gt; TCGA.V4.A9EL.01     2       0          1  0  1
#&gt; TCGA.V4.A9EI.01     1       0          1  1  0
#&gt; TCGA.V4.A9F0.01     2       0          1  0  1
#&gt; TCGA.V4.A9E7.01     2       0          1  0  1
#&gt; TCGA.RZ.AB0B.01     2       0          1  0  1
#&gt; TCGA.VD.AA8O.01     2       0          1  0  1
#&gt; TCGA.VD.A8KD.01     2       0          1  0  1
#&gt; TCGA.WC.A88A.01     1       0          1  1  0
#&gt; TCGA.VD.AA8N.01     2       0          1  0  1
#&gt; TCGA.VD.A8KM.01     2       0          1  0  1
#&gt; TCGA.V4.A9EF.01     2       0          1  0  1
#&gt; TCGA.V4.A9EE.01     2       0          1  0  1
#&gt; TCGA.WC.A87Y.01     2       0          1  0  1
#&gt; TCGA.WC.A883.01     1       0          1  1  0
#&gt; TCGA.V4.A9F5.01     2       0          1  0  1
</code></pre>

<script>
$('#tab-node-01-get-classes-1-a').parent().next().next().hide();
$('#tab-node-01-get-classes-1-a').click(function(){
  $('#tab-node-01-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-01-get-classes-2'>
<p><a id='tab-node-01-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1   p2   p3
#&gt; TCGA.V4.A9EX.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.V4.A9F3.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.V4.A9EU.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.V4.A9F1.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.V3.A9ZX.01     3   0.000      0.939  0 0.00 1.00
#&gt; TCGA.V4.A9EV.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.VD.A8KI.01     3   0.000      0.939  0 0.00 1.00
#&gt; TCGA.V4.A9EQ.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.VD.A8K8.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.V4.A9EL.01     3   0.000      0.939  0 0.00 1.00
#&gt; TCGA.V4.A9EI.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.V4.A9F0.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.V4.A9E7.01     3   0.153      0.942  0 0.04 0.96
#&gt; TCGA.RZ.AB0B.01     3   0.400      0.825  0 0.16 0.84
#&gt; TCGA.VD.AA8O.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.VD.A8KD.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.WC.A88A.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.VD.AA8N.01     3   0.153      0.941  0 0.04 0.96
#&gt; TCGA.VD.A8KM.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.V4.A9EF.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.V4.A9EE.01     3   0.207      0.931  0 0.06 0.94
#&gt; TCGA.WC.A87Y.01     2   0.000      1.000  0 1.00 0.00
#&gt; TCGA.WC.A883.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.V4.A9F5.01     2   0.000      1.000  0 1.00 0.00
</code></pre>

<script>
$('#tab-node-01-get-classes-2-a').parent().next().next().hide();
$('#tab-node-01-get-classes-2-a').click(function(){
  $('#tab-node-01-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-01-get-classes-3'>
<p><a id='tab-node-01-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4
#&gt; TCGA.V4.A9EX.01     1  0.0000      0.991 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EU.01     1  0.0000      0.991 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F1.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     3  0.4977      0.508 0.00 0.00 0.54 0.46
#&gt; TCGA.V4.A9EV.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KI.01     3  0.5062      0.613 0.00 0.02 0.68 0.30
#&gt; TCGA.V4.A9EQ.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EL.01     4  0.1211      0.000 0.00 0.00 0.04 0.96
#&gt; TCGA.V4.A9EI.01     1  0.0000      0.991 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F0.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9E7.01     3  0.0707      0.302 0.00 0.00 0.98 0.02
#&gt; TCGA.RZ.AB0B.01     3  0.7674      0.380 0.00 0.26 0.46 0.28
#&gt; TCGA.VD.AA8O.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KD.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.A88A.01     1  0.0000      0.991 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8N.01     3  0.5915      0.605 0.00 0.04 0.56 0.40
#&gt; TCGA.VD.A8KM.01     2  0.1637      0.928 0.00 0.94 0.06 0.00
#&gt; TCGA.V4.A9EF.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EE.01     3  0.6649      0.601 0.00 0.10 0.56 0.34
#&gt; TCGA.WC.A87Y.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1  0.1211      0.965 0.96 0.00 0.00 0.04
#&gt; TCGA.V4.A9F5.01     2  0.0000      0.994 0.00 1.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-01-get-classes-3-a').parent().next().next().hide();
$('#tab-node-01-get-classes-3-a').click(function(){
  $('#tab-node-01-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-01-get-classes-4'>
<p><a id='tab-node-01-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5
#&gt; TCGA.V4.A9EX.01     1   0.000      0.934 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EU.01     1   0.244      0.880 0.90 0.00 0.00 0.04 0.06
#&gt; TCGA.V4.A9F1.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     3   0.293      0.451 0.00 0.02 0.88 0.08 0.02
#&gt; TCGA.V4.A9EV.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KI.01     3   0.487      0.175 0.00 0.00 0.72 0.12 0.16
#&gt; TCGA.V4.A9EQ.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EL.01     4   0.327      0.000 0.00 0.00 0.22 0.78 0.00
#&gt; TCGA.V4.A9EI.01     1   0.000      0.934 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F0.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9E7.01     5   0.413      0.000 0.00 0.00 0.38 0.00 0.62
#&gt; TCGA.RZ.AB0B.01     3   0.553      0.270 0.00 0.36 0.58 0.04 0.02
#&gt; TCGA.VD.AA8O.01     2   0.233      0.888 0.00 0.90 0.00 0.08 0.02
#&gt; TCGA.VD.A8KD.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A88A.01     1   0.000      0.934 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8N.01     3   0.311      0.487 0.00 0.08 0.86 0.00 0.06
#&gt; TCGA.VD.A8KM.01     2   0.287      0.815 0.00 0.86 0.12 0.02 0.00
#&gt; TCGA.V4.A9EF.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EE.01     3   0.412      0.499 0.00 0.08 0.82 0.06 0.04
#&gt; TCGA.WC.A87Y.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1   0.293      0.813 0.82 0.00 0.00 0.00 0.18
#&gt; TCGA.V4.A9F5.01     2   0.000      0.976 0.00 1.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-01-get-classes-4-a').parent().next().next().hide();
$('#tab-node-01-get-classes-4-a').click(function(){
  $('#tab-node-01-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-01-get-classes-5'>
<p><a id='tab-node-01-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.V4.A9EX.01     1  0.0000      0.882 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     2  0.0000      0.941 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EU.01     1  0.2454      0.798 0.84 0.00 0.16 0.00 0.00 0.00
#&gt; TCGA.V4.A9F1.01     2  0.0000      0.941 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     6  0.4887      0.444 0.00 0.02 0.08 0.22 0.00 0.68
#&gt; TCGA.V4.A9EV.01     2  0.0547      0.937 0.00 0.98 0.02 0.00 0.00 0.00
#&gt; TCGA.VD.A8KI.01     6  0.4989      0.338 0.00 0.00 0.22 0.00 0.14 0.64
#&gt; TCGA.V4.A9EQ.01     2  0.0547      0.937 0.00 0.98 0.02 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     2  0.0000      0.941 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EL.01     4  0.0547      0.000 0.00 0.00 0.00 0.98 0.00 0.02
#&gt; TCGA.V4.A9EI.01     1  0.0000      0.882 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F0.01     2  0.1556      0.899 0.00 0.92 0.08 0.00 0.00 0.00
#&gt; TCGA.V4.A9E7.01     5  0.2048      0.000 0.00 0.00 0.00 0.00 0.88 0.12
#&gt; TCGA.RZ.AB0B.01     6  0.4002      0.372 0.00 0.32 0.00 0.02 0.00 0.66
#&gt; TCGA.VD.AA8O.01     2  0.4002      0.581 0.00 0.66 0.32 0.00 0.00 0.02
#&gt; TCGA.VD.A8KD.01     2  0.0000      0.941 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A88A.01     1  0.0547      0.879 0.98 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.VD.AA8N.01     6  0.5177      0.453 0.00 0.02 0.06 0.06 0.14 0.72
#&gt; TCGA.VD.A8KM.01     2  0.2260      0.795 0.00 0.86 0.00 0.00 0.00 0.14
#&gt; TCGA.V4.A9EF.01     2  0.0547      0.937 0.00 0.98 0.02 0.00 0.00 0.00
#&gt; TCGA.V4.A9EE.01     6  0.3007      0.547 0.00 0.08 0.04 0.02 0.00 0.86
#&gt; TCGA.WC.A87Y.01     2  0.0000      0.941 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     1  0.4608      0.648 0.68 0.00 0.22 0.00 0.10 0.00
#&gt; TCGA.V4.A9F5.01     2  0.0000      0.941 0.00 1.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-01-get-classes-5-a').parent().next().next().hide();
$('#tab-node-01-get-classes-5-a').click(function(){
  $('#tab-node-01-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-01-get-classes-6'>
<p><a id='tab-node-01-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.V4.A9EX.01     1  0.0000      0.869 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EU.01     1  0.2803      0.743 0.84 0.00 0.06 0.00 0.00 0.00 0.10
#&gt; TCGA.V4.A9F1.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     6  0.4644      0.487 0.00 0.02 0.12 0.18 0.00 0.68 0.00
#&gt; TCGA.V4.A9EV.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KI.01     6  0.6216      0.296 0.00 0.00 0.20 0.00 0.12 0.52 0.16
#&gt; TCGA.V4.A9EQ.01     2  0.0504      0.916 0.00 0.98 0.02 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EL.01     4  0.0000      0.000 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EI.01     1  0.0504      0.873 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9F0.01     2  0.1928      0.792 0.00 0.90 0.08 0.00 0.00 0.02 0.00
#&gt; TCGA.V4.A9E7.01     5  0.0504      0.000 0.00 0.00 0.00 0.00 0.98 0.02 0.00
#&gt; TCGA.RZ.AB0B.01     6  0.4335      0.512 0.00 0.20 0.02 0.04 0.02 0.72 0.00
#&gt; TCGA.VD.AA8O.01     3  0.3459      0.000 0.00 0.40 0.60 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KD.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A88A.01     1  0.1166      0.836 0.94 0.00 0.00 0.00 0.00 0.00 0.06
#&gt; TCGA.VD.AA8N.01     6  0.4418      0.600 0.00 0.08 0.00 0.08 0.06 0.76 0.02
#&gt; TCGA.VD.A8KM.01     2  0.2572      0.541 0.00 0.80 0.00 0.00 0.00 0.20 0.00
#&gt; TCGA.V4.A9EF.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EE.01     6  0.3257      0.582 0.00 0.02 0.04 0.00 0.02 0.84 0.08
#&gt; TCGA.WC.A87Y.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A883.01     7  0.3496      0.000 0.42 0.00 0.00 0.00 0.00 0.00 0.58
#&gt; TCGA.V4.A9F5.01     2  0.0000      0.942 0.00 1.00 0.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-01-get-classes-6-a').parent().next().next().hide();
$('#tab-node-01-get-classes-6-a').click(function(){
  $('#tab-node-01-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-01-get-classes-7'>
<p><a id='tab-node-01-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7   p8
#&gt; TCGA.V4.A9EX.01     1  0.0000      0.761 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F3.01     2  0.0471      0.913 0.00 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9EU.01     1  0.5715      0.274 0.50 0.00 0.10 0.02 0.00 0.00 0.32 0.06
#&gt; TCGA.V4.A9F1.01     2  0.0000      0.917 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V3.A9ZX.01     6  0.1408      0.308 0.00 0.00 0.02 0.02 0.00 0.94 0.00 0.02
#&gt; TCGA.V4.A9EV.01     2  0.0471      0.913 0.00 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.VD.A8KI.01     8  0.3434      0.000 0.00 0.00 0.00 0.00 0.14 0.10 0.00 0.76
#&gt; TCGA.V4.A9EQ.01     2  0.0808      0.897 0.00 0.96 0.04 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K8.01     2  0.0000      0.917 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EL.01     4  0.0471      0.000 0.00 0.00 0.00 0.98 0.00 0.02 0.00 0.00
#&gt; TCGA.V4.A9EI.01     1  0.0000      0.761 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F0.01     2  0.3714      0.718 0.00 0.80 0.10 0.00 0.04 0.02 0.02 0.02
#&gt; TCGA.V4.A9E7.01     5  0.0000      0.000 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.RZ.AB0B.01     6  0.7070      0.109 0.00 0.30 0.04 0.00 0.08 0.34 0.02 0.22
#&gt; TCGA.VD.AA8O.01     3  0.3021      0.000 0.00 0.16 0.80 0.00 0.02 0.02 0.00 0.00
#&gt; TCGA.VD.A8KD.01     2  0.0000      0.917 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A88A.01     1  0.0471      0.757 0.98 0.00 0.00 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.VD.AA8N.01     6  0.5589      0.168 0.00 0.00 0.04 0.02 0.18 0.56 0.00 0.20
#&gt; TCGA.VD.A8KM.01     2  0.4806      0.421 0.00 0.64 0.02 0.00 0.02 0.26 0.02 0.04
#&gt; TCGA.V4.A9EF.01     2  0.0471      0.908 0.00 0.98 0.02 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EE.01     6  0.5403      0.287 0.00 0.02 0.06 0.00 0.06 0.62 0.02 0.22
#&gt; TCGA.WC.A87Y.01     2  0.0471      0.913 0.00 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.WC.A883.01     7  0.2938      0.000 0.30 0.00 0.00 0.00 0.00 0.00 0.70 0.00
#&gt; TCGA.V4.A9F5.01     2  0.0000      0.917 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-01-get-classes-7-a').parent().next().next().hide();
$('#tab-node-01-get-classes-7-a').click(function(){
  $('#tab-node-01-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-01-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-01-consensus-heatmap'>
<ul>
<li><a href='#tab-node-01-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-01-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-01-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-01-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-01-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-01-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-01-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-01-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-01-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-01-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-01-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-01-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-01-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-01-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-01-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-01-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-01-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-01-membership-heatmap'>
<ul>
<li><a href='#tab-node-01-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-01-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-01-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-01-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-01-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-01-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-01-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-01-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-1-1.png" alt="plot of chunk tab-node-01-membership-heatmap-1"/></p>

</div>
<div id='tab-node-01-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-2-1.png" alt="plot of chunk tab-node-01-membership-heatmap-2"/></p>

</div>
<div id='tab-node-01-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-3-1.png" alt="plot of chunk tab-node-01-membership-heatmap-3"/></p>

</div>
<div id='tab-node-01-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-4-1.png" alt="plot of chunk tab-node-01-membership-heatmap-4"/></p>

</div>
<div id='tab-node-01-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-5-1.png" alt="plot of chunk tab-node-01-membership-heatmap-5"/></p>

</div>
<div id='tab-node-01-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-6-1.png" alt="plot of chunk tab-node-01-membership-heatmap-6"/></p>

</div>
<div id='tab-node-01-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-01-membership-heatmap-7-1.png" alt="plot of chunk tab-node-01-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-01-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-01-get-signatures'>
<ul>
<li><a href='#tab-node-01-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-01-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-01-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-01-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-01-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-01-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-01-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-01-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-1-1.png" alt="plot of chunk tab-node-01-get-signatures-1"/></p>

</div>
<div id='tab-node-01-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-2-1.png" alt="plot of chunk tab-node-01-get-signatures-2"/></p>

</div>
<div id='tab-node-01-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-3-1.png" alt="plot of chunk tab-node-01-get-signatures-3"/></p>

</div>
<div id='tab-node-01-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-4-1.png" alt="plot of chunk tab-node-01-get-signatures-4"/></p>

</div>
<div id='tab-node-01-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-5-1.png" alt="plot of chunk tab-node-01-get-signatures-5"/></p>

</div>
<div id='tab-node-01-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-6-1.png" alt="plot of chunk tab-node-01-get-signatures-6"/></p>

</div>
<div id='tab-node-01-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-01-get-signatures-7-1.png" alt="plot of chunk tab-node-01-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-01-signature_compare](figure_cola/node-01-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-01-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-01-dimension-reduction'>
<ul>
<li><a href='#tab-node-01-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-01-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-01-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-01-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-01-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-01-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-01-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-01-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-1-1.png" alt="plot of chunk tab-node-01-dimension-reduction-1"/></p>

</div>
<div id='tab-node-01-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-2-1.png" alt="plot of chunk tab-node-01-dimension-reduction-2"/></p>

</div>
<div id='tab-node-01-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-3-1.png" alt="plot of chunk tab-node-01-dimension-reduction-3"/></p>

</div>
<div id='tab-node-01-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-4-1.png" alt="plot of chunk tab-node-01-dimension-reduction-4"/></p>

</div>
<div id='tab-node-01-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-5-1.png" alt="plot of chunk tab-node-01-dimension-reduction-5"/></p>

</div>
<div id='tab-node-01-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-6-1.png" alt="plot of chunk tab-node-01-dimension-reduction-6"/></p>

</div>
<div id='tab-node-01-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-01-dimension-reduction-7-1.png" alt="plot of chunk tab-node-01-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-01-collect-classes](figure_cola/node-01-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### Node02


Parent node: [Node0](#Node0).
Child nodes: 
                Node011-leaf
        ,
                Node012-leaf
        ,
                Node013-leaf
        ,
                [Node021](#Node021)
        ,
                Node022-leaf
        ,
                Node023-leaf
        ,
                Node031-leaf
        ,
                Node032-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["02"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 35 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-02-collect-plots](figure_cola/node-02-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-02-select-partition-number](figure_cola/node-02-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4946 0.506   0.506
#> 3 3 0.898           0.953       0.966         0.3658 0.815   0.635
#> 4 4 0.814           0.878       0.927         0.1065 0.919   0.749
#> 5 5 0.786           0.803       0.895         0.0441 0.973   0.888
#> 6 6 0.775           0.703       0.864         0.0307 0.914   0.646
#> 7 7 0.752           0.634       0.851         0.0168 0.988   0.937
#> 8 8 0.794           0.652       0.835         0.0207 0.992   0.954
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-02-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-02-get-classes'>
<ul>
<li><a href='#tab-node-02-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-02-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-02-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-02-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-02-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-02-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-02-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-02-get-classes-1'>
<p><a id='tab-node-02-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1 p2
#&gt; TCGA.V4.A9EZ.01     2       0          1  0  1
#&gt; TCGA.WC.A885.01     1       0          1  1  0
#&gt; TCGA.V4.A9ET.01     1       0          1  1  0
#&gt; TCGA.V4.A9F7.01     2       0          1  0  1
#&gt; TCGA.V4.A9F4.01     1       0          1  1  0
#&gt; TCGA.VD.A8KJ.01     2       0          1  0  1
#&gt; TCGA.V4.A9EW.01     2       0          1  0  1
#&gt; TCGA.WC.A880.01     2       0          1  0  1
#&gt; TCGA.WC.A881.01     1       0          1  1  0
#&gt; TCGA.V3.A9ZY.01     2       0          1  0  1
#&gt; TCGA.WC.AA9E.01     1       0          1  1  0
#&gt; TCGA.V4.A9E9.01     1       0          1  1  0
#&gt; TCGA.VD.A8KB.01     1       0          1  1  0
#&gt; TCGA.VD.A8KG.01     1       0          1  1  0
#&gt; TCGA.VD.AA8M.01     2       0          1  0  1
#&gt; TCGA.VD.AA8S.01     2       0          1  0  1
#&gt; TCGA.V4.A9EC.01     2       0          1  0  1
#&gt; TCGA.VD.AA8Q.01     2       0          1  0  1
#&gt; TCGA.VD.A8K9.01     1       0          1  1  0
#&gt; TCGA.VD.AA8R.01     2       0          1  0  1
#&gt; TCGA.VD.A8KH.01     2       0          1  0  1
#&gt; TCGA.V4.A9EJ.01     1       0          1  1  0
#&gt; TCGA.VD.A8K7.01     2       0          1  0  1
#&gt; TCGA.VD.A8KA.01     1       0          1  1  0
#&gt; TCGA.V4.A9EK.01     1       0          1  1  0
#&gt; TCGA.YZ.A982.01     1       0          1  1  0
#&gt; TCGA.V4.A9EH.01     2       0          1  0  1
#&gt; TCGA.WC.A87U.01     2       0          1  0  1
#&gt; TCGA.YZ.A983.01     2       0          1  0  1
#&gt; TCGA.V4.A9EY.01     2       0          1  0  1
#&gt; TCGA.WC.A87T.01     2       0          1  0  1
#&gt; TCGA.VD.A8KE.01     2       0          1  0  1
#&gt; TCGA.VD.A8KO.01     2       0          1  0  1
#&gt; TCGA.V4.A9EA.01     1       0          1  1  0
#&gt; TCGA.WC.A884.01     2       0          1  0  1
</code></pre>

<script>
$('#tab-node-02-get-classes-1-a').parent().next().next().hide();
$('#tab-node-02-get-classes-1-a').click(function(){
  $('#tab-node-02-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-2'>
<p><a id='tab-node-02-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3
#&gt; TCGA.V4.A9EZ.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.WC.A885.01     1  0.0000      0.984 1.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.V4.A9F7.01     2  0.0892      0.923 0.00 0.98 0.02
#&gt; TCGA.V4.A9F4.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.VD.A8KJ.01     2  0.0892      0.923 0.00 0.98 0.02
#&gt; TCGA.V4.A9EW.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.WC.A880.01     2  0.0892      0.923 0.00 0.98 0.02
#&gt; TCGA.WC.A881.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.V3.A9ZY.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.WC.AA9E.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.V4.A9E9.01     1  0.0000      0.984 1.00 0.00 0.00
#&gt; TCGA.VD.A8KB.01     1  0.0000      0.984 1.00 0.00 0.00
#&gt; TCGA.VD.A8KG.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.VD.AA8M.01     2  0.0892      0.923 0.00 0.98 0.02
#&gt; TCGA.VD.AA8S.01     2  0.0892      0.923 0.00 0.98 0.02
#&gt; TCGA.V4.A9EC.01     2  0.4796      0.798 0.00 0.78 0.22
#&gt; TCGA.VD.AA8Q.01     2  0.5560      0.684 0.00 0.70 0.30
#&gt; TCGA.VD.A8K9.01     1  0.0000      0.984 1.00 0.00 0.00
#&gt; TCGA.VD.AA8R.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.VD.A8KH.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.V4.A9EJ.01     1  0.0000      0.984 1.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.VD.A8KA.01     1  0.0000      0.984 1.00 0.00 0.00
#&gt; TCGA.V4.A9EK.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.YZ.A982.01     1  0.0892      0.985 0.98 0.02 0.00
#&gt; TCGA.V4.A9EH.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.WC.A87U.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.YZ.A983.01     2  0.0892      0.923 0.00 0.98 0.02
#&gt; TCGA.V4.A9EY.01     2  0.4002      0.855 0.00 0.84 0.16
#&gt; TCGA.WC.A87T.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.VD.A8KE.01     2  0.3686      0.868 0.00 0.86 0.14
#&gt; TCGA.VD.A8KO.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.V4.A9EA.01     1  0.2959      0.894 0.90 0.10 0.00
#&gt; TCGA.WC.A884.01     2  0.0892      0.923 0.00 0.98 0.02
</code></pre>

<script>
$('#tab-node-02-get-classes-2-a').parent().next().next().hide();
$('#tab-node-02-get-classes-2-a').click(function(){
  $('#tab-node-02-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-3'>
<p><a id='tab-node-02-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4
#&gt; TCGA.V4.A9EZ.01     3   0.304      0.907 0.00 0.02 0.88 0.10
#&gt; TCGA.WC.A885.01     1   0.000      0.912 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     4   0.441      0.758 0.30 0.00 0.00 0.70
#&gt; TCGA.V4.A9F7.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9F4.01     1   0.380      0.661 0.78 0.00 0.00 0.22
#&gt; TCGA.VD.A8KJ.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EW.01     3   0.234      0.922 0.00 0.00 0.90 0.10
#&gt; TCGA.WC.A880.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.A881.01     4   0.491      0.540 0.42 0.00 0.00 0.58
#&gt; TCGA.V3.A9ZY.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.WC.AA9E.01     4   0.441      0.758 0.30 0.00 0.00 0.70
#&gt; TCGA.V4.A9E9.01     1   0.000      0.912 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KB.01     1   0.234      0.853 0.90 0.00 0.00 0.10
#&gt; TCGA.VD.A8KG.01     4   0.234      0.809 0.10 0.00 0.00 0.90
#&gt; TCGA.VD.AA8M.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2   0.380      0.733 0.00 0.78 0.22 0.00
#&gt; TCGA.VD.AA8Q.01     2   0.452      0.569 0.00 0.68 0.32 0.00
#&gt; TCGA.VD.A8K9.01     1   0.000      0.912 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8R.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.VD.A8KH.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.V4.A9EJ.01     1   0.000      0.912 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.VD.A8KA.01     1   0.265      0.833 0.88 0.00 0.00 0.12
#&gt; TCGA.V4.A9EK.01     4   0.234      0.809 0.10 0.00 0.00 0.90
#&gt; TCGA.YZ.A982.01     4   0.234      0.809 0.10 0.00 0.00 0.90
#&gt; TCGA.V4.A9EH.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.WC.A87U.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.YZ.A983.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2   0.121      0.908 0.00 0.96 0.04 0.00
#&gt; TCGA.WC.A87T.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.VD.A8KE.01     2   0.000      0.934 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KO.01     3   0.000      0.980 0.00 0.00 1.00 0.00
#&gt; TCGA.V4.A9EA.01     1   0.000      0.912 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2   0.000      0.934 0.00 1.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-3-a').parent().next().next().hide();
$('#tab-node-02-get-classes-3-a').click(function(){
  $('#tab-node-02-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-4'>
<p><a id='tab-node-02-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5
#&gt; TCGA.V4.A9EZ.01     5   0.311      0.744 0.00 0.02 0.14 0.00 0.84
#&gt; TCGA.WC.A885.01     1   0.000      0.856 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     4   0.273      0.682 0.16 0.00 0.00 0.84 0.00
#&gt; TCGA.V4.A9F7.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F4.01     1   0.413      0.459 0.62 0.00 0.00 0.38 0.00
#&gt; TCGA.VD.A8KJ.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EW.01     5   0.398      0.698 0.00 0.00 0.34 0.00 0.66
#&gt; TCGA.WC.A880.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     4   0.380      0.499 0.30 0.00 0.00 0.70 0.00
#&gt; TCGA.V3.A9ZY.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.AA9E.01     4   0.342      0.608 0.24 0.00 0.00 0.76 0.00
#&gt; TCGA.V4.A9E9.01     1   0.000      0.856 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KB.01     1   0.425      0.625 0.70 0.00 0.00 0.28 0.02
#&gt; TCGA.VD.A8KG.01     4   0.373      0.709 0.04 0.00 0.00 0.80 0.16
#&gt; TCGA.VD.AA8M.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2   0.464      0.663 0.00 0.74 0.10 0.00 0.16
#&gt; TCGA.VD.AA8Q.01     2   0.418      0.432 0.00 0.60 0.40 0.00 0.00
#&gt; TCGA.VD.A8K9.01     1   0.141      0.834 0.94 0.00 0.00 0.06 0.00
#&gt; TCGA.VD.AA8R.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KH.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     1   0.000      0.856 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KA.01     1   0.262      0.810 0.88 0.00 0.00 0.10 0.02
#&gt; TCGA.V4.A9EK.01     4   0.273      0.704 0.00 0.00 0.00 0.84 0.16
#&gt; TCGA.YZ.A982.01     4   0.273      0.704 0.00 0.00 0.00 0.84 0.16
#&gt; TCGA.V4.A9EH.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.A87U.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.YZ.A983.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2   0.356      0.668 0.00 0.74 0.26 0.00 0.00
#&gt; TCGA.WC.A87T.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KE.01     2   0.293      0.752 0.00 0.82 0.18 0.00 0.00
#&gt; TCGA.VD.A8KO.01     3   0.000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     1   0.000      0.856 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2   0.000      0.868 0.00 1.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-4-a').parent().next().next().hide();
$('#tab-node-02-get-classes-4-a').click(function(){
  $('#tab-node-02-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-5'>
<p><a id='tab-node-02-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.V4.A9EZ.01     5  0.0547     0.5957 0.00 0.00 0.02 0.00 0.98 0.00
#&gt; TCGA.WC.A885.01     1  0.1556     0.8273 0.92 0.00 0.00 0.08 0.00 0.00
#&gt; TCGA.V4.A9ET.01     4  0.4067     0.4941 0.04 0.00 0.00 0.70 0.00 0.26
#&gt; TCGA.V4.A9F7.01     2  0.0000     0.8296 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F4.01     4  0.3982     0.6479 0.20 0.00 0.00 0.74 0.00 0.06
#&gt; TCGA.VD.A8KJ.01     2  0.0547     0.8177 0.00 0.98 0.00 0.00 0.02 0.00
#&gt; TCGA.V4.A9EW.01     5  0.3711     0.6237 0.02 0.00 0.26 0.00 0.72 0.00
#&gt; TCGA.WC.A880.01     2  0.0000     0.8296 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     4  0.1556     0.6515 0.00 0.00 0.00 0.92 0.00 0.08
#&gt; TCGA.V3.A9ZY.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.AA9E.01     4  0.3351     0.6125 0.04 0.00 0.00 0.80 0.00 0.16
#&gt; TCGA.V4.A9E9.01     1  0.2793     0.7980 0.80 0.00 0.00 0.20 0.00 0.00
#&gt; TCGA.VD.A8KB.01     4  0.3156     0.5855 0.18 0.00 0.00 0.80 0.00 0.02
#&gt; TCGA.VD.A8KG.01     6  0.4810     0.5513 0.22 0.00 0.00 0.12 0.00 0.66
#&gt; TCGA.VD.AA8M.01     2  0.0000     0.8296 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2  0.0000     0.8296 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.5364     0.3428 0.00 0.56 0.14 0.00 0.30 0.00
#&gt; TCGA.VD.AA8Q.01     3  0.3828    -0.0112 0.00 0.44 0.56 0.00 0.00 0.00
#&gt; TCGA.VD.A8K9.01     1  0.3821     0.6832 0.74 0.00 0.00 0.22 0.00 0.04
#&gt; TCGA.VD.AA8R.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KH.01     3  0.0547     0.8872 0.00 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.V4.A9EJ.01     1  0.1814     0.8297 0.90 0.00 0.00 0.10 0.00 0.00
#&gt; TCGA.VD.A8K7.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KA.01     4  0.4575     0.1832 0.34 0.00 0.00 0.62 0.02 0.02
#&gt; TCGA.V4.A9EK.01     6  0.2094     0.7774 0.02 0.00 0.00 0.08 0.00 0.90
#&gt; TCGA.YZ.A982.01     6  0.1556     0.7822 0.00 0.00 0.00 0.08 0.00 0.92
#&gt; TCGA.V4.A9EH.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87U.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A983.01     2  0.0000     0.8296 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2  0.3756     0.3737 0.00 0.60 0.40 0.00 0.00 0.00
#&gt; TCGA.WC.A87T.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KE.01     2  0.3706     0.4183 0.00 0.62 0.38 0.00 0.00 0.00
#&gt; TCGA.VD.A8KO.01     3  0.0000     0.9097 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     1  0.2631     0.7973 0.82 0.00 0.00 0.18 0.00 0.00
#&gt; TCGA.WC.A884.01     2  0.0000     0.8296 0.00 1.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-5-a').parent().next().next().hide();
$('#tab-node-02-get-classes-5-a').click(function(){
  $('#tab-node-02-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-6'>
<p><a id='tab-node-02-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.V4.A9EZ.01     5  0.0000     0.4345 0.00 0.00 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.A885.01     1  0.2016     0.5998 0.90 0.00 0.00 0.06 0.00 0.00 0.04
#&gt; TCGA.V4.A9ET.01     4  0.5046     0.6166 0.10 0.00 0.00 0.66 0.00 0.18 0.06
#&gt; TCGA.V4.A9F7.01     2  0.0504     0.8224 0.00 0.98 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9F4.01     4  0.1928     0.8011 0.08 0.00 0.00 0.90 0.00 0.02 0.00
#&gt; TCGA.VD.A8KJ.01     2  0.2422     0.6980 0.00 0.82 0.00 0.00 0.00 0.00 0.18
#&gt; TCGA.V4.A9EW.01     5  0.3685     0.4964 0.02 0.00 0.32 0.00 0.66 0.00 0.00
#&gt; TCGA.WC.A880.01     2  0.0000     0.8243 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     4  0.0504     0.7894 0.00 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.V3.A9ZY.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.AA9E.01     4  0.2769     0.7779 0.08 0.00 0.00 0.86 0.00 0.04 0.02
#&gt; TCGA.V4.A9E9.01     1  0.5002    -0.0427 0.48 0.00 0.00 0.12 0.00 0.00 0.40
#&gt; TCGA.VD.A8KB.01     4  0.1664     0.7769 0.06 0.00 0.00 0.92 0.00 0.00 0.02
#&gt; TCGA.VD.A8KG.01     7  0.6118    -0.2883 0.26 0.00 0.00 0.04 0.00 0.26 0.44
#&gt; TCGA.VD.AA8M.01     2  0.0504     0.8184 0.00 0.98 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.VD.AA8S.01     2  0.0000     0.8243 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.5708     0.5002 0.02 0.60 0.14 0.00 0.20 0.00 0.04
#&gt; TCGA.VD.AA8Q.01     3  0.3943     0.0132 0.00 0.42 0.56 0.00 0.00 0.00 0.02
#&gt; TCGA.VD.A8K9.01     1  0.3086     0.4900 0.80 0.00 0.00 0.16 0.00 0.00 0.04
#&gt; TCGA.VD.AA8R.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KH.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     1  0.0504     0.5834 0.98 0.00 0.00 0.02 0.00 0.00 0.00
#&gt; TCGA.VD.A8K7.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KA.01     4  0.5166     0.5357 0.20 0.00 0.00 0.66 0.04 0.02 0.08
#&gt; TCGA.V4.A9EK.01     6  0.2512     0.8401 0.10 0.00 0.00 0.04 0.00 0.86 0.00
#&gt; TCGA.YZ.A982.01     6  0.0504     0.8463 0.00 0.00 0.00 0.02 0.00 0.98 0.00
#&gt; TCGA.V4.A9EH.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A87U.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A983.01     2  0.0504     0.8224 0.00 0.98 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.V4.A9EY.01     2  0.3909     0.3575 0.00 0.58 0.40 0.00 0.00 0.00 0.02
#&gt; TCGA.WC.A87T.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KE.01     2  0.3517     0.5919 0.00 0.70 0.28 0.00 0.00 0.00 0.02
#&gt; TCGA.VD.A8KO.01     3  0.0000     0.9126 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     7  0.4505    -0.4806 0.44 0.00 0.00 0.06 0.00 0.00 0.50
#&gt; TCGA.WC.A884.01     2  0.0000     0.8243 0.00 1.00 0.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-6-a').parent().next().next().hide();
$('#tab-node-02-get-classes-6-a').click(function(){
  $('#tab-node-02-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-7'>
<p><a id='tab-node-02-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7   p8
#&gt; TCGA.V4.A9EZ.01     5  0.0000      0.339 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.WC.A885.01     1  0.0941      0.690 0.96 0.00 0.02 0.02 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     4  0.4355      0.549 0.02 0.00 0.04 0.72 0.00 0.16 0.06 0.00
#&gt; TCGA.V4.A9F7.01     2  0.0471      0.783 0.00 0.98 0.02 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F4.01     4  0.0471      0.723 0.02 0.00 0.00 0.98 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KJ.01     2  0.2719      0.667 0.00 0.80 0.18 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.V4.A9EW.01     5  0.5600      0.394 0.00 0.00 0.22 0.00 0.48 0.00 0.04 0.26
#&gt; TCGA.WC.A880.01     2  0.0000      0.782 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     4  0.2994      0.696 0.00 0.00 0.14 0.80 0.00 0.00 0.06 0.00
#&gt; TCGA.V3.A9ZY.01     8  0.0000      0.877 0.00 0.00 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.WC.AA9E.01     4  0.2071      0.706 0.00 0.00 0.04 0.90 0.00 0.04 0.02 0.00
#&gt; TCGA.V4.A9E9.01     1  0.3514      0.617 0.64 0.00 0.34 0.02 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KB.01     4  0.3744      0.652 0.02 0.00 0.18 0.74 0.00 0.00 0.06 0.00
#&gt; TCGA.VD.A8KG.01     7  0.4061      0.000 0.12 0.00 0.00 0.02 0.00 0.14 0.72 0.00
#&gt; TCGA.VD.AA8M.01     2  0.0471      0.778 0.00 0.98 0.02 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8S.01     2  0.0471      0.781 0.00 0.98 0.02 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EC.01     2  0.6468      0.311 0.00 0.46 0.12 0.00 0.26 0.00 0.04 0.12
#&gt; TCGA.VD.AA8Q.01     8  0.4953      0.206 0.00 0.32 0.12 0.00 0.00 0.00 0.02 0.54
#&gt; TCGA.VD.A8K9.01     1  0.3454      0.540 0.80 0.00 0.02 0.12 0.00 0.02 0.04 0.00
#&gt; TCGA.VD.AA8R.01     8  0.0000      0.877 0.00 0.00 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.VD.A8KH.01     8  0.0808      0.843 0.00 0.00 0.04 0.00 0.00 0.00 0.00 0.96
#&gt; TCGA.V4.A9EJ.01     1  0.0941      0.678 0.96 0.00 0.00 0.02 0.00 0.00 0.02 0.00
#&gt; TCGA.VD.A8K7.01     8  0.0000      0.877 0.00 0.00 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.VD.A8KA.01     4  0.5933      0.342 0.24 0.00 0.10 0.48 0.00 0.00 0.18 0.00
#&gt; TCGA.V4.A9EK.01     6  0.2071      0.873 0.02 0.00 0.00 0.04 0.00 0.90 0.04 0.00
#&gt; TCGA.YZ.A982.01     6  0.0000      0.876 0.00 0.00 0.00 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EH.01     8  0.0000      0.877 0.00 0.00 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.WC.A87U.01     8  0.1804      0.840 0.00 0.00 0.08 0.00 0.00 0.00 0.02 0.90
#&gt; TCGA.YZ.A983.01     2  0.0471      0.783 0.00 0.98 0.02 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EY.01     2  0.4848      0.347 0.00 0.54 0.10 0.00 0.00 0.00 0.02 0.34
#&gt; TCGA.WC.A87T.01     8  0.1341      0.855 0.00 0.00 0.08 0.00 0.00 0.00 0.00 0.92
#&gt; TCGA.VD.A8KE.01     2  0.4740      0.431 0.00 0.58 0.10 0.00 0.00 0.00 0.02 0.30
#&gt; TCGA.VD.A8KO.01     8  0.1091      0.864 0.00 0.00 0.06 0.00 0.00 0.00 0.00 0.94
#&gt; TCGA.V4.A9EA.01     1  0.3658      0.578 0.58 0.00 0.40 0.02 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A884.01     2  0.0471      0.781 0.00 0.98 0.02 0.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-7-a').parent().next().next().hide();
$('#tab-node-02-get-classes-7-a').click(function(){
  $('#tab-node-02-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-02-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-02-consensus-heatmap'>
<ul>
<li><a href='#tab-node-02-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-02-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-02-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-02-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-02-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-02-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-02-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-02-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-02-membership-heatmap'>
<ul>
<li><a href='#tab-node-02-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-02-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-02-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-02-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-02-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-02-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-02-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-1-1.png" alt="plot of chunk tab-node-02-membership-heatmap-1"/></p>

</div>
<div id='tab-node-02-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-2-1.png" alt="plot of chunk tab-node-02-membership-heatmap-2"/></p>

</div>
<div id='tab-node-02-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-3-1.png" alt="plot of chunk tab-node-02-membership-heatmap-3"/></p>

</div>
<div id='tab-node-02-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-4-1.png" alt="plot of chunk tab-node-02-membership-heatmap-4"/></p>

</div>
<div id='tab-node-02-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-5-1.png" alt="plot of chunk tab-node-02-membership-heatmap-5"/></p>

</div>
<div id='tab-node-02-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-6-1.png" alt="plot of chunk tab-node-02-membership-heatmap-6"/></p>

</div>
<div id='tab-node-02-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-7-1.png" alt="plot of chunk tab-node-02-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-02-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-02-get-signatures'>
<ul>
<li><a href='#tab-node-02-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-02-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-02-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-02-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-02-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-02-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-02-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-1-1.png" alt="plot of chunk tab-node-02-get-signatures-1"/></p>

</div>
<div id='tab-node-02-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-2-1.png" alt="plot of chunk tab-node-02-get-signatures-2"/></p>

</div>
<div id='tab-node-02-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-3-1.png" alt="plot of chunk tab-node-02-get-signatures-3"/></p>

</div>
<div id='tab-node-02-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-4-1.png" alt="plot of chunk tab-node-02-get-signatures-4"/></p>

</div>
<div id='tab-node-02-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-5-1.png" alt="plot of chunk tab-node-02-get-signatures-5"/></p>

</div>
<div id='tab-node-02-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-6-1.png" alt="plot of chunk tab-node-02-get-signatures-6"/></p>

</div>
<div id='tab-node-02-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-7-1.png" alt="plot of chunk tab-node-02-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-02-signature_compare](figure_cola/node-02-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-02-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-02-dimension-reduction'>
<ul>
<li><a href='#tab-node-02-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-02-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-02-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-02-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-02-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-02-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-02-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-1-1.png" alt="plot of chunk tab-node-02-dimension-reduction-1"/></p>

</div>
<div id='tab-node-02-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-2-1.png" alt="plot of chunk tab-node-02-dimension-reduction-2"/></p>

</div>
<div id='tab-node-02-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-3-1.png" alt="plot of chunk tab-node-02-dimension-reduction-3"/></p>

</div>
<div id='tab-node-02-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-4-1.png" alt="plot of chunk tab-node-02-dimension-reduction-4"/></p>

</div>
<div id='tab-node-02-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-5-1.png" alt="plot of chunk tab-node-02-dimension-reduction-5"/></p>

</div>
<div id='tab-node-02-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-6-1.png" alt="plot of chunk tab-node-02-dimension-reduction-6"/></p>

</div>
<div id='tab-node-02-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-7-1.png" alt="plot of chunk tab-node-02-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-02-collect-classes](figure_cola/node-02-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### Node021


Parent node: [Node02](#Node02).
Child nodes: 
                Node0211-leaf
        ,
                Node0212-leaf
        ,
                Node0213-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["021"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 14 columns.
#>   Top rows (1000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-021-collect-plots](figure_cola/node-021-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-021-select-partition-number](figure_cola/node-021-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.242           0.699       0.866         0.5236 0.462   0.462
#> 3 3 1.000           0.991       0.996         0.2413 0.890   0.762
#> 4 4 0.670           0.788       0.861         0.1722 0.890   0.688
#> 5 5 0.692           0.492       0.797         0.0851 0.824   0.429
#> 6 6 0.747           0.347       0.696         0.0616 0.802   0.250
#> 7 7 0.747           0.384       0.761         0.0228 0.879   0.312
#> 8 8 0.802           0.531       0.741         0.0281 0.945   0.500
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-021-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-021-get-classes'>
<ul>
<li><a href='#tab-node-021-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-021-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-021-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-021-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-021-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-021-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-021-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-021-get-classes-1'>
<p><a id='tab-node-021-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2
#&gt; TCGA.WC.A885.01     1   0.000      0.855 1.00 0.00
#&gt; TCGA.V4.A9ET.01     2   0.000      0.724 0.00 1.00
#&gt; TCGA.V4.A9F4.01     2   0.529      0.754 0.12 0.88
#&gt; TCGA.WC.A881.01     2   0.529      0.754 0.12 0.88
#&gt; TCGA.WC.AA9E.01     2   0.529      0.754 0.12 0.88
#&gt; TCGA.V4.A9E9.01     1   0.795      0.645 0.76 0.24
#&gt; TCGA.VD.A8KB.01     2   0.990      0.153 0.44 0.56
#&gt; TCGA.VD.A8KG.01     1   0.529      0.729 0.88 0.12
#&gt; TCGA.VD.A8K9.01     1   0.000      0.855 1.00 0.00
#&gt; TCGA.V4.A9EJ.01     1   0.000      0.855 1.00 0.00
#&gt; TCGA.VD.A8KA.01     1   0.000      0.855 1.00 0.00
#&gt; TCGA.V4.A9EK.01     2   0.795      0.604 0.24 0.76
#&gt; TCGA.YZ.A982.01     2   0.795      0.604 0.24 0.76
#&gt; TCGA.V4.A9EA.01     1   0.795      0.645 0.76 0.24
</code></pre>

<script>
$('#tab-node-021-get-classes-1-a').parent().next().next().hide();
$('#tab-node-021-get-classes-1-a').click(function(){
  $('#tab-node-021-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-021-get-classes-2'>
<p><a id='tab-node-021-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3
#&gt; TCGA.WC.A885.01     1  0.0000      0.993 1.00 0.00 0.00
#&gt; TCGA.V4.A9ET.01     2  0.0892      0.977 0.00 0.98 0.02
#&gt; TCGA.V4.A9F4.01     2  0.0000      0.994 0.00 1.00 0.00
#&gt; TCGA.WC.A881.01     2  0.0000      0.994 0.00 1.00 0.00
#&gt; TCGA.WC.AA9E.01     2  0.0000      0.994 0.00 1.00 0.00
#&gt; TCGA.V4.A9E9.01     1  0.0000      0.993 1.00 0.00 0.00
#&gt; TCGA.VD.A8KB.01     2  0.0000      0.994 0.00 1.00 0.00
#&gt; TCGA.VD.A8KG.01     1  0.0892      0.980 0.98 0.00 0.02
#&gt; TCGA.VD.A8K9.01     1  0.0000      0.993 1.00 0.00 0.00
#&gt; TCGA.V4.A9EJ.01     1  0.0000      0.993 1.00 0.00 0.00
#&gt; TCGA.VD.A8KA.01     1  0.0892      0.979 0.98 0.02 0.00
#&gt; TCGA.V4.A9EK.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.YZ.A982.01     3  0.0000      1.000 0.00 0.00 1.00
#&gt; TCGA.V4.A9EA.01     1  0.0000      0.993 1.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-021-get-classes-2-a').parent().next().next().hide();
$('#tab-node-021-get-classes-2-a').click(function(){
  $('#tab-node-021-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-021-get-classes-3'>
<p><a id='tab-node-021-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2 p3   p4
#&gt; TCGA.WC.A885.01     1  0.4977      0.301 0.54 0.00  0 0.46
#&gt; TCGA.V4.A9ET.01     2  0.3606      0.829 0.14 0.84  0 0.02
#&gt; TCGA.V4.A9F4.01     2  0.1211      0.854 0.00 0.96  0 0.04
#&gt; TCGA.WC.A881.01     2  0.3335      0.836 0.02 0.86  0 0.12
#&gt; TCGA.WC.AA9E.01     2  0.2647      0.833 0.00 0.88  0 0.12
#&gt; TCGA.V4.A9E9.01     4  0.2647      1.000 0.12 0.00  0 0.88
#&gt; TCGA.VD.A8KB.01     2  0.4332      0.820 0.16 0.80  0 0.04
#&gt; TCGA.VD.A8KG.01     1  0.0000      0.635 1.00 0.00  0 0.00
#&gt; TCGA.VD.A8K9.01     1  0.4277      0.654 0.72 0.00  0 0.28
#&gt; TCGA.V4.A9EJ.01     1  0.4277      0.654 0.72 0.00  0 0.28
#&gt; TCGA.VD.A8KA.01     1  0.0707      0.621 0.98 0.02  0 0.00
#&gt; TCGA.V4.A9EK.01     3  0.0000      1.000 0.00 0.00  1 0.00
#&gt; TCGA.YZ.A982.01     3  0.0000      1.000 0.00 0.00  1 0.00
#&gt; TCGA.V4.A9EA.01     4  0.2647      1.000 0.12 0.00  0 0.88
</code></pre>

<script>
$('#tab-node-021-get-classes-3-a').parent().next().next().hide();
$('#tab-node-021-get-classes-3-a').click(function(){
  $('#tab-node-021-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-021-get-classes-4'>
<p><a id='tab-node-021-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5
#&gt; TCGA.WC.A885.01     4  0.5834      0.600 0.16 0.02 0.00 0.66 0.16
#&gt; TCGA.V4.A9ET.01     2  0.4527      0.417 0.12 0.78 0.02 0.00 0.08
#&gt; TCGA.V4.A9F4.01     2  0.4613      0.150 0.00 0.62 0.00 0.02 0.36
#&gt; TCGA.WC.A881.01     2  0.4798     -0.327 0.02 0.54 0.00 0.00 0.44
#&gt; TCGA.WC.AA9E.01     5  0.2929      0.000 0.00 0.18 0.00 0.00 0.82
#&gt; TCGA.V4.A9E9.01     4  0.0000      0.600 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.VD.A8KB.01     2  0.0609      0.440 0.00 0.98 0.00 0.02 0.00
#&gt; TCGA.VD.A8KG.01     1  0.0609      0.681 0.98 0.00 0.00 0.02 0.00
#&gt; TCGA.VD.A8K9.01     4  0.6184      0.520 0.38 0.00 0.00 0.48 0.14
#&gt; TCGA.V4.A9EJ.01     4  0.6184      0.520 0.38 0.00 0.00 0.48 0.14
#&gt; TCGA.VD.A8KA.01     1  0.4825      0.694 0.72 0.22 0.00 0.04 0.02
#&gt; TCGA.V4.A9EK.01     3  0.0000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.YZ.A982.01     3  0.0000      1.000 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     4  0.0609      0.589 0.00 0.02 0.00 0.98 0.00
</code></pre>

<script>
$('#tab-node-021-get-classes-4-a').parent().next().next().hide();
$('#tab-node-021-get-classes-4-a').click(function(){
  $('#tab-node-021-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-021-get-classes-5'>
<p><a id='tab-node-021-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.WC.A885.01     6  0.6175     0.0000 0.08 0.04 0.00 0.32 0.02 0.54
#&gt; TCGA.V4.A9ET.01     2  0.6138     0.3772 0.12 0.60 0.00 0.00 0.10 0.18
#&gt; TCGA.V4.A9F4.01     5  0.3828    -0.1171 0.00 0.44 0.00 0.00 0.56 0.00
#&gt; TCGA.WC.A881.01     5  0.5802     0.0136 0.00 0.40 0.00 0.00 0.42 0.18
#&gt; TCGA.WC.AA9E.01     5  0.0937     0.3448 0.00 0.04 0.00 0.00 0.96 0.00
#&gt; TCGA.V4.A9E9.01     4  0.0000     0.8947 0.00 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.VD.A8KB.01     2  0.0000     0.4035 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KG.01     1  0.0000     0.1856 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K9.01     1  0.5698     0.0166 0.44 0.00 0.00 0.16 0.00 0.40
#&gt; TCGA.V4.A9EJ.01     1  0.5698     0.0166 0.44 0.00 0.00 0.16 0.00 0.40
#&gt; TCGA.VD.A8KA.01     1  0.5682    -0.0776 0.46 0.38 0.00 0.00 0.00 0.16
#&gt; TCGA.V4.A9EK.01     3  0.0000     0.9546 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A982.01     3  0.1480     0.9546 0.00 0.00 0.94 0.00 0.02 0.04
#&gt; TCGA.V4.A9EA.01     4  0.1267     0.8974 0.00 0.06 0.00 0.94 0.00 0.00
</code></pre>

<script>
$('#tab-node-021-get-classes-5-a').parent().next().next().hide();
$('#tab-node-021-get-classes-5-a').click(function(){
  $('#tab-node-021-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-021-get-classes-6'>
<p><a id='tab-node-021-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.WC.A885.01     6  0.4889      0.117 0.00 0.12 0.00 0.22 0.00 0.64 0.02
#&gt; TCGA.V4.A9ET.01     2  0.4882      0.000 0.04 0.56 0.00 0.00 0.36 0.00 0.04
#&gt; TCGA.V4.A9F4.01     5  0.0000      0.172 0.00 0.00 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.WC.A881.01     7  0.0504      0.000 0.00 0.00 0.00 0.00 0.02 0.00 0.98
#&gt; TCGA.WC.AA9E.01     5  0.4348      0.200 0.00 0.18 0.00 0.00 0.68 0.00 0.14
#&gt; TCGA.V4.A9E9.01     4  0.2163      0.821 0.00 0.02 0.00 0.88 0.00 0.10 0.00
#&gt; TCGA.VD.A8KB.01     5  0.7322     -0.496 0.00 0.28 0.00 0.10 0.34 0.04 0.24
#&gt; TCGA.VD.A8KG.01     1  0.0000      0.379 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8K9.01     6  0.4998      0.640 0.32 0.00 0.00 0.14 0.00 0.54 0.00
#&gt; TCGA.V4.A9EJ.01     6  0.4998      0.640 0.32 0.00 0.00 0.14 0.00 0.54 0.00
#&gt; TCGA.VD.A8KA.01     1  0.6719      0.379 0.52 0.08 0.00 0.08 0.00 0.22 0.10
#&gt; TCGA.V4.A9EK.01     3  0.0000      0.847 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A982.01     3  0.3011      0.847 0.00 0.06 0.82 0.00 0.00 0.12 0.00
#&gt; TCGA.V4.A9EA.01     4  0.0000      0.832 0.00 0.00 0.00 1.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-021-get-classes-6-a').parent().next().next().hide();
$('#tab-node-021-get-classes-6-a').click(function(){
  $('#tab-node-021-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-021-get-classes-7'>
<p><a id='tab-node-021-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2  p3   p4   p5   p6   p7   p8
#&gt; TCGA.WC.A885.01     8  0.0471      0.000 0.00 0.00 0.0 0.02 0.00 0.00 0.00 0.98
#&gt; TCGA.V4.A9ET.01     2  0.0000      0.410 0.00 1.00 0.0 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9F4.01     5  0.3551      0.590 0.06 0.22 0.0 0.00 0.72 0.00 0.00 0.00
#&gt; TCGA.WC.A881.01     7  0.0808      0.000 0.00 0.04 0.0 0.00 0.00 0.00 0.96 0.00
#&gt; TCGA.WC.AA9E.01     5  0.1765      0.621 0.00 0.00 0.0 0.00 0.88 0.00 0.12 0.00
#&gt; TCGA.V4.A9E9.01     4  0.1341      0.734 0.00 0.00 0.0 0.92 0.00 0.00 0.00 0.08
#&gt; TCGA.VD.A8KB.01     2  0.5273      0.376 0.34 0.50 0.0 0.04 0.00 0.00 0.12 0.00
#&gt; TCGA.VD.A8KG.01     1  0.3690      0.256 0.56 0.02 0.0 0.00 0.00 0.42 0.00 0.00
#&gt; TCGA.VD.A8K9.01     6  0.2756      1.000 0.00 0.00 0.0 0.00 0.00 0.74 0.00 0.26
#&gt; TCGA.V4.A9EJ.01     6  0.2756      1.000 0.00 0.00 0.0 0.00 0.00 0.74 0.00 0.26
#&gt; TCGA.VD.A8KA.01     1  0.3320      0.243 0.80 0.00 0.0 0.04 0.00 0.00 0.04 0.12
#&gt; TCGA.V4.A9EK.01     3  0.5087      0.733 0.06 0.00 0.7 0.04 0.08 0.10 0.00 0.02
#&gt; TCGA.YZ.A982.01     3  0.0000      0.733 0.00 0.00 1.0 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EA.01     4  0.3897      0.745 0.10 0.00 0.0 0.78 0.04 0.04 0.04 0.00
</code></pre>

<script>
$('#tab-node-021-get-classes-7-a').parent().next().next().hide();
$('#tab-node-021-get-classes-7-a').click(function(){
  $('#tab-node-021-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-021-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-021-consensus-heatmap'>
<ul>
<li><a href='#tab-node-021-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-021-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-021-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-021-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-021-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-021-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-021-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-021-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-021-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-021-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-021-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-021-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-021-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-021-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-021-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-021-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-021-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-021-membership-heatmap'>
<ul>
<li><a href='#tab-node-021-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-021-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-021-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-021-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-021-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-021-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-021-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-021-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-1-1.png" alt="plot of chunk tab-node-021-membership-heatmap-1"/></p>

</div>
<div id='tab-node-021-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-2-1.png" alt="plot of chunk tab-node-021-membership-heatmap-2"/></p>

</div>
<div id='tab-node-021-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-3-1.png" alt="plot of chunk tab-node-021-membership-heatmap-3"/></p>

</div>
<div id='tab-node-021-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-4-1.png" alt="plot of chunk tab-node-021-membership-heatmap-4"/></p>

</div>
<div id='tab-node-021-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-5-1.png" alt="plot of chunk tab-node-021-membership-heatmap-5"/></p>

</div>
<div id='tab-node-021-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-6-1.png" alt="plot of chunk tab-node-021-membership-heatmap-6"/></p>

</div>
<div id='tab-node-021-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-021-membership-heatmap-7-1.png" alt="plot of chunk tab-node-021-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-021-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-021-get-signatures'>
<ul>
<li><a href='#tab-node-021-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-021-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-021-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-021-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-021-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-021-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-021-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-021-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-1-1.png" alt="plot of chunk tab-node-021-get-signatures-1"/></p>

</div>
<div id='tab-node-021-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-2-1.png" alt="plot of chunk tab-node-021-get-signatures-2"/></p>

</div>
<div id='tab-node-021-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-3-1.png" alt="plot of chunk tab-node-021-get-signatures-3"/></p>

</div>
<div id='tab-node-021-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-4-1.png" alt="plot of chunk tab-node-021-get-signatures-4"/></p>

</div>
<div id='tab-node-021-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-5-1.png" alt="plot of chunk tab-node-021-get-signatures-5"/></p>

</div>
<div id='tab-node-021-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-6-1.png" alt="plot of chunk tab-node-021-get-signatures-6"/></p>

</div>
<div id='tab-node-021-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-021-get-signatures-7-1.png" alt="plot of chunk tab-node-021-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-021-signature_compare](figure_cola/node-021-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-021-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-021-dimension-reduction'>
<ul>
<li><a href='#tab-node-021-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-021-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-021-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-021-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-021-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-021-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-021-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-021-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-1-1.png" alt="plot of chunk tab-node-021-dimension-reduction-1"/></p>

</div>
<div id='tab-node-021-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-2-1.png" alt="plot of chunk tab-node-021-dimension-reduction-2"/></p>

</div>
<div id='tab-node-021-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-3-1.png" alt="plot of chunk tab-node-021-dimension-reduction-3"/></p>

</div>
<div id='tab-node-021-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-4-1.png" alt="plot of chunk tab-node-021-dimension-reduction-4"/></p>

</div>
<div id='tab-node-021-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-5-1.png" alt="plot of chunk tab-node-021-dimension-reduction-5"/></p>

</div>
<div id='tab-node-021-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-6-1.png" alt="plot of chunk tab-node-021-dimension-reduction-6"/></p>

</div>
<div id='tab-node-021-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-021-dimension-reduction-7-1.png" alt="plot of chunk tab-node-021-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-021-collect-classes](figure_cola/node-021-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### Node03


Parent node: [Node0](#Node0).
Child nodes: 
                Node011-leaf
        ,
                Node012-leaf
        ,
                Node013-leaf
        ,
                [Node021](#Node021)
        ,
                Node022-leaf
        ,
                Node023-leaf
        ,
                Node031-leaf
        ,
                Node032-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["03"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 16 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-03-collect-plots](figure_cola/node-03-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-03-select-partition-number](figure_cola/node-03-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4589 0.542   0.542
#> 3 3 0.608           0.376       0.831         0.3489 0.917   0.846
#> 4 4 0.675           0.578       0.756         0.1467 0.800   0.586
#> 5 5 0.650           0.743       0.772         0.0974 0.892   0.649
#> 6 6 0.708           0.743       0.833         0.0477 0.950   0.750
#> 7 7 0.800           0.741       0.863         0.0537 1.000   1.000
#> 8 8 0.875           0.584       0.833         0.0365 0.967   0.778
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-03-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-03-get-classes'>
<ul>
<li><a href='#tab-node-03-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-03-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-03-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-03-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-03-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-03-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-03-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-03-get-classes-1'>
<p><a id='tab-node-03-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1 p2
#&gt; TCGA.YZ.A980.01     1       0          1  1  0
#&gt; TCGA.WC.AA9A.01     1       0          1  1  0
#&gt; TCGA.VD.AA8T.01     2       0          1  0  1
#&gt; TCGA.V4.A9E8.01     1       0          1  1  0
#&gt; TCGA.VD.A8KL.01     2       0          1  0  1
#&gt; TCGA.V4.A9EO.01     1       0          1  1  0
#&gt; TCGA.V4.A9ED.01     1       0          1  1  0
#&gt; TCGA.V4.A9ES.01     1       0          1  1  0
#&gt; TCGA.YZ.A985.01     2       0          1  0  1
#&gt; TCGA.VD.A8KN.01     1       0          1  1  0
#&gt; TCGA.VD.A8KK.01     1       0          1  1  0
#&gt; TCGA.WC.A888.01     1       0          1  1  0
#&gt; TCGA.V4.A9F8.01     1       0          1  1  0
#&gt; TCGA.YZ.A984.01     2       0          1  0  1
#&gt; TCGA.VD.AA8P.01     2       0          1  0  1
#&gt; TCGA.VD.A8KF.01     1       0          1  1  0
</code></pre>

<script>
$('#tab-node-03-get-classes-1-a').parent().next().next().hide();
$('#tab-node-03-get-classes-1-a').click(function(){
  $('#tab-node-03-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-03-get-classes-2'>
<p><a id='tab-node-03-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3
#&gt; TCGA.YZ.A980.01     1   0.619     -0.717 0.58 0.00 0.42
#&gt; TCGA.WC.AA9A.01     1   0.619     -0.717 0.58 0.00 0.42
#&gt; TCGA.VD.AA8T.01     2   0.429      0.897 0.00 0.82 0.18
#&gt; TCGA.V4.A9E8.01     1   0.556      0.379 0.70 0.00 0.30
#&gt; TCGA.VD.A8KL.01     2   0.000      0.933 0.00 1.00 0.00
#&gt; TCGA.V4.A9EO.01     1   0.000      0.564 1.00 0.00 0.00
#&gt; TCGA.V4.A9ED.01     1   0.000      0.564 1.00 0.00 0.00
#&gt; TCGA.V4.A9ES.01     3   0.630      0.000 0.48 0.00 0.52
#&gt; TCGA.YZ.A985.01     2   0.000      0.933 0.00 1.00 0.00
#&gt; TCGA.VD.A8KN.01     1   0.556      0.379 0.70 0.00 0.30
#&gt; TCGA.VD.A8KK.01     1   0.000      0.564 1.00 0.00 0.00
#&gt; TCGA.WC.A888.01     1   0.000      0.564 1.00 0.00 0.00
#&gt; TCGA.V4.A9F8.01     1   0.000      0.564 1.00 0.00 0.00
#&gt; TCGA.YZ.A984.01     2   0.000      0.933 0.00 1.00 0.00
#&gt; TCGA.VD.AA8P.01     2   0.429      0.897 0.00 0.82 0.18
#&gt; TCGA.VD.A8KF.01     1   0.619     -0.717 0.58 0.00 0.42
</code></pre>

<script>
$('#tab-node-03-get-classes-2-a').parent().next().next().hide();
$('#tab-node-03-get-classes-2-a').click(function(){
  $('#tab-node-03-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-03-get-classes-3'>
<p><a id='tab-node-03-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4
#&gt; TCGA.YZ.A980.01     4  0.4790     0.0153 0.38 0.00 0.00 0.62
#&gt; TCGA.WC.AA9A.01     4  0.2011     0.6075 0.08 0.00 0.00 0.92
#&gt; TCGA.VD.AA8T.01     2  0.0707     0.8273 0.00 0.98 0.00 0.02
#&gt; TCGA.V4.A9E8.01     1  0.4406     0.2514 0.70 0.00 0.30 0.00
#&gt; TCGA.VD.A8KL.01     2  0.4939     0.8789 0.00 0.74 0.22 0.04
#&gt; TCGA.V4.A9EO.01     1  0.4406     0.6050 0.70 0.00 0.00 0.30
#&gt; TCGA.V4.A9ED.01     1  0.4406     0.6050 0.70 0.00 0.00 0.30
#&gt; TCGA.V4.A9ES.01     4  0.6299     0.3751 0.06 0.00 0.42 0.52
#&gt; TCGA.YZ.A985.01     2  0.4134     0.8827 0.00 0.74 0.26 0.00
#&gt; TCGA.VD.A8KN.01     1  0.4406     0.2514 0.70 0.00 0.30 0.00
#&gt; TCGA.VD.A8KK.01     1  0.4406     0.6050 0.70 0.00 0.00 0.30
#&gt; TCGA.WC.A888.01     1  0.4855     0.4624 0.60 0.00 0.00 0.40
#&gt; TCGA.V4.A9F8.01     1  0.4624     0.5660 0.66 0.00 0.00 0.34
#&gt; TCGA.YZ.A984.01     2  0.4134     0.8827 0.00 0.74 0.26 0.00
#&gt; TCGA.VD.AA8P.01     2  0.0707     0.8273 0.00 0.98 0.02 0.00
#&gt; TCGA.VD.A8KF.01     4  0.2011     0.6075 0.08 0.00 0.00 0.92
</code></pre>

<script>
$('#tab-node-03-get-classes-3-a').parent().next().next().hide();
$('#tab-node-03-get-classes-3-a').click(function(){
  $('#tab-node-03-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-03-get-classes-4'>
<p><a id='tab-node-03-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5
#&gt; TCGA.YZ.A980.01     4  0.3983      0.633 0.34 0.00 0.00 0.66 0.00
#&gt; TCGA.WC.AA9A.01     4  0.2732      0.791 0.16 0.00 0.00 0.84 0.00
#&gt; TCGA.VD.AA8T.01     2  0.6813      0.569 0.00 0.46 0.36 0.02 0.16
#&gt; TCGA.V4.A9E8.01     5  0.3424      0.985 0.24 0.00 0.00 0.00 0.76
#&gt; TCGA.VD.A8KL.01     2  0.2797      0.690 0.00 0.88 0.00 0.06 0.06
#&gt; TCGA.V4.A9EO.01     1  0.0609      0.908 0.98 0.00 0.02 0.00 0.00
#&gt; TCGA.V4.A9ED.01     1  0.0000      0.919 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ES.01     3  0.5607      0.000 0.08 0.00 0.54 0.38 0.00
#&gt; TCGA.YZ.A985.01     2  0.0609      0.706 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.VD.A8KN.01     5  0.3999      0.985 0.24 0.00 0.02 0.00 0.74
#&gt; TCGA.VD.A8KK.01     1  0.0000      0.919 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A888.01     1  0.2280      0.832 0.88 0.00 0.00 0.12 0.00
#&gt; TCGA.V4.A9F8.01     1  0.1732      0.882 0.92 0.00 0.00 0.08 0.00
#&gt; TCGA.YZ.A984.01     2  0.0000      0.707 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8P.01     2  0.6064      0.569 0.00 0.46 0.42 0.00 0.12
#&gt; TCGA.VD.A8KF.01     4  0.2732      0.791 0.16 0.00 0.00 0.84 0.00
</code></pre>

<script>
$('#tab-node-03-get-classes-4-a').parent().next().next().hide();
$('#tab-node-03-get-classes-4-a').click(function(){
  $('#tab-node-03-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-03-get-classes-5'>
<p><a id='tab-node-03-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.YZ.A980.01     4  0.5235      0.419 0.38 0.00 0.00 0.52 0.00 0.10
#&gt; TCGA.WC.AA9A.01     4  0.2260      0.677 0.14 0.00 0.00 0.86 0.00 0.00
#&gt; TCGA.VD.AA8T.01     6  0.3321      0.915 0.00 0.10 0.08 0.00 0.00 0.82
#&gt; TCGA.V4.A9E8.01     5  0.4221      0.868 0.04 0.08 0.06 0.02 0.80 0.00
#&gt; TCGA.VD.A8KL.01     2  0.7034      0.658 0.00 0.52 0.12 0.12 0.02 0.22
#&gt; TCGA.V4.A9EO.01     1  0.2790      0.785 0.84 0.14 0.02 0.00 0.00 0.00
#&gt; TCGA.V4.A9ED.01     1  0.0000      0.903 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9ES.01     3  0.4503      0.000 0.08 0.00 0.68 0.24 0.00 0.00
#&gt; TCGA.YZ.A985.01     2  0.4334      0.804 0.00 0.72 0.04 0.00 0.02 0.22
#&gt; TCGA.VD.A8KN.01     5  0.0937      0.868 0.04 0.00 0.00 0.00 0.96 0.00
#&gt; TCGA.VD.A8KK.01     1  0.0000      0.903 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.WC.A888.01     1  0.2728      0.796 0.86 0.00 0.00 0.04 0.00 0.10
#&gt; TCGA.V4.A9F8.01     1  0.0547      0.897 0.98 0.00 0.00 0.02 0.00 0.00
#&gt; TCGA.YZ.A984.01     2  0.2941      0.810 0.00 0.78 0.00 0.00 0.00 0.22
#&gt; TCGA.VD.AA8P.01     6  0.1814      0.915 0.00 0.10 0.00 0.00 0.00 0.90
#&gt; TCGA.VD.A8KF.01     4  0.2260      0.677 0.14 0.00 0.00 0.86 0.00 0.00
</code></pre>

<script>
$('#tab-node-03-get-classes-5-a').parent().next().next().hide();
$('#tab-node-03-get-classes-5-a').click(function(){
  $('#tab-node-03-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-03-get-classes-6'>
<p><a id='tab-node-03-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4  p5   p6   p7
#&gt; TCGA.YZ.A980.01     4  0.5229      0.640 0.18 0.00 0.00 0.64 0.0 0.06 0.12
#&gt; TCGA.WC.AA9A.01     4  0.1166      0.825 0.00 0.00 0.00 0.94 0.0 0.00 0.06
#&gt; TCGA.VD.AA8T.01     6  0.2259      0.898 0.00 0.16 0.00 0.00 0.0 0.84 0.00
#&gt; TCGA.V4.A9E8.01     5  0.0000      0.732 0.00 0.00 0.00 0.00 1.0 0.00 0.00
#&gt; TCGA.VD.A8KL.01     2  0.3047      0.698 0.28 0.72 0.00 0.00 0.0 0.00 0.00
#&gt; TCGA.V4.A9EO.01     7  0.3047      0.663 0.28 0.00 0.00 0.00 0.0 0.00 0.72
#&gt; TCGA.V4.A9ED.01     7  0.0000      0.856 0.00 0.00 0.00 0.00 0.0 0.00 1.00
#&gt; TCGA.V4.A9ES.01     3  0.1664      0.000 0.00 0.00 0.92 0.06 0.0 0.00 0.02
#&gt; TCGA.YZ.A985.01     2  0.0504      0.838 0.02 0.98 0.00 0.00 0.0 0.00 0.00
#&gt; TCGA.VD.A8KN.01     5  0.4569      0.732 0.18 0.00 0.04 0.00 0.7 0.08 0.00
#&gt; TCGA.VD.A8KK.01     7  0.0000      0.856 0.00 0.00 0.00 0.00 0.0 0.00 1.00
#&gt; TCGA.WC.A888.01     7  0.3770      0.699 0.18 0.00 0.00 0.00 0.0 0.08 0.74
#&gt; TCGA.V4.A9F8.01     7  0.0863      0.848 0.04 0.00 0.00 0.00 0.0 0.00 0.96
#&gt; TCGA.YZ.A984.01     2  0.0504      0.843 0.00 0.98 0.00 0.02 0.0 0.00 0.00
#&gt; TCGA.VD.AA8P.01     6  0.4707      0.898 0.04 0.16 0.04 0.04 0.0 0.72 0.00
#&gt; TCGA.VD.A8KF.01     4  0.1166      0.825 0.00 0.00 0.00 0.94 0.0 0.00 0.06
</code></pre>

<script>
$('#tab-node-03-get-classes-6-a').parent().next().next().hide();
$('#tab-node-03-get-classes-6-a').click(function(){
  $('#tab-node-03-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-03-get-classes-7'>
<p><a id='tab-node-03-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7   p8
#&gt; TCGA.YZ.A980.01     4  0.5183      0.437 0.00 0.00 0.34 0.52 0.00 0.00 0.06 0.08
#&gt; TCGA.WC.AA9A.01     4  0.0000      0.707 0.00 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8T.01     6  0.4937      0.752 0.08 0.18 0.00 0.00 0.00 0.64 0.00 0.10
#&gt; TCGA.V4.A9E8.01     5  0.0000      0.770 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.VD.A8KL.01     1  0.3237      0.594 0.60 0.40 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.V4.A9EO.01     8  0.3318      0.000 0.00 0.00 0.00 0.00 0.00 0.00 0.46 0.54
#&gt; TCGA.V4.A9ED.01     7  0.0000      0.711 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.V4.A9ES.01     3  0.3808      0.000 0.00 0.34 0.62 0.04 0.00 0.00 0.00 0.00
#&gt; TCGA.YZ.A985.01     1  0.2071      0.768 0.90 0.02 0.04 0.00 0.00 0.00 0.00 0.04
#&gt; TCGA.VD.A8KN.01     5  0.4019      0.770 0.00 0.06 0.00 0.00 0.74 0.06 0.00 0.14
#&gt; TCGA.VD.A8KK.01     7  0.0000      0.711 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.WC.A888.01     7  0.4480      0.187 0.00 0.00 0.30 0.00 0.00 0.00 0.58 0.12
#&gt; TCGA.V4.A9F8.01     7  0.0471      0.701 0.00 0.00 0.00 0.00 0.00 0.02 0.98 0.00
#&gt; TCGA.YZ.A984.01     1  0.0000      0.773 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.VD.AA8P.01     6  0.1341      0.752 0.08 0.00 0.00 0.00 0.00 0.92 0.00 0.00
#&gt; TCGA.VD.A8KF.01     4  0.1091      0.707 0.00 0.00 0.00 0.94 0.00 0.00 0.00 0.06
</code></pre>

<script>
$('#tab-node-03-get-classes-7-a').parent().next().next().hide();
$('#tab-node-03-get-classes-7-a').click(function(){
  $('#tab-node-03-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-03-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-03-consensus-heatmap'>
<ul>
<li><a href='#tab-node-03-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-03-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-03-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-03-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-03-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-03-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-03-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-03-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-03-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-03-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-03-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-03-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-03-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-03-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-03-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-03-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-03-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-03-membership-heatmap'>
<ul>
<li><a href='#tab-node-03-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-03-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-03-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-03-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-03-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-03-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-03-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-03-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-1-1.png" alt="plot of chunk tab-node-03-membership-heatmap-1"/></p>

</div>
<div id='tab-node-03-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-2-1.png" alt="plot of chunk tab-node-03-membership-heatmap-2"/></p>

</div>
<div id='tab-node-03-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-3-1.png" alt="plot of chunk tab-node-03-membership-heatmap-3"/></p>

</div>
<div id='tab-node-03-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-4-1.png" alt="plot of chunk tab-node-03-membership-heatmap-4"/></p>

</div>
<div id='tab-node-03-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-5-1.png" alt="plot of chunk tab-node-03-membership-heatmap-5"/></p>

</div>
<div id='tab-node-03-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-6-1.png" alt="plot of chunk tab-node-03-membership-heatmap-6"/></p>

</div>
<div id='tab-node-03-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-03-membership-heatmap-7-1.png" alt="plot of chunk tab-node-03-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-03-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-03-get-signatures'>
<ul>
<li><a href='#tab-node-03-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-03-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-03-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-03-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-03-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-03-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-03-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-03-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-1-1.png" alt="plot of chunk tab-node-03-get-signatures-1"/></p>

</div>
<div id='tab-node-03-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-2-1.png" alt="plot of chunk tab-node-03-get-signatures-2"/></p>

</div>
<div id='tab-node-03-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-3-1.png" alt="plot of chunk tab-node-03-get-signatures-3"/></p>

</div>
<div id='tab-node-03-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-4-1.png" alt="plot of chunk tab-node-03-get-signatures-4"/></p>

</div>
<div id='tab-node-03-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-5-1.png" alt="plot of chunk tab-node-03-get-signatures-5"/></p>

</div>
<div id='tab-node-03-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-6-1.png" alt="plot of chunk tab-node-03-get-signatures-6"/></p>

</div>
<div id='tab-node-03-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-03-get-signatures-7-1.png" alt="plot of chunk tab-node-03-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-03-signature_compare](figure_cola/node-03-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-03-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-03-dimension-reduction'>
<ul>
<li><a href='#tab-node-03-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-03-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-03-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-03-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-03-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-03-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-03-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-03-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-1-1.png" alt="plot of chunk tab-node-03-dimension-reduction-1"/></p>

</div>
<div id='tab-node-03-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-2-1.png" alt="plot of chunk tab-node-03-dimension-reduction-2"/></p>

</div>
<div id='tab-node-03-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-3-1.png" alt="plot of chunk tab-node-03-dimension-reduction-3"/></p>

</div>
<div id='tab-node-03-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-4-1.png" alt="plot of chunk tab-node-03-dimension-reduction-4"/></p>

</div>
<div id='tab-node-03-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-5-1.png" alt="plot of chunk tab-node-03-dimension-reduction-5"/></p>

</div>
<div id='tab-node-03-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-6-1.png" alt="plot of chunk tab-node-03-dimension-reduction-6"/></p>

</div>
<div id='tab-node-03-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-03-dimension-reduction-7-1.png" alt="plot of chunk tab-node-03-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-03-collect-classes](figure_cola/node-03-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 4.1.0 (2021-05-18)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS/LAPACK: /usr/lib64/libopenblas-r0.3.3.so
#> 
#> locale:
#>  [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C               LC_TIME=en_US.UTF-8       
#>  [4] LC_COLLATE=en_US.UTF-8     LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
#>  [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.74.0    ComplexHeatmap_2.8.0 markdown_1.1         knitr_1.33          
#> [5] matrixStats_0.59.0   cola_1.9.4          
#> 
#> loaded via a namespace (and not attached):
#>   [1] bitops_1.0-7           bit64_4.0.5            doParallel_1.0.16      RColorBrewer_1.1-2    
#>   [5] httr_1.4.2             GenomeInfoDb_1.28.1    data.tree_1.0.0        tools_4.1.0           
#>   [9] utf8_1.2.1             R6_2.5.0               irlba_2.3.3            DBI_1.1.1             
#>  [13] BiocGenerics_0.38.0    colorspace_2.0-2       GetoptLong_1.0.5       gridExtra_2.3         
#>  [17] tidyselect_1.1.1       bit_4.0.4              compiler_4.1.0         Biobase_2.52.0        
#>  [21] Cairo_1.5-12.2         xml2_1.3.2             microbenchmark_1.4-7   slam_0.1-48           
#>  [25] scales_1.1.1           askpass_1.1            stringr_1.4.0          digest_0.6.27         
#>  [29] XVector_0.32.0         pkgconfig_2.0.3        umap_0.2.7.0           fastmap_1.1.0         
#>  [33] highr_0.9              rlang_0.4.11           GlobalOptions_0.1.2    rstudioapi_0.13       
#>  [37] RSQLite_2.2.7          impute_1.66.0          generics_0.1.0         shape_1.4.6           
#>  [41] jsonlite_1.7.2         mclust_5.4.7           dplyr_1.0.7            dendextend_1.15.1     
#>  [45] RCurl_1.98-1.3         magrittr_2.0.1         GenomeInfoDbData_1.2.6 Matrix_1.3-4          
#>  [49] fansi_0.5.0            Rcpp_1.0.7             munsell_0.5.0          S4Vectors_0.30.0      
#>  [53] viridis_0.6.1          reticulate_1.20        lifecycle_1.0.0        scatterplot3d_0.3-41  
#>  [57] stringi_1.7.3          zlibbioc_1.38.0        blob_1.2.1             parallel_4.1.0        
#>  [61] crayon_1.4.1           lattice_0.20-44        Biostrings_2.60.1      splines_4.1.0         
#>  [65] annotate_1.70.0        circlize_0.4.13        KEGGREST_1.32.0        polylabelr_0.2.0      
#>  [69] pillar_1.6.1           rjson_0.2.20           codetools_0.2-18       stats4_4.1.0          
#>  [73] XML_3.99-0.6           glue_1.4.2             evaluate_0.14          png_0.1-7             
#>  [77] vctrs_0.3.8            foreach_1.5.1          polyclip_1.10-0        purrr_0.3.4           
#>  [81] gtable_0.3.0           openssl_1.4.4          assertthat_0.2.1       clue_0.3-59           
#>  [85] cachem_1.0.5           ggplot2_3.3.5          xfun_0.24              eulerr_6.1.0          
#>  [89] xtable_1.8-4           skmeans_0.2-13         RSpectra_0.16-0        viridisLite_0.4.0     
#>  [93] survival_3.2-11        tibble_3.1.2           Polychrome_1.3.1       iterators_1.0.13      
#>  [97] AnnotationDbi_1.54.1   memoise_2.0.0          IRanges_2.26.0         cluster_2.1.2         
#> [101] ellipsis_0.3.2         brew_1.0-6
```




