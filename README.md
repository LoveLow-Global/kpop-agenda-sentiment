# K-Pop Agenda Dynamics: A Comparative Analysis of Topic Diffusion and Sentiment on News and Social Media

**국문 한줄 요약**: 케이팝 관련 기사들을 분야별로 나누고, 분야별로 온라인 커뮤니티/SNS에서 어떻게 반응이 나오는지를 비교한다. 그 후, 커뮤니티/SNS 플렛폼 별 반응에 대해서도 비교한다.

**Target of Analysis**: Top K-pop related articles on [Naver엔터](https://m.entertain.naver.com/series?tab=subject&categoryId=ALL), from 20240101 to 20241231

**Data Source**: News data, Korean SNS platforms such as X(Twitter)[API](https://developer.x.com/en/docs/x-api), DCinside[API?](https://github.com/eunchuldev/dcinside-python3-api), [Instagram](https://github.com/huaying/instagram-crawler).

## Step 1 - Cluster News Articles to Distinct Agenda Topics

### 1.1 - News Data Collection

From Jan 1st, 2024 to Dec 31rd, 2024, the 10 articles with the highest number of daily views were collected. Top [5th article on July 29th](https://m.entertain.naver.com/ranking/article/144/0000978581) and [4th article on Dec 23rd](https://m.entertain.naver.com/ranking/article/312/0000693987) could not be opened and so I just skipped that. Therefore, a total of 3658 articles were collected.

For this task, I first obtained the list of top 10 articles for each day.
[Source code for Ranking Crawler](https://github.com/LoveLow-Global/kpop-agenda-sentiment/blob/main/Step1/Step1-1/ranking_crawler.ipynb)
[list of top10 articles](https://github.com/LoveLow-Global/kpop-agenda-sentiment/blob/main/Step1/metadata.tsv)

Then, I obtained the article texts for the 3658 articles.
[Source code for Content Crawler](https://github.com/LoveLow-Global/kpop-agenda-sentiment/blob/main/Step1/Step1-1/content_crawler.ipynb)
Article texts on only on my computer.

Used Selenium along with
[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) for this. (Dynamic crawling)

Note: Ignore the **Rank** column in the tsv file for now (written 20250220).

### 1.2 - Find news articles with same content

Sort out the news articles with the same content. It is very likely that differnet media companies posted articles with the core information. Example: [Article 1](https://m.entertain.naver.com/ranking/article/382/0001097705) and [Article 2](https://m.entertain.naver.com/ranking/article/312/0000643408) is about the same event. A single company could have also re-posted with a little tweak over time as well. We will sort out the articles with the same core information. This is to focus on the upload time of the 1st news article, as the information diffusion among the public starts then.

$\to$ NER

In this process, I failed to improve accuracy over a certain point. This means that some articles are classified as **different**, even after NER. Therefore, I will manually check all the articles before for better accuracy before starting Step2.

### 1.3 - Topic Modeling

Apply topic modeling on the gathered news articles, used KoBERT.

The research paper below uses LDA(u_mass).

[K-POP 아이돌 그룹의 세대별 이슈 변화 분석 고찰 - 뉴스 빅데이터를 중심으로](https://www-dbpia-co-kr-ssl.access.yonsei.ac.kr/journal/articleDetail?nodeId=NODE11889791),[Topic Granularity & Hallucination LLM Topic Modelling](https://arxiv-org.access.yonsei.ac.kr/abs/2405.00611), 
[multi-granularity learning towards open topic classification](https://www-sciencedirect-com-ssl.access.yonsei.ac.kr/science/article/pii/S0020025521011555), [Granularity of algorithmically constructed publication-level classifications of research publications: Identification of topics](https://arxiv-org.access.yonsei.ac.kr/abs/1801.02466)

## Step 2 - Analysis on the Diffusion of each Article and Sentiment

### 2.1 - Select some news over different topics.

Select the top **8 to 10** most influential news per topic type. (numbers subject to change)

### 2.2 - Analysis

Analyze the user reactions on various websites / SNS platforms. (number of likes, comments, shares)

As most articles regarding K-pop have clear keywords (usually the person / group / company name), we can analyze the articles with these keywords included in the title or text.

$\to$ [Azua](https://github.com/microsoft/project-azua/), [MatchDG](https://www.microsoft.com/en-us/research/publication/domain-generalization-using-causal-matching/)

#### 2.2.1 - Time period Analysis

Analyze the number of the keywords appearing before / after the news article being posted. Check how long it takes for the news to be at its highest attention. On top of that, we can also check the number of changes in the positive / negative word usage around the keywords. (Useful for platforms like DCinside)

$\to$ We can also do this by counting the number of related tags on a SNS platform before / after the news article posted (Useful for platforms like Instagram)

From this, we can draw insights on the distinct agenda topics and their differences when it comes to information diffusion and reactions. We can also **compare the different information diffusion and reactions across different platforms**.

#### 2.2.2 - Example

For example, after the news of 카리나 and 이재욱 dating was first told to the public by 디스패치(company code: 311), we can analyze the number of articles with '카리나' or '재욱' included in the article, and analyze how the numbers of these articles change over time. We can also check the number of changes in the positive / negative word usage in the articles containing '카리나' or '재욱'. This data can be part of the "romance" category. (category name subject to change)

## Step 3 - Comparison Between the Different Diffusion and Sentiment Across Different Topics and Platforms

Comparison based on the results. TBD after checking the amount of data.

Visualization: Charts and graphs to show results, may use Python or R instead as Step 1&2 is likely to be in Python, and R provides great visualization packages. [Plots.jl](https://docs.juliaplots.org/stable/), [Plotly for Julia](https://plotly.com/julia/), [wordcloud for Julia](https://github.com/guo-yong-zhi/WordCloud.jl), [TimeSeries Plotting for Julia](https://juliastats.org/TimeSeries.jl/latest/plotting/)
