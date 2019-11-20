# BigdataTopics

Proyecto desarrollado en AWS + Notebooks (Jupiter)
Dataset:https://www.kaggle.com/snapcrack/all-the-news

Analitica:
* Análisis de sentimientos
* Generación automáticas de keyworks

Librerias de apoyo:
* NLTK
* Pandas
* Textblob

### 1.Carga de datos
Datos cargados y subidos mediante S3 de manera publica:
:

    s3://sortizcdataset/DatasetFinal/articles1.csv
    s3://sortizcdataset/DatasetFinal/articles2.csv
    s3://sortizcdataset/DatasetFinal/articles3.csv

### 2.Preparacion de datos
* 2.1: Elminacion de caracteres especiales:
::

    def remove_punctuation(text):  
    
        no_punc = "".join([c for c in text if c not in string.punctuation])
        no_punc = re.sub('[^A-Za-z0-9’\w\s]', '', no_punc)
        no_punc = re.sub('[’]',' ', no_punc)
        return no_punc   
        
    pandas_df['content'] = pandas_df['content'].apply(lambda x: remove_punctuation(str(x).lower()))


* 2.2: Eliminacion de Stopwords: 
: :

    stopwords = ['i', 'me'.....]    
    def remove_stopwords(text):
    
        words = [w for w in text if w not in stopwords]
        return words
    pandas_df['content'] = pandas_df['content'].apply(lambda x: remove_stopwords(x))
    
    
* 2.3: Eliminacion de "palabras" de 1 letra:

    def delete_lenght(text):
    
        words = []
        for x in text:
            if len(x) > 1:
                words.append(x)
        return words
        
    pandas_df['content'] = pandas_df['content'].apply(lambda x: delete_lenght(x))
    
 * 2.4: Stemmizer / Lemmatizer
 ::
 
       def word_lemmatizer(text):
          words = []
          for x in text:
              words.append(str(Word(x).lemmatize()))
          return words
       #Stemmizer
         pandas_df['content']=pandas_df['content'].apply(lambda x: [stemmer.stem(y) for y in x])
         #pandas_df['content']=pandas_df['content'].apply(lambda x: [porter_stemmer.stem(y) for y in x])

       #lemmatizer
         #pandas_df['content'] = pandas_df['content'].apply(lambda x: word_lemmatizer(x))
         
  * 3 : tokenizar
  ::
  
    pandas_df['content'] = pandas_df['content'].apply(lambda x: tokenizer.tokenize(x.lower()))
    
* Analisis de datos
  

### Marco De referencia

https://unipython.com/analisis-de-sentimientos-con-textblob-y-vader/
https://towardsdatascience.com/interactive-visualizations-in-jupyter-notebook-3be02ab2b8cd
https://towardsdatascience.com/why-you-should-avoid-removing-stopwords-aa7a353d2a52
https://towardsdatascience.com/nlp-for-beginners-cleaning-preprocessing-text-data-ae8e306bef0f
  
