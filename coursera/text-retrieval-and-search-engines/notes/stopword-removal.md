# Stopword Removal

Stopword removal is task to remove non-informative words, such as 'a', 'the', 'is', etc. By removing non-informative words, the inverted index size will be smaller, thus increase indexing performance.


## Using MeTa to do stopword removal

MeTa uses a list of stopwords saved in **/meta/data/lemur-stopwords.txt**. Below step-by-step to do stopword removal using MeTa:

1. Consider this document called as `doc.txt` with following content:
        
        Recent years have seen a dramatic growth of natural language text data, including web pages, news articles, scientific literature, emails, enterprise documents, and social media such as blog articles, forum posts, product reviews, and tweets. Text data are unique in that they are usually generated directly by humans rather than a computer system or sensors, and are thus especially valuable for discovering knowledge about people's opinions and preferences, in addition to many other kinds of knowledge that we encode in text.

        This course will cover search engine technologies, which play an important role in any data mining applications involving text data for two reasons. First, while the raw data may be large for any particular problem, it is often a relatively small subset of the data that are relevant, and a search engine is an essential tool for quickly discovering a small subset of relevant text data in a large text collection. Second, search engines are needed to help analysts interpret any patterns discovered in the data by allowing them to examine the relevant original text data to make sense of any discovered pattern. You will learn the basic concepts, principles, and the major techniques in text retrieval, which is the underlying science of search engines.
2. Execute stop word removal:
```./profile config.toml doc.txt --stop```
3. The new document called `doc.stops.txt` created with stopwords removed. Here the content of `doc.stops.txt`:
        
        recent years dramatic growth natural language text data web pages news articles scientific literature emails enterprise documents social media blog articles forum posts product reviews tweets 
        text data unique usually generated directly humans computer system sensors especially valuable discovering knowledge people's opinions preferences addition kinds knowledge encode text 
        course cover search engine technologies play important role data mining applications involving text data two reasons 
        raw data large particular problem relatively small subset data relevant search engine essential tool quickly discovering small subset relevant text data large text collection 
        second search engines needed help analysts interpret patterns discovered data allowing examine relevant original text data make sense discovered pattern 
        learn basic concepts principles major techniques text retrieval underlying science search engines 
