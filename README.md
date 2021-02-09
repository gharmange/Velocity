# These steps only need to be done once per computer you want to run RNA velocity on
## Adding gcc compiler to your computer
   This step is needed to install the velocyto package
  1. To install homebrew paste this into terminal `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` and hit enter
   (more detail here: https://brew.sh)
  2. Once installed paste this into terminal `brew install gcc` and hit enter
  3. The gcc compiler is installed at this point but doesn't get accessed when trying to install velocyto. This next step makes it work, but REMEMBER TO UNDO IT when you are done. I have no idea why this works, if there is a better way please let me know.
  4. Navigate to this path in finder "/usr/local/bin/" (to do this you can click "Go" in the finder toolbar, then click "Go To Folder..." and just type in "/usr/local/bin/") you should find a file in there called gcc-# (where # will be the number of the version of gcc (ex. gcc-10)) change the name of this file to just gcc (REMEMBER THE OLD NAME TO REVERT THIS LATER)


## Installing environment
1. If you have not installed anaconda do so following these instructions (choose anaconda not miniconda):
https://docs.conda.io/projects/conda/en/latest/user-guide/install/

2. Click the green Code button on this page and selecting zip to download the code needed to run velocity

3. Open terminal and run this line of code to download the right environment:
      `conda env create -f velocityenv.yml`
      (replacing <velocityenv.yml> with the full path to that file)
4. Go back to the directory /usr/local/bin/ in finder and revert the file name back from "gcc" to "gcc-#"

# These Steps need to be done for every new data set you want to do RNA velocity on
## Files needed to run velocity
   File 1: Output folder from running CellRanger on the 10x Data

   File 2: The reference genome file used when running CellRanges (the gene.gtf file) which you can find in your installation of CellRange or download here:https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest

-once downloaded unzip and the file will be in the subfolder named gene (you can delete everything else)

   File 3: A repeat masking file (in GTF format)for the genome you are using which you can find here: https://genome.ucsc.edu/cgi-bin/hgTables?hgsid=611454127_NtvlaW6xBSIRYJEBI0iRDEWisITa&clade=mammal&org=Human&db=0&hgta_group=allTracks&hgta_track=rmsk&hgta_table=rmsk&hgta_regionType=genome&position=&hgta_outputType=gff&hgta_outFileName=mm10_rmsk.gtf

-once downloaded unzip the file

## Creating Intron and exon reads file
1. Next activate the environment by running this line of code in the terminal `conda activate velocityenv`

2. You can then open jupyter notebook in this environment by typing `jupyter notebook` in the same terminal window you did step 4

3. Next navigate in the jupyter notebook file navigator to open RunRNAvelocity.ipynb downloaded from this page

4. Run the fist block of code and run the first block of code to make sure you are in the righ environment (should see a * next ot the velocityenv line printed in the output)

5. Now change all the path names in the second block of code to the files indicated and run the block of code

6. If in the output next to any of the files you see "permission denied", open up a new window in terminal, activate the virtual environment by running `conda activate velocityenv` and then run `chmod -R 775 <path to file where permission is denied>`

   If you run this block and it's starts printing a bunch of lines in the output then you have permission, just hit the "interrupt the kernel"
   button (black box at the top of the jupyter notebook next to Run)

7. you can now run the next block of code to sort the bam files.
8. Once the file is sorted you should see a file called "cellsorted_possorted_genome_bam.bam" in your outs folder in the 10X output folder
9. You can now run the next block of code, which runs velocyto to get intronic and exonic reads in your data. once done there should be a velocyto folder in your 10x output folder with a .loom file
10. Once the velocyto command has finished you have two options, you can filter your data in python, or you can move to R and use an R script to filter your data with Seurat. I have only done this step in R so there is no code for this step in python, but there is code in R.

## Filtering Data using R
1. Open the file "LoomProcessingSCVELO.Rmd" downloaded from this page in R. If you do not have R already, get R here:https://www.r-project.org and get Rstudio here: https://rstudio.com
2. Run the first block of code to load all packages. If you don't have them installed just run `install.packages("name of package")` for each package you don't have installed and then run the first block of code
3. In the second block of code change the path name to the path to the .loom file created by velocyto command in the steps above, and run this block of code
4. In the 3rd block of code I have the parameters I used to filter my data, but I suggest you look at your own data to determine what filters to use. If you are running velocity you likely already went through looking at your data in Seurat so just use the parameters you have been using in your previous analysis. If you have not run your data in Seurat, go to the Seurat website (https://satijalab.org/seurat/) and there you can learn how to set these parameters.
5. Once you have adjusted the filter parameters run this 3rd block of code, and make sure the UMAP looks as you expect.
6. In the 4th block of code change the path names to output the "SeuratProcessed.h5Seurat" and the "SeuratProcessed.h5ad" files in the velocyto file in the 10x output file, and run this block of code
# Once you have generated the files above you can start at this step every time
## Run RNA velocity using scvelo
1. We are now back into the jupyter notebook called "RunRNAvelocity.ipynb". If you still have the jupyter notebook running move on to the next step. If not, re-open the jupyter notebook by opening terminal running `conda activate velocityenv` and then running `jupyter notebook` and then navigating to, and opening "RunRNAvelocity.ipynb" (which is in the folder downloaded from GitHub) in the jupyter notebook navigator window
2. Run the 5th block of code to import all the python packages and set certain setting for scvelo
3. Run the 6th block of code to import the file you created in R (if you kept the file names indicated and the right paths in previous steps you should not have to change any paths here. If not just change the path to your path to the .h5ad file created in R)
4. From here on out you should be able to run the block of code sequentially and get the right RNA velocity outputs. I have put a few example things you can do with RNA velocity in this notebook, but you can do more! For details on what each line of code is doing and finding out what else you can do, go to the scvelo website (https://scvelo.readthedocs.io/VelocityBasics.html) and go through their tutorials. At this point you should be able to copy and paste any line of code from their tutorial into this notebook and it should run without a problem.
