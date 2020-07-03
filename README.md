# SongLyricsSearch
## Getting Started
Download and run <a href="https://www.elastic.co/downloads/elasticsearch">Elasticsearch</a><br>
Install <a href="https://www.elastic.co/guide/en/elasticsearch/plugins/current/analysis-icu.html">ICU Analysis plugin.</a><br>
If You use Kibana for Query operations.You can install and run <a href="https://www.elastic.co/downloads/kibana">Kibana</a><br>

## Setup Index and Mapping

1.First create index and 
```
PUT /lyrics
{
   "settings": {
        "index": {
            "number_of_shards": 1,
            "number_of_replicas": 1
        },
        "analysis": {
            "filter": {
                "n_gram_tockenizer": {
                    "type": "edge_ngram",
                    "min_gram": 2,
                    "max_gram": 15
                },
                "stop_words": {
                    "type": "stop",
                    "stopwords": [
                        "හා",   
                        "හෝ",
                        "ද",
                        "සහ",
                        "ගීත",
                        "ගී",
                        "සින්දු"
                    ]
                }
            },
            "char_filter": {
                "character_filter": {
                    "type": "mapping",
                    "mappings": [
                        "\u200d=>",
                        "\u200B=>",
                        ",=> ",
                        ".=> ",
                        "/=> ",
                        "|=> ",
                        "-=> ",
                        "'=> ",
                        "_=> ",
                        ":=> "

                    ]
                }
            },
            "analyzer": {
                "indexing_analyzer": {
                    "type": "custom",
                    "char_filter": "character_filter",
                    "tokenizer": "icu_tokenizer",
                    "filter": [
                        "n_gram_tockenizer"
                    ]
                },
                "search_analyzer": {
                    "type": "custom",
                    "char_filter": "character_filter",
                    "tokenizer": "icu_tokenizer",
                    "filter": [
                        "stop_words"
                    ]
                }
            }
        }
    },
  "mappings": {
        "properties": {
            "name": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
            
            },
            "artist": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
            
            },
            "genere": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
            
            },
            "lyrics by": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
            
            },
            "music by": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
            
            },
            "key": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
                
            },
            "views": {
                "type": "integer"
                
            },
            "shares": {
                "type": "integer"
            
            },
            "lyrics": {
                "type": "text",
                "analyzer": "indexing_analyzer",
                "search_analyzer":"search_analyzer"
            
            }
        }
    

    }
}
```
2.download <a href="https://github.com/Dhananjana97/SongLyricsSearch/blob/master/SearchComponent/bulk_json_generator/bulk_lyrics_objects.json">Sinhala Song Lyrics dataset</a> and add it to the created index using <a href=https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html>Bulk API</a>

## Setup and Run flask server

1.Activate the virtual environment in SongLyricsSearch/SearchComponent/ .
2.Download and setup  <a href="https://github.com/nlpc-uom/Sinling">Sinling</a> You have to append your project path to path environment variable.otherwise, you can go into the sinling folder and run ``` export PYTHONPATH="$PWD"```.Then you can use sinling, but only in that terminal.
3.run ```flask run```

##Usage Examples




