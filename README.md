### Natural language processing (NLP)
### Author: 
Zhaojie Chen (zc153) 
TJ Tang (tt238) 
Elena Wang (xnw3) 
Chihui Shao (cs662) 
Qin He (qh58) 
Mingxuan Wang (mw466)
### Introduction
We are thinking of using Python to conduct text analysis. The targets for our product are college students who are struggling with literature or other scholarly articles.Some methods we may consider (inspired from https://www.machinelearningplus.com/nlp/text-summarization-approaches-nlp-example/):
-         TextRank: It is based on the concept that words which occur more frequently are significant.
-         LexRank: A sentence that is similar to many other sentences of the text has a high probability of being important.
-         LSA (Latent semantic analysis): It extracts semantically significant sentences by applying singular value decomposition (SVD) to the matrix of term-document frequency.
-         Luhn Summarization (Term Frequency-Inverse Document Frequency: It is useful when very low frequent words, as well as highly frequent words (stopwords), are both not significant.
-         KL-Sum: It selects sentences based on similarity of word distribution as the original text.Given a text, we decide to first adopt some scoring schemes to compare different algorithms, and then select one or a few optimal algorithms to perform text analysis. The scoring schemes can be based on the user’s input. For example, in Grammarly, users need to set “goals,” including audience, formality, domain, etc. We may also need to decide the output format for the summarization.
For each test case, we are going to compare the summary texts generated by algorithms with the summaries written by humans. And to see if algorithms like BLEU and ROUGE can be used for evaluations. The attached page can be a direction to start with. 
https://stackoverflow.com/questions/9879276/how-do-i-evaluate-a-text-summarization-tool

### The PRFAQ document comprises a Press Release (PR) and a Frequently Asked Questions (FAQ) section.
### PR:
A group of Duke graduate students aims to reduce college students’ workload through artificial intelligence.
Durham NC—April 23, 2022—Today 6 Duke graduate students from Biostatistics,  Computer Science, and Statistical Science department prototyped a computer-aided text summarization system called “Summary Devil” that uses state-of-the-art methods in machine learning and natural language processing to help people extract information from long text documents. Especially, the system is intended to help college students with a heavy workload of required readings. The users can upload any document which they want to obtain summaries, including literature articles, prose fiction, and news. The system has an automated pipeline to process and parse the text uploaded and generated summaries. Users can expect auto-generated summaries comparable to those written by human experts. 
Under many circumstances, reading is enjoyable and can reduce stress to some extent. However, for students who are taking courses with a long weekly reading assignment, it is another story. In fact, many of the articles are not written for educational purposes in the first place, and hence their authors may not have the intention to express their idea directly. They may choose to include delicate expressions and detailed descriptions for aesthetical, political, or commercial purposes. Take novels as an example. Authors may intend to provide readers with descriptions of the background before the story begins. Therefore, readings can sometimes be unnecessarily verbose and therefore tedious to read. Spending a prolonged period of time reading documents could increase the stress level of students and impede their learning of other subjects.
Many existing resources provide summaries written by experts. However, there are several drawbacks of human-written summaries. Firstly, people can be biased by their own experiences, education level, and political viewpoint when reading, and these biases are later reflected in the summaries. In addition, only famous works that have been published for a long time are likely to have well-written summaries. It should be easy to find multiple resources if you want a summary of Shakespeare’s *The Tragedy of Macbeth*, but it may not be the case if you are looking for a summary of a book published last week, or a news article just released. All these issues mentioned above can be resolved by a system that automatically generates summaries. As the system purely algorithmically extracts information from the original document, it is not likely that the generated text includes biases. Moreover, users can choose any document and obtain its summary immediately. It does not have to be long-existing and well-recognized articles, and in fact, it can be an article that is finished seconds ago before being uploaded to the system. It provides users with more flexible resources for obtaining summaries.
### FAQs:
#### What is the highlight of your product?
Given a single text, our product will generate not only one summary but four different summaries. Therefore, users can easily find and pick the summary that fits their demand well.
#### What are the methods being used in your product?
The methods we considered are Luhn, KL-Sum, LSA, and TextRank. They are from the Sumy package in Python, which is used for the automatic summarization of text documents. Here are some brief introductions to our methods:
- Luhn Summarization finds the sentences that contain the most information based on the keyword in the sentences. 
- KL-Sum selects sentences based on the similarity of word distribution to the original text.
- LSA (Latent semantic analysis) extracts semantically significant sentences by applying singular value decomposition (SVD) to the matrix of term-document frequency. 
- TextRank is based on the concept that words which occur more frequently are significant
See Technical Details for methods details.
#### Do you think your product will help college students?
We would say that our product can only be served as a guide for readings but never a substitute for readings, especially for novels and other literature. Our product can only help people get a basic idea of the contents. However, the summary will not capture literary elements such as rhetorical devices. Therefore, we strongly recommend college students to read the full text as well, rather than only relying on our product. 
#### What is the target population for your product?
The main target population is college students who are struggling with readings for general requirement courses. When I was a freshman at college, I always struggled with reading novels for the literature course and reading news for the journalism course. Therefore, our team came up with an idea to develop a study tool for college students. Additionally, some people may be too busy to read the full news articles, so our product will also be beneficial to them.
#### What are the evaluation tools for comparing different methods?
We mainly used ROUGE as a tool to compare an automatically produced summary against a humanproduced summary. Besides that, we also considered the length of the summary. Certain users care about the time spent on the reading. They may just want to get a very basic about what is going on in the news when they are preparing for breakfast. However, some readers may want to get enough information out of the summaries. So, they may prefer longer summaries.
#### What is ROUGE and how does it work?
We used ROUGE, or Recall-Oriented Understudy for Gisting Evaluation as an important evaluation tool. ROUGE is a set of metrics that compare an automatically produced summary against a human produced summary. Among all metrics in ROUGE, we considered the below metrics.
- ROUGE-1 measures the overlap of each word between the system and reference summaries. 
- ROUGE-L measures the Longest Common Subsequence (LCS) based statistics, which considers sentence-level structure similarity naturally and identifies the longest co-occurring in sequence N-grams automatically.
ROUGE will measure precision, recall, and F-score. In ROUGE, precision measures how much of the automatically produced summary is relevant or needed, which is computed as the percentage of overlapping words in the machine-generated summary. On the other hand, recall means how much of the reference summary is the automatically produced summary recovering, which can be computed as the percentage of overlapping words in the reference summary. And F-score combines precision and recall together.
See Technical Details for methods details
#### What are the pros and cons of different methods?
From the character count perspective, given the same number of sentences counts, LSA will give the shortest summaries, and then TextRank. Both Luhn and KLSum will output much longer summaries. In terms of ROUGE, for A Tale of Two Cities, which is a historical novel, different methods have similar results and TextRank is a little bit better. For The Five Orange Pips, which is a fictional novel, Luhn and TextRank are better than the other two methods. For 1984, which is a political science fiction novel, KL-SUM, LSA, and TextRank are much better than Luhn. For news articles and blog articles, overall speaking, Luhn is the worst but there are some case-by-case variations. Luhn will give long summaries so we may expect that it does not have a good performance in ROUGE. However, Luhn tends to extract the most information, which might be useful in certain cases. TextRank selects words that are more frequent. So, we can also see that TextRank does a good job in terms of ROUGE and generates shorter summaries. But generally speaking, different people might have different demand for our products, so we cannot say one of the methods outperform the rest.
See Technical Details for preliminary results. 
#### Have you tested your product? And what is the feedback from users who already have used your product?
Yes, some developers in our team and some volunteers have tried out our project. We generated summaries using all four methods. To make the test objective, the volunteers do not know which summary paragraph is generated from which method. The articles to test are the first chapter of 1984, the first chapter of A Tale of Two Cities, and The Five Orange Pips. One of the volunteers preferred  TextRank and he thought the worst of them is LSA. He argued that LSA only extracted some highlights of the article rather than providing a detailed summary of the text, while TextRank did a good job of summarizing. However, some volunteers give different feedbacks that they ranked the methods from the best to worst as LSA, TextRank, KLSum, and Luhn. And their criterion is that the summaries generated by KLSum and Luhn are long and hard to digest. So, we think different audiences may have different preferences. So, we will provide some brief descriptions of our methods, and ROUGE and character count metrics, but eventually it is up to the users to pick the one they like the most. 
See Technical Details for model details and preliminary results.
#### What might be your future development of this product?
We have not tested our product on scholarly publications in natural and social sciences. Also, we are thinking if we could incorporate more evaluation metrics to help our users to pick the best method according to their demands. In addition, our product currently only supports article summaries in text format and does not support article summaries in pdf format. Many articles are now presented on the Internet in the form of pdf, and we also want to provide a function that can convert pdf to text form and summarize in the future.
#### Do you think that your product has long-term development?
Our team believes that our product has a bright prospect. The word Artificial Intelligence has already become more and more popular in our life. As Web 3.0 developed, everything will tend to be conducted by individuals rather than companies, which means that the user has more autonomy in our new era. Therefore, more and more information will be directly posted and spread faster and faster online. People would be willing to gain the information simpler and quicker, which is one of the reasons why Tiktok and Meta is popular recently. We believe that our product would bring a similar development to face this new age. 
#### Do you think that your team would use this product to make a living?
All we have done is just non-profit and just want to contribute to our society, especially, aim to reduce high-intensity study pressure. However, as I said in the last question, Web 3.0 would allow people to directly make money online, which means that we could get some benefits from that. For example, people who are using our product could get some coins, and with our reputation becoming better, we also could get more advertisement payback.
#### What will be considered plagiarism when people use your products in reading reports or other essays?
Our product is only a study guide to let people understand the texts. Therefore, people need to cite and acknowledge when they referred the contents of the summaries generated by our product.
### Technical details/preliminary results:
See the attached Python codes.
### References:
Sharma et al., “Evaluation of Python Text Summarization Libraries,” IJEDR 2021, Volume 9, Issue 1 Shrivarsheni, “Text Summarization Approaches for NLP – Practical Guide with Generative Examples,” October 2020. 
https://www.machinelearningplus.com/nlp/text-summarization-approaches-nlp-example/
The references for codes and implementation of our product are included in the attached Python codes.
