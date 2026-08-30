# Returns chromosome counts from Chromosome Counts Database API

This function calls the Chromsome Counts Database (CCDB) API and returns
all counts for specified higher taxa.

## Usage

``` r
chrom_counts(
  taxa,
  rank = c("species", "genus", "family", "majorGroup"),
  full = FALSE,
  foptions = list()
)
```

## Arguments

- taxa:

  Taxonomic name(s) to query. Can be either a single name, a vector of
  multiple names or a list. If supplying multiple names, these must all
  be of the same `rank`.

- rank:

  Rank to query.

- full:

  Logical. Whether to return full records. Defaults to `FALSE` which
  returns only partial records. Partial records includes the resolved
  name as well as the gametophytic (n) and sporophytic (2n) counts.

- foptions:

  additional options to be passed to
  [`httr::GET`](https://httr.r-lib.org/reference/GET.html)

## Value

A `data.frame` containing all records matched by query

## Details

When using the API to query for species, both matched names and resolved
names are searched. This means that all records for potential synonyms
will be returned as well. Currently species binomials must be specified
by either 'genus species' (i.e., space between genus and species) or
'genus_species'.

To search for subspecies (subsp.) or varieties (var.), you can use
search terms like:

`"Solanum acaule var. albicans"`.

Searching for `"Solanum acaule"` will return all subspecies and
varieties.

Currently the only acceptable search terms when specifying
`"majorGroup"` are `"Angiosperms"`, `"Gymnosperms"`, `"Pteridophytes"`,
or `"Bryophytes"`.

## Examples

``` r
if (FALSE) { # \dontrun{

## Get all counts for genus Castilleja
chrom_counts("Castilleja", "genus")

## Get all counts for both Castilleja and Lachemilla
chrom_counts(c("Castilleja", "Lachemilla"), "genus")

## Get all counts for Castilleja miniata
chrom_counts("Castilleja miniata", "species")

## Get all counts for only Castilleja miniata subsp. elata
chrom_counts("Castilleja miniata subsp. elata", "species")

## Note that searching for "Castilleja miniata" will return
## all subspecies and varieties

## Get all counts for the Orobanchaceae
chrom_counts("Orobanchaceae", "family")

} # }
```
