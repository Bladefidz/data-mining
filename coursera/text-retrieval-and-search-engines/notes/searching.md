# Searching

After the `inverted index` has been created, then we can set up the search engine. We can easily set up the search engine by set ranking function in configuration file `config.toml`.

## Setup the search engine in MeTa

1. Open `config.toml` and set the `ranker` section:

    ```
    [ranker]
    method = "bm25"
    k1 = 1.2
    b = 0.2
    k3 = 500
    ```
    The configuration above tells MeTa to uses `BM25` rangking function with specified parameters.

2. Run the interactive search engine in shell:

    ```meta/build/interactive-search meta/config.toml```