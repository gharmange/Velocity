# Files needed to run velocity
   File 1: Output folder from runing CellRanger on the 10x Datat
   
   File 2: The referece genome file used when running CellRanges (the gene.gtf file) which you can find in your installation of CellRange or download here:https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest
   
   File 3: A repeat masking file (in GTF format)for the genome you are using which you can find here: https://genome.ucsc.edu/cgi-bin/hgTables?hgsid=611454127_NtvlaW6xBSIRYJEBI0iRDEWisITa&clade=mammal&org=Human&db=0&hgta_group=allTracks&hgta_track=rmsk&hgta_table=rmsk&hgta_regionType=genome&position=&hgta_outputType=gff&hgta_outFileName=mm10_rmsk.gtf

# Setting up environment and running velocity
1. If you have not installed anaconda do so following these instructions (choose anoconda not miniconda):
https://docs.conda.io/projects/conda/en/latest/user-guide/install/

2. Click the green Code button on this page and selecting zip to download the conde needed to run velocity

3. Open terminal and run this line of code to download the right envronment: 
      `conda env create -f velocityenv.yml` 
      (replacing <velocityenv.yml> with the full path to that file) to create 
4. Next activate the environment by runing this line of code in the terminal `conda activate velocityenv`
5. You can then open jupyter notebook in this environment by typying `jupyter notebook` in the same terminal windo you did step 4
6. Next navigate in the jupyter notebook file navigator to open RunRNAvelocity.ipynb dowloaded from this page
7.

