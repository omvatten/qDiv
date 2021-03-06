Plotting
********

Heatmap
#######

.. code-block:: python

   plot.heatmap(obj, xAxis='None', levels=['Phylum', 'Genus'], levelsShown='None', subsetLevels='None', subsetPatterns='None', order='None', numberToPlot=20, method='max_sample', merge=False, figsize=(14, 10), fontsize=15, sepCol = [], labels=True, labelsize=10, cThreshold=8, cMap='Reds', cLinear=0.5, cBar=[], savename='None')

Plots a heatmap showing the relative abundance of different taxa in different samples.

*obj* is the object. 

*xAxis* specifies heading in meta data used to merge samples and use a labels on x-axis; levels specifies the taxonomic levels to be displayed on the y-axis.

*levels* specifies the taxonomic levels shown on the y-axis. It should be list with one or two taxonomic levels.

if *levelsShown* ='Number', there will be a list of numbers on the y-axis instead of taxonomic names.

*subsetLevels* and *subsetPatterns* refers to text patterns which can be used to filter the results for specific taxa.
If these arguments are used, the inputs should be a list of taxanomic levels to search within and a list of text patterns to search for (see also subset.text_patterns() function).

*order* refers to heading of meta data column used to order samples. The column should contain numbers.
The sample with the smallest number will be placed to the left in the heatmap.

*numberToPlot* refers to the number of taxa with highest abundance to include in the heatmap. 

*method* refers to the method used to define the taxa with highest abundance: 

- 'max_sample' uses the maximum relative abundance in a sample
- 'mean_all' uses the mean relative abundance across all samples to rank the taxa

if *merge* =True, unclassified sequences will be merged. If False (default), they will be kept separate and identified with sequence id found in the count table.

*figsize* is the width and height of the figure in inches

*fontsize* refers to the axis text font size

*sepCol* is a list of column numbers between which to include a separator, i.e. to clarify grouping of samples 

*labels* =True means that relative abundance values are shown in the plot. 

*labelsize* is the font size of the relative abundance labels.

*cThreshold* is the percentage relative abundance threshold at which the label color switches from black to white (for clarity). 

*cMap* is the color map used in the heatmap.

*cLinear* is a parameter determining how the color intensity changes with relative abundance. A value of 1 means the change is linear.

*cBar* is a list of tick marks to use if a color bar is included as legend. The tick marks indicate relative abundance percentage levels to include in the legend. 

*savename* is the name (also include path) of the saved png file. If 'None', no figure is saved.

Alpha diversity
###############

.. code-block:: python

   plot.alpha_diversity(obj, distmat='None', var='None', slist='None', order='None', ylog=False, figsize=(10, 6), fontsize=18, colorlist='None', savename='None')

Visualizes how alpha diversity depends on diversity order.

*obj* is the object. 

If *distmat* is specified, the diversity.phyl_alpha function is used, otherwise diversity.naive_alpha is used. A *distmat* dataframe can be generated with the diversity.sequence_comparison() function.

*var* refers to column heading in meta data used to color code samples; *slist* is a list of samples from the var column to include (default is to include all).

*order* refers to column heading in meta data used to order the samples. 

If *ylog* =True, the y-axis of the plot will be logarithmic.

*figsize* is the width and height of the figure in inches

*fontsize* refers to the axis text font size

*colorlist* is a list of colors used for the lines in the plot, if colorlist=’None’, qdiv will decide the colors. 

*savename* is the name (also include path) of the saved png file, if 'None' no figure is saved.

PCoA
####

.. code-block:: python

   plot.pcoa(dist, meta='None', var1='None', var2='None', var1_title='', var2_title='', biplot=[], arrow_width=0.001, whitePad=1.1, var2pos=0.4, tag='None', order='None', title='', connectPoints='None', figsize=(9, 6), fontsize=12, markersize=50, markerscale=1.1, lw=1, hideAxisValues=False, showLegend=True, ellipse='None', n_std=2, ellipse_tag='None', ellipse_connect='None', flipx=False, flipy=False, returnData=False, colorlist='None', markerlist='None', savename='None')

Visualizes dissimilarities between samples in principal coordinate analysis plot.

*dist* is a distance matrix with pairwise dissimilarities. This can be generated using the beta diversity functions, i.e. naive_beta, phyl_beta, jaccard, bray.

*meta* is the meta data, typically object['meta'].

*var1* is a column heading in the meta used to color code.

*var2* is a column heading in the meta used to code by marker type.

*var1_title* and *var_2 title* are the titles used in the legend.

*biplot* is a list of columns in meta data containing numeric data that should be plotted as a biplot in the PCoA. The arrows associated with each column are scaled to the plot area of the PCoA.

*arrow_width* is the width of the arrows used in the biplot.

*whitePad* sets the space between the outermost points and the plot limits (1.0=no space).

*var2pos* is the vertical position of the var2 legend.

*tag* is meta data column used to add labels to each point in figure

*order* is meta data column used to order samples (should be numbers)

*title* is the title of the entire figure.

*connectPoints* is a meta data column with numbers. If specified, the sample points in the PCoA will be connected by lines in the order determined by the numbers in the column.

*figsize* is the figure size in inches (width, height).

*markersize* is the size of the markers in the figure.

*markerscale* sets the size of the markers in the legend

*lw* is linewidth of lines in the plot

if *hideAxisValues=True* no numbers are shown on the axes

if *showLegend=False* the legend is removed

*ellipse* is metadata column with categories of samples that should be grouped with confidence ellipses

