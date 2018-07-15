# Write Custom Function

MeTa is modular software written is C++. We can write [custom filter chain](https://meta-toolkit.org/analyzers-filters-tutorial.html) by modifying configuration file or hard coding. By default, MeTa provides `analyzer` module that can execute chain filter task. The `analyzer` method can be called in two way:

1. Through configuration file called as `config.toml`:
```
[[analyzers]]
method = "METHOD_NAME"
// METHOD_PARAMETERS
    [[analyzers.filter]]
    type = "FILTER_TYPE"
    // FILTER_PARAMETERS
```
2. Through custom function:
```
#include "meta/analyzers/analyzer.h"
#include "meta/analyzers/filters/all.h"
#include "meta/analyzers/ngram/ngram_word_analyzer.h"
#include "meta/analyzers/tokenizers/icu_tokenizer.h"

using namespace meta::analyzers;
std::unique_ptr<token_stream> stream =
    make_unique<tokenizers::YOUR_TOKENIZER>();
stream = make_unique<filters::YOUR_FILTER1>(std::move(stream));
stream = make_unique<filters::YOUR_FILTER2>(std::move(stream));

stream->set_content(STREAM_OBJECT);
```


## Write filter chain function: Stop word removal and then stemming

Here, we want to create filter chain function that do stopword removal then stemming using Porter2 algorithm:

1. Include required libraries:

    ```
    #include "cpptoml.h"
    #include "meta/analyzers/analyzer.h"
    #include "meta/analyzers/filters/all.h"
    #include "meta/analyzers/ngram/ngram_word_analyzer.h"
    #include "meta/analyzers/tokenizers/icu_tokenizer.h"
    ```
    note that `cpptoml.h` contains `cpptoml` module that read toml file into c++ object.

2. Declaring a new function called `stopstem()` that accept a path of document file:

    ```
    void stopstem(const std::string& file, const cpptoml::table& config) {
        // Logic will discussed in the next steps
    }
    ```
    assume that `config` parameter will be assigned automatically by `main()` method by calling `auto config = cpptoml::parse_file(CONFIG_FILE_PATH);`.

3. Use `analyzer` namespace:

    ```using namespace meta::analyzers;```

4. Get list of stopwords from config file:

    ```auto stopwords = config.get_as<std::string>("stop-words");```

5. Implement tokenizer method to create bag of words:
    
    ```std::unique_ptr<token_stream> stream = make_unique<tokenizers::icu_tokenizer>();```
    note that bag of words is pointer of unique word token.

6. Apply lowercase filter:

    ```stream = make_unique<filters::lowercase_filter>(std::move(stream));```

7. Apply stopwords removal filter by scanning each word:

    ```stream = make_unique<filters::list_filter>(std::move(stream), *stopwords);```

8. Apply stemming filter using Porter2 algorithm:

    ```stream = make_unique<filters::porter2_filter>(std::move(stream));```

9. Apply empty sentence filter that remove empty line or empty string:
    
    ```stream = make_unique<filters::empty_sentence_filter>(std::move(stream));```

10. Here the complete code that do stopword removal and stemming for given document and save it as new document file:

    ```
    template <class Stream>
    void write_file(Stream& stream, const std::string& in_name,
                    const std::string& out_name) {
    std::ofstream outfile{out_name};
    stream->set_content(filesystem::file_text(in_name));
    while (*stream) {
        auto next = stream->next();
        if (next == "<s>" || next == " ")
        continue;
        else if (next == "</s>")
        outfile << std::endl;
        else
        outfile << next << " ";
    }
    }

    void stopstem(const std::string& file, const cpptoml::table& config) {
    std::cout << "Running stopword removal and stemming" << std::endl;

    using namespace meta::analyzers;
    auto stopwords = config.get_as<std::string>(
        "stop-words");  // Reads the stop words from file
    std::unique_ptr<token_stream> stream =
        make_unique<tokenizers::icu_tokenizer>();
    stream = make_unique<filters::lowercase_filter>(std::move(stream));
    // Insert the line required to do stopword removal here
    stream = make_unique<filters::list_filter>(std::move(stream), *stopwords);
    // Insert the line required to do stemming here (using Porter2 Stemmer)
    stream = make_unique<filters::porter2_filter>(std::move(stream));
    stream = make_unique<filters::empty_sentence_filter>(std::move(stream));

    auto out_name = no_ext(file) + ".stopstem.txt";
    write_file(stream, file, out_name);
    std::cout << " -> file saved as " << out_name << std::endl;
    }
    ```