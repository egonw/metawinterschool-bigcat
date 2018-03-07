# metawinterschool-bigcat
#metawinterschool contribution by BiGCaT

This workshop consists of a part about identifier mapping (BridgeDb) and pathway analysis (WikiPathways and PathVisio).

# Identifier Mapping

## BridgeDb

[BridgeDb](https://www.bridgedb.org/) is a project, an application programming interface (API),
a Java library, a webservice, a collection of identifier mapping database, and more (see doi:[10.1186/1471-2105-11-5](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-11-5)).

In this practical you will use BridgeDb to modify identifier mappings. However, using the R package does require you
to have a working [rJava](https://cran.r-project.org/web/packages/rJava/index.html) package, which sometimes is hard
to get working.

### Installation

First, install the [BridgeDbR](https://bioconductor.org/packages/release/bioc/html/BridgeDbR.html) package. This can
be done with Bioconductor:

```(R)
source("https://bioconductor.org/biocLite.R")
biocLite("BridgeDbR")
```

Alternatively, install the package directly from GitHub:

```(R)
install.packages("rJava") # if not present already
install.packages("RCurl") # if not present already
install.packages("devtools") # if not present already
library(devtools)
install_github("bridgedb/BridgeDbR")
```

### Identifier mapping data

Besides a toolkit that can do identifier mapping, we actually still need the data that does the identifier
mapping. The latest metabolite ID mapping database can be
[downloaded from Figshare](https://figshare.com/articles/Metabolite_BridgeDb_ID_Mapping_Database_20180201_/5845134).

### Browsing the documentation

The [vignette on Bioconductor](https://bioconductor.org/packages/release/bioc/vignettes/BridgeDbR/inst/doc/tutorial.pdf)
was a short walkthrough how to use the R package.

### Mapping identifiers

This identifier database can then be loaded into R with (it assumes the file is located in the current working folder):

```(R)
mbmaps = loadDatabase("metabolites_20180201.bridge")
```

With the mappin data loaded, a single metabolite identifier
([CHEBI:55](http://www.ebi.ac.uk/chebi/searchId.do?chebiId=CHEBI:55))
can be mapped to other identifiers with the following code:

```(R)
map(mbmaps, "Ce", "CHEBI:55")
```

If you have a data matrix (like [this one](https://github.com/egonw/metawinterschool-bigcat/blob/master/macs_glucose_challenge.tsv)),
then a helper function can be helpful, for example, to handle multiple mapped identifiers:

```(R)
helper = function(x) {
  mappings = map(mbmaps, "Ch", x, "Wd")
  if (length(mappings) == 1) {
    result = mappings
  } else {
    result = mappings[1]
  }
  return(result)
}
```

This function takes a HMDB identifier and returns the corresponding [Wikidata](http://wikidata.org/) identifier.

You can load that aforementioned data file with:

```(R)
data <- read.table("macs_glucose_challenge.tsv", sep='\t', header=TRUE)
```

The seccond column has the HMDB identifiers:

```(R)
data[,2]
```

We can convert all these identifiers with our helper function and the **sapply** function (and some R magic):

```(R)
wikidata = unlist(sapply(as.character(data[,2]), helper))
data2 = cbind(c(wikidata,""),data)
```

You can verify that everything went fine with for example:

```(R)
data2[1:4,1:5] 
map(mbmaps, "Wd", "Q27075135", "Ch")
```

# Pathway Analysis

Pathway analysis tries to find pathways where the more interesting biology is changed.

## WikiPathways

[WikiPathways](http://wikipathways.org/) (see [this Scholia page](https://tools.wmflabs.org/scholia/topic/Q7999828) and
this [feedback with use cases](http://wikipathways.tumblr.com/)) is a community project to develop an
Open knowledge database of biological pathways. Over the years many communities have collaborated
via the website's **portals**. There is a colorful [academy](https://wikipathways.github.io/academy/path.html)
where you can learn about the ins and outs of WikiPathways.

## PathVisio

PathVisio is one of the tools that can be used to explore pathways, map experimental data onto
pathways, and do pathway enrichment (see doi:[10.1371/journal.pcbi.1004085](https://doi.org/10.1371/journal.pcbi.1004085)).

