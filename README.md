# SAV-alternating-designs-code

Code for the analysis in **Modeling occupancy probabilities hierarchically, given misclassification and spatial dependence** by Katherine St. Clair, Jun Young Park,  Brian R. Gray, Robert S. Capers


You must have R and [WinBUGS](https://www.mrc-bsu.cam.ac.uk/software/bugs/the-bugs-project-winbugs/) installed to fit the models. 

We recommend that you use Rstudio for easiest running of these R Markdown scripts. 


1. `DataCleanUp.Rmd`: Creates the data needed to run `RunModels.Rmd`
2. `EDA.Rmd`: Creates basic EDA stats and plot
3. `RunModels.Rmd`: After running `DataCleanUp.Rmd` commands, run these commands to fit the three models.
4. `PosteriorResults.Rmd`: After all models and species runs are complete, use these commands to create the figures presented in the paper.