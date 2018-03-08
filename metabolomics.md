# Metabolomics

## Step 1: Preparation

Download the following files:

* Metabolite database [metabolites_20180201.bridge](https://figshare.com/articles/Metabolite_BridgeDb_ID_Mapping_Database_20180201_/5845134) (same as with the BridgeDbR part)
* The [glucose_challenge.gpml](https://github.com/egonw/metawinterschool-bigcat/blob/master/glucose_challenge.gpml) GPML file (Save the file with the Raw button)
* An experimental dataset named [macs_glucose_challenge.tsv](https://github.com/egonw/metawinterschool-bigcat/blob/master/macs_glucose_challenge.tsv) (Save the file with the Raw button)

Furthermore, you need Java installed on your computer.

## Step 2: Launch PathVisio
Start [PathVisio](http://pathvisio.org/) by going to the [Download](https://www.pathvisio.org/downloads/)
page and clicking the download link (Binary installation). When asked to open or save the file, select open. After this step, when prompted to save a shortcut to your desktop, select cancel.

## Step 3: Data import
The data is in the file *macs_glucose_challenge.tsv*. This is a file in tab-delimited text format. You can preview the data by opening it in a spreadsheet (Excel, OpenOffice, etc).

1. While the file is open in a spreadsheet, you can examine the dataset. In this file metabolites are identified with a HMDB identifier. PathVisio can understand many different metabolite identifiers, a.o. CAS, HMDB, PubChem (CID), ChEBI and KEGG Compounds.
2. Switch back to PathVisio. Select *Data > Import expression data*.
3. For the input file, select *macs_glucose_challenge.tsv*.
4. Leave the output file as it is.
5. Make sure the gene database is set to *metabolites_20180201.bridge* (if not loaded already). Click Next.
6. Make sure the data delimiter is set to "tab". Click Next.
7. Make sure the primary identifier column is set to "Column B".
8. Make sure the Use the same **system code** for all rows radio button is selected.
9. Make sure the system code is set to "HMDB".
10. Right-click on the header of the third row and select *First data row* from the menu. This is to ensure that the first two rows are treated as header. The first two rows will be shaded yellow, to indicate that they will be used as header. Click Next. It may take a few minutes for the data to import.

When the import is finished, you should see a message like this:

```
97 rows of data were imported successfully
```

You may see a small set of exception; these exceptions are caused by metabolite identifiers that
are not recognized by BridgeDb. The BridgeDb metabolite database is based on HMDB, ChEBI, and Wikidata.
Usually this means that the metabolite can not be found in these database. However, if you add these identifiers
to Wikidata, then the next monthly WikiPathways release will support it.

When the *Finish* button becomes clickable, click it. A file named **macs_glucose_challenge.pgex** has now been created, this stores all experimental data.

## Step 4: Create a color set

1. Go to *File > Open* and select the file *glucose_challenge.gpml* that you've downloaded at the beginning of the tutorial.
2. Go to *Data > Visualization* options. A dialog window pops up.
3. Enable the check box Text Label. A small panel shows up, but you don't need to change anything there.
4. Enable the check box *Expression as Color*. A panel shows up.
5. Mark the check box for **log2_avg_30**, **log2_avg_60**, **log2_avg_90** and **log2_avg_120**.
6. Create a new color set by clicking the tool icon in the bottom right and selecting "New"
7. In the new dialog, select the Gradient check box.
8. Select the red-yellow-green gradient.
9. Make sure the values range from -1.0 to 0 to 1.0.
10. Now the gene boxes on the pathway should have changed color based on their expression values. For example low measurements are green, high measurements are red, and unchanged measurements are yellow (This depends on the exact color options you selected).

Open other pathways. Which pathway has changed the most?

## Step 5: Search for regulated pathways

Pathway enrichment analysis is best done against a large collection of pathways. You can download the collection
of [human pathways aimed at data analysis](https://www.pathvisio.org/downloads/download-pathways/). Unzip the
downloaded archive and remember the location (you need it in step 3).

The enrichment is then performed with the following steps:

1. Go to *Data > Statistics*.
2. In the *Expression* field, enter out the following:
   ```
   [Ttest_30vs120] < 0.05
   ```
3. In the Pathway directory field, select the pathway directory that comes with the tutorial files you downloaded in the beginning.
4. Press Calculate.

After the calculations have finished, you now get a list of pathways, ordered by how many genes that have a ttest of < 0.05 (i.e have a significant test for difference between timepoints 30 and 120 with a confidence level of 0.05)

In the result table you see the values for r, the number of genes that meet your criterion, and n, the total number of genes in the Pathway. From these values a percentage and a z-score are calculated. Note how the Z-score and percentages are related for different pathways.

---
Copyright (C) 2009 Kristina Hanspers, [source](http://developers.pathvisio.org/wiki/MetabolomicsTutorial).

