# Indexing

MeTa supports two index types: **forward index** and **inverted index**. By default, MeTa will created inverted index if we set `index` key in `config.toml`. Also for full-text searching engine, we only need to build inverted index. The interactive demo can be found at [here](https://meta-toolkit.org/search-demo.html).


## Building MOOC search engine using MeTa

Here step-by-step building search engine for [mooc dataset](mooc-dataset.md) which stored in directory called as `moocs`:

1. Open configuration file. Assummed it called as `config.toml`.
2. Create `line.toml` file inside `path/to/moocs_directory` which has following content:

    ```
    type = "line-corpus"

    [[metadata]]
    name = "name"
    type = "string"
    ```
    The `type` key tell MeTa that to used **line corpus** which means MeTa will parse each line in `metadata.data`. The `metadata` section specify how MeTa should parse each line. The metadata configuration above will create `name` field with data type `string` for each line in `metadata.dat`. 

3. Set following keys in `config.toml` to initialize search engine:

    ```
    query-judgements = "path/to/moocs-qrels.text"
    querypath = "path/to/moocs_directory"
    corpus = "line.toml"
    dataset = "moocs"
    index = "moocs"
    ```
    The main keys are `dataset` and `corpus`. The `dataset` key defines dataset name found in relative path defined in `querypath` key. The `corpus` keys defines corpus configuration file found in relative path defined in `querypath`. The `query-judgements` key defined qury judgements that can be used for speific algorithms, such as BM25, collaborative filltering, etc. The `index` key will tells MeTa to create `inverted index` which name `moocs`.

4. Set `analyzers` configuration section in `config.toml`:

    ```
    [[analyzers]]
    method = "ngram-word"
    ngram = 1
    filter = "default-unigram-chain"
    ```
    The `analyzers` section defines tokenization and filtering mechanism. The values of `method` and `ngram` above means MeTa used `n-gram` model with size 1. In other words, MeTa will construct inverted index contains `unigram` word, such as "move", "down", "philip", etc. The value of `filter` key means MeTa will used default filtering chain method, which performs a couple of predifined filters including *lower case conversion*, *length filtering*, and *stemming*. For more information about `n-gram`, please read [wikipedia](https://en.wikipedia.org/wiki/N-gram).

5. Execute indexing command:

    ```meta/build/index meta/config.toml```

6. The output should be similar to this:

    ```
    > Counting lines in file: [=================================] 100% ETA 00:00:00 
    1531644629: [info]     Creating index: moocs/inv (/home/bladefidz/Codes/data-mining/meta/src/index/inverted_index.cpp:119)
    > Tokenizing Docs: [========================================] 100% ETA 00:00:00 
    > Merging: [================================================] 100% ETA 00:00:00 
    1531644642: [info]     Created uncompressed postings file moocs/inv/postings.index (9.120000 MB) (/home/bladefidz/Codes/data-mining/meta/src/index/inverted_index.cpp:148)
    > Compressing postings: [===================================] 100% ETA 00:00:00 
    1531644642: [info]     Created compressed postings file (7.620000 MB) (/home/bladefidz/Codes/data-mining/meta/src/index/inverted_index.cpp:279)
    1531644642: [info]     Done creating index: moocs/inv (/home/bladefidz/Codes/data-mining/meta/src/index/inverted_index.cpp:166)
    Number of documents: 17972
    Avg Doc Length: 358.238
    Unique Terms: 160615
    Index generation took: 14.709 seconds
    ```

6. If the above command successfully executed, then it will created the inverted index and places it in **meta/build/moocs/inv**.

For more information, please read the documentation [here](https://meta-toolkit.org/overview-tutorial.html).