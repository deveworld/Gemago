## Update Logs
- You can all update logs at [Blog(Korean)](https://blog.worldsw.dev/tag/gemago/)

---

# Gemago
A lightweight English-and-Korean bidirectional translation model based on Gemma.

We were inspired by [jwj7140's Gugugo](https://github.com/jwj7140/Gugugo).

## Versions
| Model Name | Version | Parameters | Published | Colab |
| --- | :---: | :---: | :---: | ---: |
| [Gemago-2b](https://huggingface.co/DevWorld/Gemago-2b) | Alpha | 2B | ✅ | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/deveworld/Gemago/blob/main/Gemago_2b_Infer.ipynb) |
| [Gemago-7b](https://huggingface.co/DevWorld/Gemago-7b) | - | 7B | ❌ | TBD |

## Evaluation
We used GPT-4 for auto evaluation.

### Prompt
We leveraged `G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment (Yang Liu. et. al. 2023)` and `USR: An Unsupervised and Reference Free Evaluation Metric for Dialog Generation (Shikib Mehri. et. al. 2020)` to construct evaluation prompts similar to [KULLM Evaluation](https://github.com/nlpai-lab/KULLM)
```
You will be given one translation for a original text.
Your task is to rate the translation on one metric.
Please make sure you read and understand these instructions carefully. Please keep this document open while reviewing, and refer to it as needed.

Evaluation Criteria:
- Understandable: Is the translation understandable given the original text?
- Natural: Does the translation seem to be something that a person would naturally say?
- Maintains Context: Does the translation serve as a valid continuation of the preceding conversation?
- Interesting: Is the translation dull or interesting?
- Coherence: Is the translation understandable consistent in same word?
- Overall Quality: Given your answers above, what is your overall impression of the quality of this translation?

Evaluation Steps:
1. Read the original text carefully and identify the main topic and key points.
2. Read the translation and compare it to the original text. Check if the translation covers the main topic and key points of the original text, and if it presents them in a clear and logical order.
3. Assign a score on a scale of 1 to 100, where 1 is the lowest and 100 is the highest.

Original text:
{original}

Translation:
{translation}


Evaluation Form (scores ONLY):
- Understandable:
- Natural:
- Maintains Context:
- Interesting:
- Coherence:
- Overall Quality:
```

### Demos
Here are the Korean -> English demos.

Evaluation results for the newly released models will be available soon after the evaluation is performed.

From Gugugo demo:
```
"한편 금융위원회와 금융감독원의 '6월 가계대출 동향'에 따르면 은행권과 제2금융권을 포함한 전 금융권 가계대출은 지난달 3조 5천억원 증가해 3개월 연속 증가세를 이어갔다."
```
| Model | Score (average 5 samples) | Output Example |
| --------------- | :---: | ---: | 
| GPT-4           |   -   | According to the "June Household Loan Trends" by the Financial Services Commission and the Financial Supervisory Service, household loans across the entire financial sector, including banks and the secondary financial sector, increased by 3.5 trillion won last month, continuing an upward trend for three consecutive months. |
| Papago          |  . | Meanwhile, according to the "June Household Loan Trends" by the Financial Services Commission and the Financial Supervisory Service, household loans in all financial sectors, including the banking and non-banking sectors, increased by 3.5 trillion won last month, continuing their increase for the third consecutive month. |
| GPT-3.5-turbo   |  . | According to the "June Trends in Household Loans" by the Financial Services Commission and the Financial Supervisory Service, household loans in the entire financial sector, including banks and non-bank financial institutions, increased by 3 trillion 500 billion won last month, continuing to rise for the third consecutive month. |
| DeepL           |  . | Meanwhile, according to the Financial Services Commission and the Financial Supervisory Service, household loans across all financial institutions, including banks and secondary financial institutions, increased by 3.5 trillion won last month, the third consecutive month of growth. |
| **Gemago-2b**   |  . | Meanwhile, according to the "June Household Loan Trend" by the Financial Services Commission and the Financial Supervisory Service, household loans in all financial sectors, including banks and secondary financial institutions, increased by KRW 3.5 trillion last month, continuing the trend of increase for three consecutive months. |
| Gugugo-7b       |  . | Meanwhile, according to the "June Household Lending Trend" by the Financial Services Commission and Bank of Korea, household lending in all financial institutions including banks and non-banking institutions increased by 3.5 trillion won (US$3.1 billion) last month, continuing its growth streak for three months |
| Papago(offline) |  . | Meanwhile, according to the Financial Supervisory Commission and the Financial Supervisory Service's  '.조 trillion won, including banks and the second financial institutions, a  전.조 trillion won last month |
| Gugugo-1.3b     |  . | On the one hand, followed by the Financial Services Commission and the Financial Services Commission's 'Monthly Household Loan Trends' followed by the Financial Services Commission's 'Monthly Household Loan Trends' followed by the Financial Services Commission's 'Monthly Household Loan Trends' followed by the Financial Services Commission's 'Monthly Household Loan Trends' followed by the ...(repeat) |

Other one:
```
"이때 뚜우 하고 정오 사이렌이 울었다. 사람들은 모두 네 활개를 펴고 닭처럼 푸드덕거리는 것 같고 온갖 유리와 강철과 대리석과 지폐와 잉크가 부글부글 끓고 수선을 떨고 하는 것 같은 찰나! 그야말로 현란을 극한 정오다."
```
| Model | Score (average 5 samples) | Output Example |
| --------------- | :---: | ---: | 
| GPT-4           |   -   | At this moment, the noon siren went off with a blare. It seemed like everyone was spreading their wings wide, clucking like chickens, amidst the bubbling chaos of glass, steel, marble, paper money, and ink—all in a buzzing uproar! Truly, it was the ultimate dazzling noon. |
| GPT-3.5-turbo   |  . | At this moment, a loud siren rang between noon and midnight. People were all spreading their wings and making fluttering chicken-like noises, and it felt like all kinds of glass, steel, marble, banknotes, and ink were boiling and trembling for a moment! It was truly a dazzling and extreme noon. |
| DeepL           |  . | Then the noon siren sounded. All the people seemed to be pecking like chickens, all the glass and steel and marble and paper money and ink boiling and shuddering and mending! It was noon at the height of the commotion. |
| Gugugo-7b       |  . | Then there was a thunder, and at noon a clarion was blown. The people all stood on one leg and bobbed like chickens; and everything was boiling and bubbling, like a great cauldron of glass and iron and marble and money and ink. It was a glaring noon. |
| Papago          |  . | At noon, the siren sounded like a rooster. Everyone seemed to be paddling like a chicken with all four legs spread out, and all kinds of glass, steel, marble, bills, and ink bubbling and quaking! It's really a flashy noon. |
| **Gemago-2b**   |  . | At this time, the four o'clock siren went off. It's like everyone is opening their nets and flapping their wings like a chicken, and all kinds of glass, steel, marble, bills, and ink are boiling, and they are making repairs. It's like a flash of brilliance at noon. |
| Gugugo-1.3b     |  . | In this case, the sound of two hours happened. The people were everywhere, they seemed to feel like they were feeding themselves all over the place. It seemed like the people felt like the whole world was bursting with glass and steel and glass and minerals and ink. It was like a terrifying extremely high hour! happening at the same time! 공영주 At this time there was a place that seemed to burst all the way around ... |
| Papago(offline) |  . | At this time, Jungo Saen cried.People all seem to spread four bows and poop like a snake, and the cobble of glass, steel and bills and ink are shaking크가It's just as a big deal. |

## Acknowledgements
Thanks to support the TPU resources, [TPU Research Cloud](https://sites.research.google/trc/) Program.
