# What's New ?
This is the page that reports ZcurveHub updates and their latest work. You can bookmark this page to keep up with the latest news.

## Released version 1.6.0

### Software Update:

**Date:** 2025-06-05  
**[1]** Fixed the program crash issue caused by the memory management error of ZcurvePlotter.z_curve;  
**[2]** Sliding window AT-fraction and GC-fraction are added as auxiliary curves for ZcurvePlotter;  
**[3]** The calculation process of fitting the Z-curve was optimized to enhance robustness;  
**[4]** The calculation of genome order numbers for AT disparity and GC disparity were revised to better find the segmentation points;

### Web Service Update:

**Date:** 2025-06-02  
**[1]** Added auxiliary curve (AT/GC fraction/skew) plotting options to Z-curve Plotter;  
**[2]** NCBI Sequence Viewer was added for Z-curve Plotter and Z-curve Segmenter;  
**[3]** Z-curve Segmenter can now display GC content curves and jump directly to the corresponding segment;  
**[4]** The Z-curve database was updated;  

## Released version 1.5.12

### Software Update:
**[1]** Sliding window calculated AT skew and GC skew have been added into APIs of ZcurvePlotter;  
**[2]** Sliding window calculated AT fraction and GC fraction have been added into APIs of ZcurvePlotter;  
**[3]** The directory of NCBI download cache is migrated from ncbi_acc_download to ncbi_cache;  
**[4]** No longer use ncbi-acc-download as the downloader. From 1.5.12, it use Entrez directly;  
**[5]** Add support for Python 3.12 and macOS systems.

## Released version 1.5.11

### Software Update:

**Date:** 2025-04-14  
**[1]** Fixed a Bug that could cause the C++ core to crash;  
**[2]** Adjusted the ZcurveSegmenter parameter name to prevent confusion;  
**[3]** Added the feature to handle subsequences intercepted from genomes for ZcurveSegmenter;  
**[4]** Updated the description of the Web Server in the documentation;  
**[5]** Frequently used API functions have been modified some return's type from Python list to Numpy ndarray;  
**[6]** The missing examples in the document have been completed.  

### Web Service Update:

**Date:** 2025-04-17  
**[1]** The 2D mode of Z-curve Plotter now allows users to select up to 4 components for each sequence;  
**[2]** The floating labels on the 3D mode curve can now display position information;  

## Released version 1.5.10

### Software Update:

**Date:** 2025-04-01  
**[1]** Fixed the errors in the document and standard documentation for ZcurveSegmenter;  
**[2]** Add version restrictions for dependent packages to prevent incorrect configuration;  
**[3]** Optimized C++ module compilation process, supports installation on unsupported systems;  
**[4]** Fixed a bug where plot sampling intervals could not be set automatically;  
**[5]** The output saving process of command line program is optimized;  

## Released version 1.5.9

### Software Update:

**Date:** 2025-03-15  
**[1]** Fixed incorrect display of date and version information in `__init__` module comments;  
**[2]** Removes the constraint that ZcurveBuilder's input data type must be Iterable;  
**[3]** Fixed ZcurveBuilder compatibility issues with models in sklearn;  
**[4]** Fixed incorrect display of formulas in README documentation;  
**[5]** Fixed an issue where jump links in documentation did not work;  
**[6]** The GenBank files will only be downloaded when users need to extract CDS;  
**[7]** Fixed an issue where the graphical interface could not be displayed properly on Linux systems;  