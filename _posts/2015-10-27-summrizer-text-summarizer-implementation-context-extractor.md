---
layout: single
title: "Summrizer: Text summarizer (Implementation) & Context Extractor"
date: 2015-10-27T16:52:00+00:00
permalink: /2015/10/summrizer-text-summarizer-implementation-context-extractor.html
categories: jekyll
---

![alt text][screen]

<div dir="ltr" style="text-align: left;">
  <p>
  </p>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Recently, I&#8217;ve been working on implementing a text summarization script in Python (previous blog <a href="http://vipulsharma20.blogspot.in/2015/10/summrizer-text-summarizer.html" rel="nofollow" target="_blank"><span style="color: red;">post</span></a>). I&#8217;ve built a naive implementation of a text summarizer and also a custom Text Context Analyzer which is basically a kind of self-customized Part Of Speech and Noun Phrase tagger which determines that what the content is about i.e. the important context of the text content.</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">For all the impatient folks, TL;DR here is the link to the&nbsp;code : <a href="https://github.com/vipul-sharma20/summrizer"><span style="color: red;">https://github.com/vipul-sharma20/summrizer</span></a></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Please read further for the complete explanation of the implementation.</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><b>NOTE: </b>Works only for English language 🙂</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><i><br /></i> </span>
  </div>
  
  <h2 style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Implementing Summarizing Script</span>
  </h2>
  
  <div>
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">This summary script works well for news articles and blog posts and that&#8217;s the basic motive of implementing this script. It inputs the text content, splits it into paragraphs, splits it into sentences, filter out&nbsp;<a href="https://en.wikipedia.org/wiki/Stop_words" target="_blank"><span style="color: red;">stopwords</span></a>, calculates&nbsp;score&nbsp;<i>(relevance)</i> of each sentence, and on the basis of the scores assigned to each sentence it displays the most relevant results depending upon how concise we want our summary to be.</span>
    </div>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Splitting the content into paragraphs and then to sentence is easier than rest of the tasks so it can be skipped. Before implementing the scoring algorithm, I filtered out the <a href="https://en.wikipedia.org/wiki/Stop_words" rel="nofollow" target="_blank"><span style="color: red;">stopwords</span></a>. Stopwords are the most commonly used words in any language. For example: In English we have words like <i><b>this, that, he, she, I&#8230;</b></i>etc. These are among the most frequently used words in the&nbsp;English language which may not have significance in deciding the importance of a sentence. Therefore, it is required to remove these stopwords from the text content so that the scoring algorithm does not need to score a sentence based on some irrelevant words.</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <h3 style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Scoring</span>
  </h3>
  
  <div>
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">The <a href="https://github.com/vipul-sharma20/summrizer/blob/master/getSummary.py#L14-%23L30" style="color: red; font-style: italic;" target="_blank">scoreSentence()</a><span style="color: red; font-style: italic;">&nbsp;</span>function receives two sentences, finds the intersection between the two i.e. the words/tokens common in both the sentences and then the result is normalized by the average length of the two sentence.</span>
    </div>
    
    <div style="text-align: left;">
      <span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; line-height: 16px; text-align: center; white-space: pre;"><br /></span>
    </div>
    
    <div style="text-align: left;">
      <span style="font-size: large;"><span style="background-color: white; text-align: center;"></span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">avg </span><span style="box-sizing: border-box; color: #a71d5d; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">=</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;"> </span><span style="box-sizing: border-box; color: #0086b3; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">len</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">(s1)</span><span style="box-sizing: border-box; color: #a71d5d; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">+</span><span style="box-sizing: border-box; color: #0086b3; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">len</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">(s2) </span><span style="box-sizing: border-box; color: #a71d5d; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">/</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;"> </span><span style="box-sizing: border-box; color: #0086b3; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">2.0</span></span>
    </div>
    
    <div style="text-align: left;">
      <span style="font-size: large;"><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">score </span><span style="box-sizing: border-box; color: #a71d5d; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">=</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;"> </span><span style="box-sizing: border-box; color: #0086b3; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">len</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">(s1.intersection(s2)) </span><span style="box-sizing: border-box; color: #a71d5d; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;">/</span><span style="background-color: white; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; line-height: 16px; text-align: center; white-space: pre;"> avg</span></span>
    </div>
    
    <div style="text-align: left;">
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;">The most important and interesting part is: how to make use of this scoring algorithm? Here, I&#8217;ve created an all-pair-score-graph of sentences i.e. a completely connected and weighted graph which contains scores between all the pairs of sentences in a paragraph. The function,&nbsp;<i><a href="https://github.com/vipul-sharma20/summrizer/blob/master/getSummary.py#L48-%23L67" target="_blank"><span style="color: red;">sentenceGraph()</span></a> </i>performs this task.</span></span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Suppose <i><b>scoreGraph</b> </i>is the obtained weighted graph. So, <i><b>scoreGraph[0][5]</b></i> will contain the score between sentence no. 1 and sentence no. 6. And similarly, there will be separate intersection score for all the pairs. Therefore, if there are 6 sentences in a paragraph, we will have a <i>6&#215;6</i> matrix as a score-graph.</span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">The <i><b>scoreGraph</b> </i>consist of paired scores. So, to calculate individual score of each sentence, we sum up all the intersection of a particular sentence with the other sentences in the paragraph and store the result in a dictionary with the sentence as the <i>key </i>and the calculated score as the <i>value</i>. The function, <i><a href="https://github.com/vipul-sharma20/summrizer/blob/master/getSummary.py#L70-%23L86" rel="nofollow" target="_blank"><span style="color: red;">build()</span></a> </i>performs this task.</span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
      </div>
    </div>
    
    <h3 style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Summary</span>
    </h3>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">To build the summary from the final score dictionary, we can choose as per our need, depending upon the conciseness of the summary required.</span>
      </div>
    </div>
    
    <div style="text-align: left;">
      </p> 
      
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Complete code of summarizing script : </span><span style="font-size: large;"><i style="font-family: Arial, Helvetica, sans-serif;"><a href="https://github.com/vipul-sharma20/summrizer/blob/master/getSummary.py" rel="nofollow" target="_blank"><span style="color: red;">getSummary.py</span></a></i><span style="font-family: Arial, Helvetica, sans-serif;">&nbsp;</span></span>
      </div>
    </div>
    
    <h3 style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Example</span>
    </h3>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">I&#8217;ve tested the scoring algorithm on a paragraph of an article from techcrunch:</span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <i><b><span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">&#8220;The BBC has been testing a new service called SoundIndex, which lists the top 1,000 artists based on discussions crawled from Bebo, Last.fm, Google Groups, iTunes, MySpace and YouTube. The top five bands according to SoundIndex right now are Coldplay, Rihanna, The Ting Tings, Duffy and Mariah Carey , but the index is refreshed every six hours. SoundIndex also lets users sort by popular tracks, search by artist, or create customized charts based on music preferences or filters by age range, sex or location. Results can also be limited to just one data source (such as Last.fm).&#8221;</span></b></i>
      </div>
    </div>
    
    <div style="text-align: left;">
      <h3 style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Result</span>
      </h3>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: #38761d;">The BBC has been testing a new service called SoundIndex, which lists the top 1,000 artists based on discussions crawled from Bebo, Last.fm, Google Groups, iTunes, MySpace and YouTube : </span><span style="color: #660000;">0.338329361595</span></span>
      </div>
      
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: #660000;"><br /></span></span>
      </div>
    </div>
    
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: #38761d;">The top five bands according to SoundIndex right now are Coldplay, Rihanna, The Ting Tings, Duffy and Mariah Carey , but the index is refreshed every six hours. : </span><span style="color: #660000;">0.286057692308</span></span>
    </div>
    
    <p>
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"></span>
    </p>
    
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: #38761d;"><br /></span></span>
    </div>
    
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: #38761d;">SoundIndex also lets users sort by popular tracks, search by artist, or create customized charts based on music preferences or filters by age range, sex or location. : </span><span style="color: #660000;">0.285784751456</span></span>
    </div>
    
    <p>
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"></span>
    </p>
    
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: #38761d;">Results can also be limited to just one data source (such as Last.fm). : </span><span style="color: #660000;">0.237041838857</span></span>
    </div>
    
    <p>
    </p>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">As per the context of the news, it is evident that the first two sentences are the most relevant part of the paragraph and hence have higher score than the rest of the sentences.</span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
      </div>
    </div>
    
    <div style="text-align: left;">
      <div style="text-align: justify;">
        <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Speaking of Coldplay, I highly recommend :&nbsp;<span style="color: red;"><a href="https://www.youtube.com/watch?v=5gvofiXHbUI" rel="nofollow" target="_blank"><span style="color: red;"><b>Coldplay &#8211; Fix You (Live 2012 from Paris)</b></span></a>&nbsp;</span>😀</span><br /><span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span></p> 
        
        <h3>
          <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Comparison</span>
        </h3>
        
        <p>
          <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">I&#8217;ve tried various text compacting and text summarizing websites and used the above paragraph to test their performance and here are the results:</span>
        </p>
        
        <ul>
          <li>
            <span style="font-family: Arial, Helvetica, sans-serif;"><span style="color: red; font-size: large;"><a href="http://autosummarizer.com/index.php"><span style="color: red;">http://autosummarizer.com/index.php</span></a>&nbsp;</span><span style="font-size: large;">summarized it to <span style="color: #38761d;"><i>&#8220;<span style="line-height: 25.666667938232422px; text-align: center;">Sound Index also lets users sort by popular tracks, search by artist, or create customized charts based on music preferences or filters by age range, sex or location.</span>&#8220;</i></span></span></span>
          </li>
          <li>
            <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><a href="http://freesummarizer.com/"><span style="color: red;">http://freesummarizer.com</span></a> summarized it to <span style="color: #38761d;"><i>&#8220;</i><span style="background-color: white; line-height: 22px; text-align: left;"><i>SoundIndex also lets users sort by popular tracks, search by artist, or create customized charts based on music preferences or filters by age range, sex or location.</i></span></span><i><span style="color: #38761d;">&#8220;</span></i></span>
          </li>
          <li>
            <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><a href="http://smmry.com/"><span style="color: red;">http://smmry.com</span></a> did nothing but just converted the paragraph into sentences and displayed them 😐</span>
          </li>
          <li>
            <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="color: red;"><a href="http://textcompactor.com/"><span style="color: red;">http://textcompactor.com</span></a> </span>summarized it to the following when I set 50 % for summary limit:&nbsp;<span style="color: #38761d;"><i>&#8220;<span style="background-color: white; text-align: start;">The BBC has been testing a new service called SoundIndex, which lists the top 1,000 artists based on discussions crawled from Bebo, Last.fm, Google Groups, iTunes, MySpace and YouTube. The top five bands according to SoundIndex right now are Coldplay, Rihanna, The Ting Tings, Duffy and Mariah Carey , but the index is refreshed every six hours.</span>&#8220;</i></span></span>
          </li>
        </ul>
      </div>
    </div>
    
    <div style="text-align: left;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><span style="text-align: justify;"><a href="http://textcompactor.com/" style="text-align: justify;"><span style="color: red;">http://textcompactor.com</span></a>&nbsp;produced the same result as my script when used for 50% compaction limit</span></span><span style="color: red; font-family: Arial, Helvetica, sans-serif; text-align: justify;">&nbsp;</span><span style="font-family: Arial, Helvetica, sans-serif; font-size: large; text-align: justify;">😀 others were pretty disappointing.</span><br /><span style="font-family: Arial, Helvetica, sans-serif; font-size: large; text-align: justify;"><br /></span><span style="font-family: Arial, Helvetica, sans-serif; font-size: large; text-align: justify;">Try copy-pasting the paragraph used in the example to verify the results.</span>
    </div>
    
    <h2 style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Context Extractor</span>
    </h2>
  </div>
  
  <div>
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">The summarizing script, as explained above, works on top of a scoring algorithm. One might need to extract the only the context or the main topics from a sentence so as to know what the text content is about. This provides a very abstract idea about the content which we might be dealing with.</span>
    </div>
  </div>
  
  <div>
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
    </div>
  </div>
  
  <div>
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">The phrase structure of a sentence in English is of the form:</span>
    </div>
  </div>
  
  <div>

    <dl style="color: #252525; line-height: 22px; margin-bottom: 0.5em; margin-top: 0.2em;">
      <dd style="margin-bottom: 0.1em; margin-left: 1.6em; margin-right: 0px; text-align: center;">
        <div style="text-align: center;">
          <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><img alt="S to NP quad VP" class="mwe-math-fallback-image-inline tex" height="23" src="http://138.68.252.233/wp-content/uploads/2015/10/f1d5f6f249c1a8bba0bb0c78afbadb55.png" style="border: none; display: inline-block; vertical-align: middle;" width="200" /></span>
        </div>
      </dd>
    </dl>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">The above rule means that a sentence (S) consists of a <a href="https://en.wikipedia.org/wiki/Noun_phrase" rel="nofollow" target="_blank"><span style="color: red;">Noun Phrase</span></a> (NP) and a <a href="https://en.wikipedia.org/wiki/Verb_phrase" rel="nofollow" target="_blank"><span style="color: red;">Verb Phrase</span></a> (VP). We can further define grammar for a Noun Phrase but let&#8217;s not get into that 🙂</span>
  </div>
  
  <p>
  </p>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">A Verb Phrase defines the action performed on or by the object whereas a Noun Phrase function as verb subject or object in a sentence. Therefore, NP can be used to extract the important topics from the sentences.</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">I&#8217;ve used Brown Corpus in Natural Language Toolkit (NLTK) for Part Of Speech (POS) tagging of the sentences and defined custom Context Free Grammar (CFG) for extracting NP.</span>
  </div>
  
  <blockquote>
    <div style="text-align: center;">
      <span style="color: #38761d; font-family: Arial, Helvetica, sans-serif; font-size: large;"><b>&#8220;The Brown Corpus was the first million-word electronic corpus of English, created in 1961 at Brown University. This corpus contains text from 500 sources, and the sources have been categorized by genre, such as&nbsp;<em>news</em>,&nbsp;<em>editorial</em>, and so on.&#8221;</b></span>
    </div>
  </blockquote>
  
  <p>
    <span style="font-family: Arial, Helvetica, sans-serif;">See more at: <a href="http://www.nltk.org/book/ch02.html#brown-corpus" rel="nofollow" target="_blank"><span style="color: red;">NLTK-Brown Corpus</span></a></span>
  </p>
  
  <blockquote>
    <div style="text-align: justify;">
      <span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;">A part-of-speech tagger, or&nbsp;<span style="font-weight: bold;">POS-tagger</span>, processes a sequence of words, and attaches a part of speech tag to each word</span><a href="https://www.blogger.com/blogger.g?blogID=3213730204187539187" name="pos_tagger_index_term"><br /></a></span>
    </div>
    
    <table border="0" cellpadding="0" cellspacing="0" style="border-bottom-color: gray; border-bottom-style: solid; border-bottom-width: 1px; border-top-color: gray; border-top-style: solid; border-top-width: 1px; margin: 0px; padding: 0px; width: 95%px;">
      <tr>
        <td style="background-color: #eeeeff; border-color: gray; border-style: solid; border-width: 0px 2px 1px 1px; font-weight: bold; margin: 0px; padding: 0.2em;">
          <table border="0" cellpadding="0" cellspacing="0" style="width: 100%px;">
            <tr>
              <td style="padding-left: 0.5em;">
                <pre style="font-weight: bold; margin: 0px; padding: 0px;"><span style="color: #9b0000;">&gt;&gt;&gt; </span>text = word_tokenize(<span style="color: #00aa00;">"And now for something completely different"</span>)<br /><span style="color: #9b0000;">&gt;&gt;&gt; </span>nltk.pos_tag(text)<br /><span style="color: blue;">[('And', 'CC'), ('now', 'RB'), ('for', 'IN'), ('something', 'NN'),</span><br /><span style="color: blue;">('completely', 'RB'), ('different', 'JJ')]</span></pre>
              </td>
            </tr>
          </table>
        </td>
      </tr>
    </table>
  </blockquote>
  
  <p>
    <span style="font-family: Arial, Helvetica, sans-serif;">See more at: <a href="http://www.nltk.org/book/ch05.html#using-a-tagger" rel="nofollow" target="_blank"><span style="color: red;">NLTK-Using a Tagger</span></a></span><br /><span style="font-family: Arial, Helvetica, sans-serif;"><br /></span>
  </p>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">In my context extractor&nbsp;script, I&#8217;ve used unigram as well as bigram POS tagging. A unigram tagger is based on a simple statistical algorithm: For every token/word assign a tag that is more likely for that token/word which is decided as per the lookup match found in the trained data. The drawback of unigram tagging is, we can just tag a token with a &#8220;most likely&#8221; tag in isolation with the larger context of the text.</span><br /><span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Therefore, for better results we use an <i>n-gram</i> tagger, whose context is current token along with the POS tags of preceding <i>n-1 </i>tokens. The problem with n-gram taggers is <i>sparse data</i> problem which is quite immanent in NLP.</span>
  </div>
  
  <p>
  </p>
  
  <blockquote>
    <div style="text-align: center;">
      <span style="color: #38761d; font-family: Arial, Helvetica, sans-serif; font-size: large;"><b>&#8220;As&nbsp;<em>n</em>&nbsp;gets larger, the specificity of the contexts increases, as does the chance that the data we wish to tag contains contexts that were not present in the training data.&#8221;</b></span>
    </div>
  </blockquote>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span> <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Even for <i>n=2</i> i.e. in case of a bigram tagger we can face this <i>sparse data</i> problem. Therefore to avoid this, I&#8217;ve initially used a Bigram Tagger and if it fails to tag some tokens, it backs off to the Unigram Tagger for tagging and if even the Unigram Tagger fails to tag the tokens, it backs off to a RegEx Tagger which has some naive rules for tagging nouns, adjectives, cardinal numbers, determinants etc.</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;">I&#8217;ve also defined a <a href="https://github.com/vipul-sharma20/summrizer/blob/master/context.py#L24-%23L30" rel="nofollow" target="_blank"><span style="color: red;">custom CFG</span></a> (<a href="https://www.cs.rochester.edu/~nelson/courses/csc_173/grammars/cfg.html" rel="nofollow" target="_blank"><span style="color: red;">Context Free Grammar</span></a>) to extract Noun Phrases from the POS tagged list of tokens.</span></span><br /><span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;"><b><i>(I can discuss how the custom CFG works if someone is interested 🙂 ! )</i></b></span></span><br /><span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;"><br /></span></span> <span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;">Here is the code which performs this task : <i><a href="https://github.com/vipul-sharma20/summrizer/blob/master/context.py" rel="nofollow" target="_blank"><span style="color: red;">context.py</span></a></i></span></span></p> 
    
    <h3>
      <span style="font-family: Arial, Helvetica, sans-serif;"><span style="font-size: large;">Example</span></span>
    </h3>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">I&#8217;ve used the same content as used in the summarizer script as the test example for context extracting script:</span>
  </div>
  
  <p>
  </p>
  
  <div style="text-align: justify;">
    <i><b><span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">&#8220;The BBC has been testing a new service called SoundIndex, which lists the top 1,000 artists based on discussions crawled from Bebo, Last.fm, Google Groups, iTunes,&nbsp;MySpace&nbsp;and YouTube. The top five bands according to SoundIndex right now are Coldplay, Rihanna, The Ting Tings, Duffy and Mariah&nbsp;Carey ,&nbsp;but the index is refreshed every six hours. SoundIndex also lets users sort by popular tracks, search by artist, or create customized charts based on music preferences or filters by age range, sex or location. Results can also be limited to just one data source (such as Last.fm).&#8221;</span></b></i>
  </div>
  
  <p>
  </p>
  
  <div style="text-align: justify;">
  </div>
  
  <h4 style="text-align: justify;">
    <b><span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Result</span></b>
  </h4>
  
  <div style="text-align: justify;">
    <span style="color: #38761d; font-family: Arial, Helvetica, sans-serif; font-size: large;">[&#8216;BBC&#8217;, &#8216;new service&#8217;, &#8216;SoundIndex&#8217;, &#8216;Bebo&#8217;, &#8216;Last.fm&#8217;, &#8216;Google Groups&#8217;, &#8216;MySpace&#8217;, &#8216;YouTube&#8217;, &#8216;SoundIndex&#8217;, &#8216;Coldplay&#8217;, &#8216;Rihanna&#8217;, &#8216;Ting Tings&#8217;, &#8216;Duffy&#8217;, &#8216;Mariah Carey&#8217;, &#8216;SoundIndex&#8217;, &#8216;lets users sort&#8217;, &#8216;popular tracks&#8217;, &#8216;music preferences&#8217;, &#8216;age range&#8217;, &#8216;data source&#8217;, &#8216;Last.fm&#8217;]</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="color: #38761d; font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">This is the list of topics discussed in the test paragraph which looks good :D. NLP can never yield 100% accurate results. All we can do is train using the data set therefore in this case, some undesired results may arise.</span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;"><br /></span>
  </div>
  
  <div style="text-align: justify;">
    <span style="font-family: Arial, Helvetica, sans-serif; font-size: large;">Please suggest me some improvements 🙂 I would love to hear your views 😀</span>
  </div>
</div>

[screen]: /assets/images/screen.jpg
