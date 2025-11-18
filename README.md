# Agent
个人笔记-学习AI agent
# Agent 第三章：大语言模型基础习题
# 请使用本章提供的迷你语料库（datawhale agent learns, datawhale agent works），计算句子 agent works 在Bigram模型下的概率。
from collections import defaultdict

# 给定的迷你语料库
corpus = ["datawhale agent learns", "datawhale agent works"]

# 初始化用于存储 bigram 频率的字典
bigram_freq = defaultdict(int)
unigram_freq = defaultdict(int)

# 构建 unigram 和 bigram 频率表
for sentence in corpus:
    words = sentence.split()
    for i, word in enumerate(words):
        # 更新 unigram 频率
        unigram_freq[word] += 1
        if i > 0:
            # 更新 bigram 频率
            bigram = (words[i-1], word)
            bigram_freq[bigram] += 1

# 计算句子 "agent works" 的概率
sentence = "agent works"
words = sentence.split()
probability = 1.0

for i, word in enumerate(words):
    if i > 0:
        bigram = (words[i-1], word)
        bigram_count = bigram_freq.get(bigram, 0)
        unigram_count = unigram_freq[words[i-1]]
        probability *= (bigram_count / unigram_count)

print(f"The probability of the sentence '{sentence}' is: {probability}")
