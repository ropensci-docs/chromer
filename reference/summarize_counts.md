# Summarize chromosome counts from API call

This function processes and cleans the data returned from the API call
for use in downstream analysis.

## Usage

``` r
summarize_counts(counts)
```

## Arguments

- counts:

  A 'chrom.counts' object inherited from
  [`chrom_counts`](https://docs.ropensci.org/chromer/reference/chrom_counts.md).

## Value

A `data.frame` containing the resolved binomial, the count type
(gametophytic or sporophytic), the counts, the inferred gametophytic
count (for sporophytic records) and the number of records supporting
each count.

## Details

The results from the API call are a bit messy and difficult to use for
downstream analyses. This function cleans up the data in three ways.
First, it combines aggregates and summarizes all records from each
species. Second, many of the counts are combined with text characters
(e.g., `"#-#"`, `"c.#"`, and `"#, #, #"`. This function uses regular
expressions to pull out all and any numeric values from these strings.
Third, some of the records are gametophytic (n) counts and others are
from sporophytes (2n); the function simply divides the sporophytic
counts in half so that all measurements are on a common scale.

IMPORTANT: Use this function with caution. Parsing the counts
programmatically may be useful but it may generate erroneous results in
some cases if input is in an odd format. For example, if the count is
`"#+-#"`, the function will return both the first and second `#` as
valid counts . Given the creativity(?) of researchers in entering data,
it is hard to predict all possible ways that the counts may be
represented. Therefore, some manual checking will probably be necessary.

## Examples

``` r
if (FALSE) { # \dontrun{

## Get all counts for genus Castilleja
res <- chrom_counts("Castilleja", "genus")

## summarize the results
summarize_counts(res)

} # }
```
