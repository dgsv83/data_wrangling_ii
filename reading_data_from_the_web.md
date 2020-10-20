Data Wrangling II
================

## scrape a table

I want the first table from \[this page\]
(<http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm>)

read in the html

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"


drug_use_html = read_html(url)
```

extract the table(s) which got me all the 15 tables in the website;
focus on the first one

``` r
tabl_marj = 
  drug_use_html %>%
  html_nodes(css = "table") %>%
  first() %>%
  html_table() %>% 
  slice(-1) %>%
  as_tibble()
```

## star wars movie info

I want the data from [here](https://www.imdb.com/list/ls070150896/)

``` r
url = "https://www.imdb.com/list/ls070150896/"

swm_html = read_html(url)
```

Grab elements that I want.

``` r
title_vec = 
  swm_html %>%
  html_nodes(".lister-item-header a") %>%
  html_text()

gross_rev_vec = 
  swm_html %>%
  html_nodes(".text-small:nth-child(7) span:nth-child(5)") %>%
  html_text()

runtime_vec = 
  swm_html %>%
  html_nodes(".runtime") %>%
  html_text()

swm_df = 
  tibble(
    title = title_vec,
    rev = gross_rev_vec,
    runtime = runtime_vec)
```
