# What's New ?
This is the page that reports ZCurveHub updates and their latest work. You can bookmark this page to keep up with the latest news.

## Released version 1.5.11

### Software Update:

**Date:** 2025-04-14  
**[1]** Fixed a Bug that could cause the C++ core to crash;  
**[2]** Adjusted the ZCurveSegmenter parameter name to prevent confusion;  
**[3]** Added the feature to handle subsequences intercepted from genomes for ZCurveSegmenter;  
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
**[1]** Fixed the errors in the document and standard documentation for ZCurveSegmenter;  
**[2]** Add version restrictions for dependent packages to prevent incorrect configuration;  
**[3]** Optimized C++ module compilation process, supports installation on unsupported systems;  
**[4]** Fixed a bug where plot sampling intervals could not be set automatically;  
**[5]** The output saving process of command line program is optimized;  

## Released version 1.5.9

### Software Update:

**Date:** 2025-03-15  
**[1]** Fixed incorrect display of date and version information in `__init__` module comments;  
**[2]** Removes the constraint that ZCurveBuilder's input data type must be Iterable;  
**[3]** Fixed ZCurveBuilder compatibility issues with models in sklearn;  
**[4]** Fixed incorrect display of formulas in README documentation;  
**[5]** Fixed an issue where jump links in documentation did not work;  
**[6]** The GenBank files will only be downloaded when users need to extract CDS;  
**[7]** Fixed an issue where the graphical interface could not be displayed properly on Linux systems;  