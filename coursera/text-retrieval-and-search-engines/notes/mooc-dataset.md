# MOOC Dataset

The [MOOC dataset](../../../meta/data/moocs) contains the descriptions found on the webpages of arround 23,000 MOOCs (Massive Open Online Courses).

Below the description of each file:

* **mooc.dat** contains the content of the webpages of all the MOOCs. Actually, this file was generated by scrap all course sites on coursera. Format:
```
<COURSE NAME> - <COURSE PROVIDER> <COURSE URL> <LONG TEXT>
```
* **metadata.dat** contains the names and the URLs of the MOOCs. Actually, this file is simplified version of *mooc.dat*. Format:
```
<COURSE NAME> - <COURSE PROVIDER> <COURSE URL>
```
* **mooc-queries.txt** contains a set of queries that will use to evaluate the effectiveness of search engine. Format:
```
<QUERY TEXT>
```
* **mooocs-qrel.txt** contains the relevance judgements corresponding to the queries in *moocsqueries.txt*. Format:
```
<QUERY NUMBER> <DOCUMENT ID> <JUDGEMENT>
```
where:
- *QUERY NUMBER* is line number in *mooc-queries.txt*.
- *DOCUMENt ID* is line number in *mooc.dat*.
- *JUDGEMENT* is boolean value: 1 or 0. 1 if relevance and 0 if not relevance.