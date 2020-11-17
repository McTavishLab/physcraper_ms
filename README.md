# Physcraper manuscript

## To render the BMC Bioinformatics version:

```
tools::texi2pdf(file = "sources/bmc_template/bmc_article.tex", clean=TRUE)
# but I have not found a way to assign name and location to output.

# so I just moved it:
mv bmc_article.pdf docs/submission-bmc-2020-11-25.pdf

#output = paste0("docs/submission-bmc-", Sys.Date(), ".pdf")
```

## How to render other versions of this ms.

```
rmarkdown::render(input = "physcraper_ms.Rmd", output_file = paste("physcraper_ms-", Sys.Date(), ".pdf"))
```

```
rmarkdown::render(input = "render2-word.Rmd", output_file = paste0("docs/word-", Sys.Date(), ".docx"))
rmarkdown::render(input = "render2-sysbio.Rmd", output_file = paste0("docs/submission-sysbio-", Sys.Date(), ".pdf"))
rmarkdown::render(input = "render2-mee.Rmd", output_file = paste0("docs/submission-mee-", Sys.Date(), ".pdf"))
rmarkdown::render(input = "render2-mee.Rmd", output_file = paste0("docs/submission-mee-", Sys.Date(), ".doc"), output_format = "word_document")

```

The following will render the ms on various outputs specified in the yaml. This does not work with different outputs from the `rticles` package.

```
rmarkdown::render(input = "physcraper_ms.Rmd", output_format= "all")
```

Trying output_yaml worked. You just have to use the yaml params that are common to different formats in the main document, and add the extra ones on the extra yaml file. If there are any overlapping params, it will take the ones from the yaml specified in output_yaml:

```
rmarkdown::render(input = "physcraper_ms.Rmd", output_yaml= "joss.yaml")
rmarkdown::draft("ams_submission", template = "ams_article", package = "rticles")

rmarkdown::render(input = "physcraper_ms.Rmd", output_file= paste("ams_submission.pdf"), output_yaml= "ams.yaml")
```

To compile a .tex file to pdf I simply use the compile pdf button from RStudio,
which I think uses `tools::texi2pdf(output, clean=clean)`; tip taken from this [RStudio community thread](https://community.rstudio.com/t/what-commands-are-run-when-the-compile-pdf-button-is-clicked/6291/4)
