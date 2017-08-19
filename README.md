This is an attempt to open a repository of the scripts I have written for various zooniverse projects.
It is a work in progress.
These scripts are written in Python 3.6.2.  They use as few additional packages as possible - the goal is to be able to run them with an out-of-the box Python set-up.  This is not always possible (eg plotting); in those cases I will provide a complete list of the required dependencies.  
I am not a professional coder - I deliberately use simple explicit code to make these scripts as easy to undersatnd and modify as possible - the goal is that they are useable by someone with minimal coding experience. To use most of them one needs to be able to follow some (hopefully) simple instructions.  These will include copying and pasting defined blocks of code, commenting out or "uncommenting" various lines of code, modifing some specified strings/and or variable names, and running the result in a python interpreter. Between the instructions, comments in the code, and the example demos someone with minimal coding experience (like me) should be able to extract their zooniverse data in a useable form from projects built with the standard project builder.

## DBSCAN clustering script: Completed, with demo and readme

This DBSCAN clustering algorithm is intended for data sets which are limited to a few hundred points – it is not optimized for R-trees or large data sets, but works well for the data sets expected from drawing tool uses in zooniverse projects.
It is useful for aggregating the user data for various drawing tools (points circles etc). It is also useful for determining if a user placed more than one drawing tool within a close proximity to one already place within the same classifcation (ie testing for double clicks). It can also be used to test for drawing tools which were placed where no other user placed one - this can be used to test for the user's incidence of noise generation as a measure of their competance or as a test for bots.

## Flatten classification file building blocks

This group of scripts is my approach to the problem of flattening (ie simplifying and breaking apart) the JSON formatted strings in the Zooniverse classification download.  This is directed at project owners with little IT support using the project builder to create their project. Like the project builder the effort is made up of a basic framework on which blocks are added - basically the correct blocks are added to handle the output from each particular task in the project. Each block of code must be slightly modified in a easy to understand way to match the project's task labels so the output data is labeled in a way the project owner expects.
The following modules or blocks are planned:
#### 1) The basic framework with ability to Slice the Classification file in various ways to select the pertinent records. Completed, with slicing demo and readme.
This will provide the framework the other blocks will be added onto. By itself it can be used to slice (ie to select specific records) the Classification file based on various conditional clauses using specificed fields in the classification records.

#### 2) General utility blocks to provide some simple functions that make the output file more useful: Completed, with two demos and readme. 
  -	user_name This block replaces not-logged-in user_name based on an external picklist prepared elsewhere and keyed off user_ip.  The scripts to generate a picklist can use ip or browser data to group the not-logged-in users.
  -	image_number These blocks attempt to get subject image metadata from the subject_data field and generate a image identifier that may be more significant to the project owner or alternately, merge a cross-reference csv file into the flattened output file. The cross reference file is generated elsewhere and could have additional fields such as geo-references. The image_number (and possibly other info) will be (a) field(s) in the output file to aid analysis.  The external cross reference file is read in its entirety into memory.  If it is a very large file this may strain computing resources.  In that case one could use the slice function of the Frame to break the task into blocks by subject number.  Alternately a script could be written to handle a customized file merge later – the effort to set one up is likely more than the effort to break the task into chunks and run the job piecemeal 
  -	elapsed_time This block pulls the started and finished times from the metadata field and calculates the elapsed time the user spent on the classification.
  -	image_size This block attempts to pull the natural height and width for the subject image from the metadata file. This can be used for various scaling operations for plotting, clustering or for testing out-of-bounds drawing tools.

#### 3) Task specific blocks that handle the various task types allowed by the project builder.  The following blocks are planned. Those with an asterix are written and working in some form:
- *Question with single answer
- *Question with Multiple answers 
- *Drawing tool - Point
- Drawing tool - Line
- *Drawing tool - Circle
- Drawing tool - Box (rectangle and column)
- Drawing tool - Triangle
- Drawing tool - Polygon
- Drawing tool - Elipse
- Drawing tool - Bezier
- Transcription - single field
- Transcriptiion - drop-down
- Transcription - multiple fields
- Survey - 2D (choice and howmany) full array
- Survey - 3D (choice, howmany, behaviour) full array
- Survey - 2D non-zero elements only
- Survey - 3D non-zero elements only_

#### 4) Test blocks which will preform simple tests on the output from one or more of the blocks listed in 3):
-	*Test points from point drawing tools lay within the image_size (ie no out-of-bounds points.)
-	*Test circle centers are within a fixed percentage of the circle radius of an image edge (ie part of the circle lies within the image.)
-	*Test that no two points of the same type are placed within a distance “eps” of each other on the same subject by the same classifier (ie test for double clicks)
-	*As for above except for circle centres.
-	*Test the radius of a circle is within a range specified (relative to the image_size)
-	Test the duration is consistent with a human classifier.







