# Stemming

Stemming is task to identify similar words, for example words 'retrieve', 'retrieval', and 'retrieving' should be mapped to the root word 'retrieve'.


## Using MeTa to do stemming

MeTa uses [Porter2 English Stemmer](http://snowball.tartarus.org/algorithms/english/stemmer.html). Here step by step how to do stemming using MeTa:

1. Consider a document called as `doc.txt` with following content:

       Recent years have seen a dramatic growth of natural language text data, including web pages, news articles, scientific literature, emails, enterprise documents, and social media such as blog articles, forum posts, product reviews, and tweets. Text data are unique in that they are usually generated directly by humans rather than a computer system or sensors, and are thus especially valuable for discovering knowledge about people's opinions and preferences, in addition to many other kinds of knowledge that we encode in text.

        This course will cover search engine technologies, which play an important role in any data mining applications involving text data for two reasons. First, while the raw data may be large for any particular problem, it is often a relatively small subset of the data that are relevant, and a search engine is an essential tool for quickly discovering a small subset of relevant text data in a large text collection. Second, search engines are needed to help analysts interpret any patterns discovered in the data by allowing them to examine the relevant original text data to make sense of any discovered pattern. You will learn the basic concepts, principles, and the major techniques in text retrieval, which is the underlying science of search engines.
2. Execute stemming:
```./profile config.toml doc.txt --stem```
3. The new document called `doc.stems.txt` created with stopwords removed. Here the content of `doc.stems.txt`:

    recent year have seen a dramat growth of natur languag text data , includ web page , news articl , scientif literatur , email , enterpris document , and social media such as blog articl , forum post , product review , and tweet . 
    text data are uniqu in that they are usual generat direct by human rather than a comput system or sensor , and are thus especi valuabl for discov knowledg about peopl opinion and prefer , in addit to mani other kind of knowledg that we encod in text . 
    this cours will cover search engin technolog , which play an import role in ani data mine applic involv text data for two reason . 
    first , while the raw data may be larg for ani particular problem , it is often a relat small subset of the data that are relev , and a search engin is an essenti tool for quick discov a small subset of relev text data in a larg text collect . 
    second , search engin are need to help analyst interpret ani pattern discov in the data by allow them to examin the relev origin text data to make sens of ani discov pattern . 
    you will learn the basic concept , principl , and the major techniqu in text retriev , which is the under scienc of search engin .