# Preprocessing Text Python Package

This python package is prepared by Simhadri Madhuri.

Dependencies
```
import sys
!{sys.executable} -m pip install spacy
!{sys.executable} -m spacy download en

pip install beautifulsoup4==4.9.1
pip install textblob==0.15.3
```

Install

`pip install git+https://github.com/smadhuri1993/preprocess_kgptalkie.git --upgrade --force-reinstall`

Uninstall

`pip uninstall preprocess_kgptalkie`

#### How to use it for preprocessing
You have to have installed spacy and python3 to make it work.

```
def get_clean(x):
    x = str(x).lower().replace('\\', '').replace('_', ' ')
    x = ps.cont_exp(x)
    x = ps.remove_emails(x)
    x = ps.remove_urls(x)
    x = ps.remove_html_tags(x)
    x = ps.remove_rt(x)
    x = ps.remove_accented_chars(x)
    x = ps.remove_special_chars(x)
    x = re.sub("(.)\\1{2,}", "\\1", x)
    return x
```

Use this if you want to use one by one
```
import pandas as pd
import numpy as np
import preprocess_kgptalkie as ps

df = pd.read_csv('imdb_reviews.txt', sep = '\t', header = None)
df.columns = ['reviews', 'sentiment']

# These are series of preprocessing
df['reviews'] = df['reviews'].apply(lambda x: ps.cont_exp(x)) #you're -> you are; i'm -> i am
df['reviews'] = df['reviews'].apply(lambda x: ps.remove_emails(x))
df['reviews'] = df['reviews'].apply(lambda x: ps.remove_html_tags(x))
df['reviews'] = df['reviews'].apply(lambda x: ps.remove_urls(x))

df['reviews'] = df['reviews'].apply(lambda x: ps.remove_special_chars(x))
df['reviews'] = df['reviews'].apply(lambda x: ps.remove_accented_chars(x))
df['reviews'] = df['reviews'].apply(lambda x: ps.make_base(x)) #ran -> run, 
df['reviews'] = df['reviews'].apply(lambda x: ps.spelling_correction(x).raw_sentences[0]) #seplling -> spelling
```
