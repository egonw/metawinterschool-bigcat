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



# Pathway Analysis

## WikiPathways



## PathVisio


