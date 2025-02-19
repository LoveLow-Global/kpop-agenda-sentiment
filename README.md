# K-Pop Agenda Dynamics: A Comparative Analysis of Topic Diffusion and Sentiment on News and Social Media
# Comparative Dynamics of K-Pop News Agenda Setting and Social Media Sentiment

**국문 한줄 요약**: 케이팝 관련 기사들을 분야별로 나누고, 분야별로 온라인 커뮤니티/SNS에서 어떻게 반응이 나오는지를 비교한다. 그 후, 커뮤니티/SNS 플렛폼 별 반응에 대해서도 비교한다.

**Target of Analysis**: K-pop related articles, from 20240101 to 20241231

**Data Source**: News data, Korean SNS platforms such as X(Twitter), DCinside, Instagram.

## Step 1 - Cluster News Articles to Distinct Agenda Topics

### 1.1 - Data Collection

Collect data from various articles. 총 3658개의 기사를 수집했고, 2024년 1월 1일부터 2024년 12월 31일까지 매일 올라온 기사중, 일간 조회수가 가장 높은 10개의 기사를 매일 수집했다. 7월29일과 12월23일의 Top 10 기사중에서는 (각각 1개씩) 열리지 않는 기사가 있어서, 생략했다.

$\to$ Data Collection method는 [A Topic Agenda Setting Model]을 참고

[Naver엔터](https://m.entertain.naver.com/series?tab=subject&categoryId=ALL)

Extract text data from the news articles.

Selenium,
[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

### 1.2 - Find news articles with same content

Sort out the news articles with the same content. It is very likely that differnet media companies posted articles with the same content. A single company could have also re-posted with a little tweak over time as well. We focus on the time of the 1st news article.

$\to$ Find a way to do this process, search for Korean NLP packages such as [KoNLPy](https://konlpy.org/en/latest/),

### 1.3 - Topic Modeling

Apply topic modeling on the gathered news articles such as LDA, NMF, BERTopic, or recent transformer-based methods.

$\to$ 토픽 모델링에 대한 공부 필요

These topics include topics such as new releases, romance, fashion, chart results.
[K-POP 아이돌 그룹의 세대별 이슈 변화 분석 고찰 - 뉴스 빅데이터를 중심으로](https://www-dbpia-co-kr-ssl.access.yonsei.ac.kr/journal/articleDetail?nodeId=NODE11889791) << LDA로 6개로 나눔

$\to$ Topic Granularity는 어느 정도로 할지에 대해서(예를 들어서 new release도 데뷔, 컴백 등으로 구분) 위에 언급한 토픽 모델링에 대한 공부를 하면서 이 문제도 해결할 수 있을 것이라 생각합니다. 

[Topic Granularity & Hallucination LLM Topic Modelling](https://arxiv-org.access.yonsei.ac.kr/abs/2405.00611), 
[multi-granularity learning towards open topic classification](https://www-sciencedirect-com-ssl.access.yonsei.ac.kr/science/article/pii/S0020025521011555), [Granularity of algorithmically constructed publication-level classifications of research publications: Identification of topics](https://arxiv-org.access.yonsei.ac.kr/abs/1801.02466)

## Step 2 - Analysis on the Diffusion of each Article and Sentiment

### 2.1 - Select some news over different topics.

In Naver, we can see the number of on the news articles. ([example](https://m.entertain.naver.com/series/article/001/0015192965?type=series&cid=1200015)) We can combine them per each news, and then select the top 10 most influential 10 news per topic type.

### 2.2 - Analysis

Analyze the user reactions on various websites / SNS platforms. (number of likes, comments, shares)

As most articles regarding K-pop have clear keywords (usually the person / group / company name), we can analyze the articles with these keywords included in the title or text.

$\to$ [Azua](https://github.com/microsoft/project-azua/), [MatchDG](https://www.microsoft.com/en-us/research/publication/domain-generalization-using-causal-matching/)

#### 2.2.1 - Time period Analysis

Analyze the number of the keywords appearing before / after the news article being posted. Check how long it takes for the news to be at its highest attention. On top of that, we can also check the number of changes in the positive / negative word usage around the keywords. (Useful for platforms like DCinside)

$\to$ We can also do this by counting the number of related tags on a SNS platform before / after the news article posted (Useful for platforms like Instagram)

From this, we can draw insights on the distinct agenda topics and their differences when it comes to information diffusion and reactions. We can also **compare the different information diffusion and reactions across different platforms**.

#### 2.2.3 - Example

For example, after the news of 카리나 and 이재욱 dating was first told to the public by 디스패치, we can analyze the number of articles with '카리나' or '재욱' included in the article, and analyze how the numbers of these articles change over time. We can also check the number of changes in the positive / negative word usage in the articles containing '카리나' or '재욱'. This data can be part of the "romance" category.

## Step 3 - Comparison Between the Different Diffusion and Sentiment Across Different Topics and Platforms

Comparison based on the results. TBD after checking the amount of data.

Visualization: Charts and graphs to show results, may use Python or R instead as Step 1&2 is likely to be in Python, and R provides great visualization packages. [Plots.jl](https://docs.juliaplots.org/stable/), [Plotly for Julia](https://plotly.com/julia/), [wordcloud for Julia](https://github.com/guo-yong-zhi/WordCloud.jl), [TimeSeries Plotting for Julia](https://juliastats.org/TimeSeries.jl/latest/plotting/)
