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

### Browsing the documentation

The [vignette on Bioconductor](https://bioconductor.org/packages/release/bioc/vignettes/BridgeDbR/inst/doc/tutorial.pdf)
was a short walkthrough how to use the R package.

For metabolites, the following code examples are useful. TODO...

# Pathway Analysis

Pathway analysis tries to find pathways where the more interesting biology is changed.

## WikiPathways

WikiPathways (see [this Scholia page](https://tools.wmflabs.org/scholia/topic/Q7999828) and
this [feedback with use cases](http://wikipathways.tumblr.com/)) is a community project to develop an
Open knowledge database of biological pathways. Over the years many communities have collaborated
via the website's **portals**. There is a colorful [academy](https://wikipathways.github.io/academy/path.html)
where you can learn about the ins and outs of WikiPathways.

## PathVisio

PathVisio is one of the tools that can be used to explore pathways, map experimental data onto
pathways, and do pathway enrichment (see doi:).

