Subset and manipulate data
**************************

Subset to specific samples
##########################

.. code-block:: python

   subset.samples(obj, var='index', slist='None', keep0=False):

Returns an object subsetted to the selected samples.

*obj* is the object generated with files.load

*var* is the column heading in the meta data used for subsetting, if var=’index’ the actual sample names will be used

*slist* is a list of samples or meta data labels to keep

if *keep0* =True, OTUs/ASVs, which have zero reads associated with them after subsetting will be kept, otherwise they will be removed from the data.

Subset to specific OTUs/ASVs
############################

.. code-block:: python

   subset.sequences(obj, svlist)

Returns an object subsetted to the selected OTUs/ASVs.

*obj* is the object generated with files.load

*svlist* is a list of OTU or ASV names that should be kept in the data set.

Subset to the most abundant OTUs/ASVs
#####################################

.. code-block:: python

   subset.abundant_sequences(obj, number=25, method='sum')

Returns an object with only the most abundant OTUs/ASVs.

*obj* is the object generated with files.load
 
*number* specifies the number of ASVs to keep 

*method* is the method used to rank OTUs/ASVs. 
If *method* ='sum', the OTUs/ASVs are ranked based on the sum of the relative abundances in all samples. 
If *method* ='max', they are ranked based on the max relative abundance in a sample.

Subset based on taxonomic classification
#########################################

.. code-block:: python

   subset.text_patterns(obj, subsetLevels=[], subsetPatterns=[]):

Searches for specific text patterns among the taxonomic classifications. Returns an object subsetted to OTUs/ASVs matching those text patterns.

*subsetLevels* is a list taxonomic levels in which text patterns are searched for, e.g. ['Family', 'Genus']

*subsetPatterns* is a list of text patterns to search for, e.g. ['Nitrosom', 'Brochadia']

Merge samples
##############

.. code-block:: python

   subset.merge_samples(obj, var='None', slist='None', keep0=False)

Returns an object where samples belonging the same category (as defined in the meta data) have been merged.

*var* is the column heading in metadata used to merge samples, the read counts for all samples with the same text in var column will be merged

*slist* is a list of names in meta data column which specify samples to keep, if slist='None' (default), all samples are kept

if *keep0* =False, all OTUs/ASVs with 0 counts after merging will be discarded from the data.


Rarefy
######

.. code-block:: python

   subset.rarefy_table(tab, depth='min', seed='None', replacement=False)
   
   subset.rarefy_object(obj, depth='min', seed='None', replacement=False):

Rarefies a count table to a specific number of reads per sample. The function subset.rarefy_table() operates only on the count table and returns only a rarefied table. 
The function subset.rarefy_object() operates on the whole object and returns a whole object. 
This means that samples and OTUs/ASVs which might have been dropped from the count table during rarefaction
are also dropped from the 'ra', 'tax', 'seq', and 'meta' dataframes of the object.

*tab* is the count table to be rarefied

*object* is the object containing the count table to be rarefied

if *depth* ='min', the minimum number of reads in a sample is used as rarefaction depth, otherwise a number can be specified 

*seed* sets a random state for reproducible results, use an integer.

if *replacement* =False, the function is similar to rarefaction without replacement, if *replacement* =True, it does rarefaction with replacement.

Consensus table
###############

.. code-block:: python

   subset.consensus(objlist, keepObj='best', taxa='None', alreadyAligned=False, differentLengths=False, nameType='ASV', onlyReturnSeqs=False)

Takes a list of objects and returns a consensus object based on ASVs found in all. Information about the fraction of reads retained from the original objects is also provided.

*objlist* is a list of objects 

*keepObj* makes it possible to specify which object in objlist that should be kept after filtering based on common ASVs, specify with integer 
(0 is the first object, 1 is the second, etc), ‘best’ means that the object which has the highest fraction of its reads mapped to the common ASVs is kept

*taxa* makes it possible to specify with an integer the object having taxa information that should be kept 
(0 is the first object, 1 is the second, etc), if 'None', the taxa information in the kept object is used 

if *alreadyAligned* =True, the subset.align_sequences function has already been run on the objects to make sure the same sequences in different objects have the same names 

if *differentLengths* =True, it assumes that the same ASV inferred with different bioinformatics pipelines could have different sequence lengths. 

*nameType* is the label used for sequences (e.g. ASV or OTU)

if *onlyReturnSeqs* =True, only a dataframe with the shared ASVs is returned. 

Example

.. code-block:: python

   import qdiv

   cons_obj, info = qdiv.subset.consensus([obj1, obj2])
   
   qdiv.stats.print_info(cons_obj)
   
   print(info)

In the example above, *cons_obj* is the new consensus object constructed based on obj1 and obj2. 

*info* contains information about the fraction of reads retained from obj1 and obj2, as well as the maximum relative abundance of reads lost in a sample in each of the original objects.

.. code-block:: python

   import qdiv

   shared_seqs, info = qdiv.subset.consensus([obj1, obj2], onlyReturnSeqs=True)
   
In the example above, *shared_seqs* is a pandas dataframe with the shared sequences

*info* just contains a text string saying that the shared ASVs were returned.

Merge objects
#############

.. code-block:: python

   subset.merge_objects(objlist, alreadyAligned=False, differentLengths=False, nameType='ASV')

Takes a list of objects and a merged objects including all OTUs/ASVs and samples.

*objlist* is a list of objects 

if *alreadyAligned* =True, the subset.align_sequences function has already been run on the objects to make sure the same sequences in different objects have the same names 

if *differentLengths* =True, it assumes that the same ASV inferred with different bioinformatics pipelines could have different sequence lengths. 

*nameType* is the label used for sequences (e.g. ASV or OTU)

Example

.. code-block:: python

   import qdiv

   merged_obj = qdiv.subset.merge_objects([obj1, obj2])
   
   qdiv.stats.print_info(merged_obj)

In the example above, *merged_obj* is the new object constructed by combining obj1 and obj2. 