*n_std* is the number of standard deviations of the confidence ellipses

*ellipse_tag* is metadata column with labels for each ellipse

*ellipse_connect* is metadata column with numbers used to connect centers of ellipses with lines.

if *flipx* =True, the x-axis will be inverted

if *flipy* =True, the y-axis will be inverted

if *returnData* =True, the coordinate of the points will be returned as a pandas dataframe. Note that if it is a biplot, two dataframes will be returned: one for the points and one for the arrows.

*colorlist* specifies colorlist to use for var1. If 'None', qdiv will decide the colors. same for markerlist and var2; savename is path and name to save png figure output.

*markerlist* specifies markers to use for var2. If 'None', qdiv will decide the markers. 

*savename* is path and name to save png and pdf figures.

Pairwise dissimilarity
######################

.. code-block:: python

   plot.pairwise_beta(obj, divType='naive', distmat='None', compareVar='None', spairs=[], nullModel=True, randomization='abundance', weight=0, iterations=10, qrange=[0, 2, 0.5], colorlist='None', onlyPlotData='None', skipJB=False, onlyReturnData=False, savename='None')

Calculate and/or plots dissimilarity between pairs of samples or sample types.

*obj* is the object. 

*divType* is the type of beta diversity to calculate: 'naive', 'phyl', or 'func'.

*distmat* is distance matrix file that must be provided if divType='func'. A *distmat* dataframe can be generated with the stats.sequence_comparison() function.

*compareVar* is a column heading in the meta data. If compareVar is not None, the dissimilarity values represent all pairwise comparisons 
between the meta data categories specified present under compareVar. 

*spairs* is a list of pairs to compare, each item in the list is another list of two samples names or categories to compare, e.g. [[sample_group_1, sample_group_2],[sample_group_X, sample_group_Y],[sample_group_3, sample_group_4]]. 

if *nullModel* =True, the null.rcq function will be run. *randomization,* *weight,* and *iterations* are all input to the null.rcq function (see documentation there).

*qrange* is a list containing the min, max, tick mark space on the diversity order x-axis of the figure.

*colorlist* is a list of colors used for the lines, if *colorlist* =’None’, qdiv will decide the colors.

If *onlyPlotData* is a dictionary containing data, the function will only plot the data in that dictionary and no further calculations with be carried out.

If *skipJB* =True, Jaccard and Bray-Curtis dissimilarities will not be calculated. 

If *onlyReturnData* =True, no plots will be done and only a python dictionary containing the output data will be generated. This dictionary can later be used as input to the onlyPlotData argument. 

*savename* is path and name to the generated output. The data in the python dictionary is saved as a pickle file.

Rarefaction curve
#################

.. code-block:: python

   plot.rarefactioncurve(obj, step='flexible', figsize=(14, 10), fontsize=18, var='None', order='None', tag='None', colorlist='None', onlyReturnData=False, onlyPlotData='None', savename='None')

Calculates a rarefaction curve based on subsampling without replacement.

*obj* is the object. 

*step* is the step size used during subsampling, if 'flexible' the total reads are divided by 20.

*figsize* is width and height of the figure in inches.

*fontsize* is size of text in figure.

*var* is the column in the meta data used to color code lines in plot.

*order* is the column in the meta data used to order the samples.

*tag* is the column in the meta data used to name lines in plot, if tag='index', the sample names are used.

*colorlist* is list of colors to be used in the plot, if 'None' qdiv default is used.

if *onlyReturnData* =True, function will return a python dictionary with data.

if *onlyPlotData* is a dictionary with data (generated in a previous step by running the function with onlyReturnData=True), it will be plotted and no calculations will be carried out.

if *savename* is specified, plots will be saved and data will be saved as a pickle file.

Octave (frequency histogram)
############################

.. code-block:: python

   plot.octave(obj, var='None', slist='None', nrows=2, ncols=2, fontsize=11, figsize=(10, 6), xlabels=True, ylabels=True, title=True, color='blue', savename='None')

Octave plot according to Edgar and Flyvbjerg, DOI:10.1101/38983

*obj* is the qdiv object. 

*var* is the column heading in metadata used to select samples to include. The counts for all samples with the same text in var column will be merged.

*slist* is a list of names in meta data column which specify samples to keep. If slist='None' (default), the whole meta data column is used.

*nrows* and *ncols* are the number of rows and columns in the plot; nrows*ncols must be equal to or more than the number of samples plotted.

if *xlabels* =True, k is shown for the bins on the x-axis

if *ylabels* =True, ASV counts are shown on the y-axis

if *title* =True, sample name is shown as title for each panel

*color* determines color of bars

*savename* is path and name of file.

Dissimilarity contributions of taxa
###################################

.. code-block:: python

   plot.dissimilarity_contributions(obj, var='None', q=1, index='local', numberToPlot=20, levels=['Genus'], fromFile='None', figsize=(18/2.54, 14/2.54), fontsize=10, savename='None')

Plot showing contribution of each taxon to observed dissimilarity between multiple samples.

*obj* is the qdiv object.

*var* is the column heading in the meta data used to categorize the samples. If a category has two or more samples, dissimilarity samples within that category is calculated.

*q* is the diversity order. 

*index* is the type of dissimilarity index (either local or regional).

*numberToPlot* is the number of taxa to include.

*levels* are taxonomic levels to include on y-axis.

*fromFile* could be that path to a csv file generated with the output from diversity.naive_dissimilarity_contributions.

*savename* is path and name of files to be saved.
