import re
text=open(r"WhatsApp Chat with Jagyaseni.txt","r")
contents=text.read()
contents=contents.lower()
con=contents.split()
con1=re.sub(r"[.,'\?!-]",'',contents)
con1=re.sub(r"\d{2}/\d{2}/\d{2}",'',con1)
con1=re.sub(r"\n",'',con1)
con1=re.sub(r"\d{2}:\d{2}\s[a-z]{2}",'',con1)
con1=re.sub(r"raktim dey:|jagyaseni:",'',con1)
con1=con1.split(" ")
wr=["I","how","yes","yeah","okay","<media","omitted>","pm","am","e","er","na","ta","ki","toh","ekta",
    "kore","ami","tui","amar","theke"]
con1=[i for i in con1 if i not in STOPWORDS if i not in wr]
import pandas as pd
c=pd.Series(con1).value_counts()
import matplotlib.pyplot as plt
from wordcloud import WordCloud,STOPWORDS

#Generate word frequencies
word_freq = c

#Generate word cloud
wc = WordCloud(width=400, height=330, max_words=100, background_color='white').generate_from_frequencies(word_freq)

plt.figure(figsize=(12, 8))
plt.imshow(wc, interpolation='bilinear')
plt.axis('off')
plt.show()
