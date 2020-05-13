# Physcraper manuscript

## How to render any version of this ms.

```
rmarkdown::render(input = "physcraper_ms.Rmd", output_file = paste("physcraper_ms-", Sys.Date(), ".pdf"))
```
The following will render the ms on various outputs specified in the yaml. However, it will not work with different outputs from the `rticles` package.

```
rmarkdown::render(input = "physcraper_ms.Rmd", output_format= "all")
```

Trying output_yaml worked. You just have to use the yaml params that are common to different formats in the main document, and add the extra ones on the extra yaml file. If there are any overlapping params, it will take the ones from the yaml specified in output_yaml:

```
rmarkdown::render(input = "physcraper_ms.Rmd", output_yaml= "joss.yaml")
rmarkdown::draft("ams_submission", template = "ams_article", package = "rticles")

rmarkdown::render(input = "physcraper_ms.Rmd", output_file= paste("ams_submission.pdf"), output_yaml= "joss.yaml")
```

