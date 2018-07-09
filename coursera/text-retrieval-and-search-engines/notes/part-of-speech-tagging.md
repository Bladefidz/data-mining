# Part-of-Speech Tagging

[Part-of-speech tagging](en.wikipedia.org/wiki/Part-of-speech_tagging) or POS is the process of assigning parts of speech (such as verb, noun, adjective, adverb, etc.) to word in a given text. Each word will be analyze depends on the context, paragraph, or phrase.

Here commonly used tags and their meaning based on [UPenn Treebank List](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html):

* CC: Coordinating conjuction, e.g., *and*, *but*, *or*.
* CD: Cardinal number, e.g., *one*, 1, *two*, 2.
* DT: Determiner, e.g., *a*, *the*, *every*.
* EX: Existential *there*, e.g., *there* in "there is a God".
* FW: Foreign word
* IN: Preposition or subordinating conjunction, e.g., *after*, *in*, *to*, *with*.
* JJ: Adjective, e.g., *blue* in "the blue car", *deep* in "the water is deep".
* JJR: Adjective, comparative, e.g., *larger*, *smaller*, *faster*, *higher*, *better*.
* JJS: Adjective, superlative, e.g., *largest*, *smallest*, *fastest*, *highest*.
* LS: List item marker.
* MD: Modal, e.g., *could*, *will*.
* NN: Noun, singular, or mass, e.g., *door*, *car*.
* NNS: Noun plural, e.g., *doors*, *cars*.
* NNP: Proper noun, singular, e.g., *john*.
* NNPS: Proper noun, plural, e.g., *Vikings*.
* PDT: Predeterminer, e.g., *both*, *a lot of*.
* POS: Possessive ending, e.g., *s* in "friend's"
* PRP: Personal pronoun, e.g., *I*, *he*, *it*.
* PRP$: Possessive pronoun, e.g., *my*, *his*.
* RB: Adverb, e.g., *however*, *usually*, *naturally*, *here*, *good*.
* RBR: Adverb, comparative, e.g., *better*.
* RBS: Adverb, superlative, e.g., *best*.
* RP: Particle, e.g., *up* in "give up".
* TO: to, e.g., *to* in "to go" and "to him".
* UH: Interjection, e.g., *uhhuhhuhh*.
* VB: Verb, base form, e.g., *take*.
* VBD: Verb, past tense, e.g., *took*.
* VBG: Verb, gerund/present participle, e.g., *taking*.
* VBN: Verb, past participle, e.g., *taken*.
* VBP: Verb, singular present, non-3d, e.g., *take*.
* VBZ: Verb, 3rd person singular present, e.g., *takes*.
* WDT: Wh-determiner, e.g., *which*.
* WP: Wh-pronoun, e.g., *who*, *what*.
* WP$: Possessive wh-pronoun, e.g., *whose*.
* WRB: Wh-adverb, e.g., *where*, *when*.


## Using MeTa to do Part-of-Speech tagging

POS tag is assigned to each word after the underscore and abbreviated.

1. Consider this document called as `doc.txt` with following content:
        
        Recent years have seen a dramatic growth of natural language text data, including web pages, news articles, scientific literature, emails, enterprise documents, and social media such as blog articles, forum posts, product reviews, and tweets. Text data are unique in that they are usually generated directly by humans rather than a computer system or sensors, and are thus especially valuable for discovering knowledge about people's opinions and preferences, in addition to many other kinds of knowledge that we encode in text.

        This course will cover search engine technologies, which play an important role in any data mining applications involving text data for two reasons. First, while the raw data may be large for any particular problem, it is often a relatively small subset of the data that are relevant, and a search engine is an essential tool for quickly discovering a small subset of relevant text data in a large text collection. Second, search engines are needed to help analysts interpret any patterns discovered in the data by allowing them to examine the relevant original text data to make sense of any discovered pattern. You will learn the basic concepts, principles, and the major techniques in text retrieval, which is the underlying science of search engines.
2. Modify `config.toml` with following content:
```
[crf]
prefix = "path/to/crf/model/folder"
```
3. Execute `pos-tag`:
```./pos-tag config.toml doc.txt```
4. The new document called `doc.pos-tagged.txt` created with stopwords removed. Here the content of `doc.pos-tagged.txt`:
        
        Recent_JJ years_NNS have_VBP seen_VBN a_DT dramatic_JJ growth_NN of_IN natural_JJ language_NN text_NN data_NNS ,_, including_VBG web_NN pages_NNS ,_, news_NN articles_NNS ,_, scientific_JJ literature_NN ,_, emails_VBZ ,_, enterprise_NN documents_NNS ,_, and_CC social_JJ media_NNS such_JJ as_IN blog_NN articles_NNS ,_, forum_NN posts_NNS ,_, product_NN reviews_NNS ,_, and_CC tweets_NNS ._. 
        Text_NNP data_NNS are_VBP unique_JJ in_IN that_IN they_PRP are_VBP usually_RB generated_VBN directly_RB by_IN humans_NNS rather_RB than_IN a_DT computer_NN system_NN or_CC sensors_NNS ,_, and_CC are_VBP thus_RB especially_RB valuable_JJ for_IN discovering_VBG knowledge_NN about_IN people_NNS 's_POS opinions_NNS and_CC preferences_NNS ,_, in_IN addition_NN to_TO many_JJ other_JJ kinds_NNS of_IN knowledge_NN that_IN we_PRP encode_VBP in_IN text_NN ._. 
        This_DT course_NN will_MD cover_VB search_NN engine_NN technologies_NNS ,_, which_WDT play_VBP an_DT important_JJ role_NN in_IN any_DT data_NNS mining_NN applications_NNS involving_VBG text_NN data_NNS for_IN two_CD reasons_NNS ._. 
        First_NNP ,_, while_IN the_DT raw_JJ data_NN may_MD be_VB large_JJ for_IN any_DT particular_JJ problem_NN ,_, it_PRP is_VBZ often_RB a_DT relatively_RB small_JJ subset_NN of_IN the_DT data_NNS that_WDT are_VBP relevant_JJ ,_, and_CC a_DT search_NN engine_NN is_VBZ an_DT essential_JJ tool_NN for_IN quickly_RB discovering_VBG a_DT small_JJ subset_NN of_IN relevant_JJ text_NN data_NNS in_IN a_DT large_JJ text_NN collection_NN ._. 
        Second_JJ ,_, search_JJ engines_NNS are_VBP needed_VBN to_TO help_VB analysts_NNS interpret_VB any_DT patterns_NNS discovered_VBN in_IN the_DT data_NNS by_IN allowing_VBG them_PRP to_TO examine_VB the_DT relevant_JJ original_JJ text_NN data_NNS to_TO make_VB sense_NN of_IN any_DT discovered_VBN pattern_NN ._. 
        You_PRP will_MD learn_VB the_DT basic_JJ concepts_NNS ,_, principles_NNS ,_, and_CC the_DT major_JJ techniques_NNS in_IN text_NN retrieval_NN ,_, which_WDT is_VBZ the_DT underlying_VBG science_NN of_IN search_NN engines_NNS ._.