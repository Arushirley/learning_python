
# [python实现词频统计(wordcount)函数](https://www.cnblogs.com/sigmod/p/wordcount.html)

作为字典(key-value)的经典应用题目，单词统计几乎出现在每一种语言键值对学习后的必练题目，主要需求：

写一个函数wordcount统计一篇文章的每个单词出现的次数(词频统计)。统计完成后，对该统计按单词频次进行

排序。

现python实现代码如下:

#!/usr/bin/env python  
# encoding:utf-8  
# @Time   : 2017/8/4  
# @Author : 茶葫芦  
# @Site   :  
# @File   : WordCount.py  
#随便取得一个BBC英文新闻  
str_context="""The US media reports suggest Robert Mueller's inquiry has taken the first step towards possible criminal charges.  
According to Reuters news agency, the jury has issued subpoenas over a June 2016 meeting between President Donald Trump's son and a Russian lawyer.  
The president has poured scorn on any suggestion his team colluded with the Kremlin to beat Hillary Clinton.  
In the US, grand juries are set up to consider whether evidence in any case is strong enough to issue indictments for a criminal trial. They do not decide the innocence or guilt of a potential defendant.  
The panel of ordinary citizens also allows a prosecutor to issue subpoenas, a legal writ, to obtain documents or compel witness testimony under oath.  
Trump: US-Russia relations are at 'dangerous low'  
The Trump-Russia saga in 200 words  
Russia: The 'cloud' over the White House  
Now it's deadly serious  
Anthony Zurcher, BBC North America reporter  
Robert Mueller's special counsel investigation has always been a concern for the Trump administration. Now it's deadly serious business.  
With the news that a grand jury has been convened in Washington DC, and that it is looking into the June 2016 meeting between Donald Trump Jr and Russian nationals, it's clear the investigation is focusing on the president's inner circle.  
This news shouldn't come as a huge shock, given that Mr Mueller has been staffing up with veteran criminal prosecutors and investigators. It is, however, a necessary step that could eventually lead to criminal indictments. At the very least it's a sign that Mr Mueller could be on the trail of something big - expanding the scope beyond former National Security Adviser Michael Flynn and his questionable lobbying. It also indicates his investigation is not going to go away anytime soon.  
In the past, when big news about the Russia investigation has been revealed, Mr Trump has escalated his rhetoric and taken dead aim at his perceived adversaries. The pressure is being applied to the president. How will he respond?  
At a rally in Huntington, West Virginia, on Thursday evening, Mr Trump said the allegations were a "hoax" that were "demeaning to our country".  
"The Russia story is a total fabrication," he said. "It's just an excuse for the greatest loss in the history of American politics, that's all it is."  
The crowd went wild as he continued: "What the prosecutor should be looking at are Hillary Clinton's 33,000 deleted emails."  
"Most people know there were no Russians in our campaign," he added. "There never were. We didn't win because of Russia, we won because of you, that I can tell you."  
Mr Trump's high-powered legal team fielding questions on the Russia inquiry said there was no reason to believe the president himself is under investigation.  
Ty Cobb, a lawyer appointed last month as White House special counsel, said in a statement: "The White House favours anything that accelerates the conclusion of his work fairly.  
"The White House is committed to fully co-operating with Mr Mueller."  
Earlier on Thursday, the US Senate introduced two separate cross-party bills designed to limit the Trump administration's ability to fire Mr Mueller.  
The measures were submitted amid concern the president might dismiss Mr Mueller, as he fired former FBI director James Comey in May, citing the Russia inquiry in his decision."""  
  
def wordcount(str):  
 # 文章字符串前期处理  
 strl_ist = str.replace('\n', '').lower().split(' ')  
 count_dict = {}  
 # 如果字典里有该单词则加1，否则添加入字典  
 for str in strl_ist:  
 if str in count_dict.keys():  
 count_dict[str] = count_dict[str] + 1  
 else:  
 count_dict[str] = 1  
 #按照词频从高到低排列  
 count_list=sorted(count_dict.iteritems(),key=lambda x:x[1],reverse=True)  
 return count_list  
print wordcount(str_context)  
  
  
由于字典是个无序的结构，所以最终返回的是一个列表，没有排序好的字典这一说法。其中

key=lambda x:x[1] 其中X表示某一迭代出来的元素，其实是个元组，而x[1] 表示元组的第二个元素，即单词的次数(词频)，若要按照单词排序则改成

key=lambda x:x[0]即可。

转载请注明出处，感谢！

---

```
#随便取得一个BBC英文新闻  
str_context="""The US media reports suggest Robert Mueller's inquiry has taken the first step towards possible criminal charges.  
According to Reuters news agency, the jury has issued subpoenas over a June 2016 meeting between President Donald Trump's son and a Russian lawyer.  
The president has poured scorn on any suggestion his team colluded with the Kremlin to beat Hillary Clinton.  
In the US, grand juries are set up to consider whether evidence in any case is strong enough to issue indictments for a criminal trial. They do not decide the innocence or guilt of a potential defendant.  
The panel of ordinary citizens also allows a prosecutor to issue subpoenas, a legal writ, to obtain documents or compel witness testimony under oath.  
Trump: US-Russia relations are at 'dangerous low'  
The Trump-Russia saga in 200 words  
Russia: The 'cloud' over the White House  
Now it's deadly serious  
Anthony Zurcher, BBC North America reporter  
Robert Mueller's special counsel investigation has always been a concern for the Trump administration. Now it's deadly serious business.  
With the news that a grand jury has been convened in Washington DC, and that it is looking into the June 2016 meeting between Donald Trump Jr and Russian nationals, it's clear the investigation is focusing on the president's inner circle.  
This news shouldn't come as a huge shock, given that Mr Mueller has been staffing up with veteran criminal prosecutors and investigators. It is, however, a necessary step that could eventually lead to criminal indictments. At the very least it's a sign that Mr Mueller could be on the trail of something big - expanding the scope beyond former National Security Adviser Michael Flynn and his questionable lobbying. It also indicates his investigation is not going to go away anytime soon.  
In the past, when big news about the Russia investigation has been revealed, Mr Trump has escalated his rhetoric and taken dead aim at his perceived adversaries. The pressure is being applied to the president. How will he respond?  
At a rally in Huntington, West Virginia, on Thursday evening, Mr Trump said the allegations were a "hoax" that were "demeaning to our country".  
"The Russia story is a total fabrication," he said. "It's just an excuse for the greatest loss in the history of American politics, that's all it is."  
The crowd went wild as he continued: "What the prosecutor should be looking at are Hillary Clinton's 33,000 deleted emails."  
"Most people know there were no Russians in our campaign," he added. "There never were. We didn't win because of Russia, we won because of you, that I can tell you."  
Mr Trump's high-powered legal team fielding questions on the Russia inquiry said there was no reason to believe the president himself is under investigation.  
Ty Cobb, a lawyer appointed last month as White House special counsel, said in a statement: "The White House favours anything that accelerates the conclusion of his work fairly.  
"The White House is committed to fully co-operating with Mr Mueller."  
Earlier on Thursday, the US Senate introduced two separate cross-party bills designed to limit the Trump administration's ability to fire Mr Mueller.  
The measures were submitted amid concern the president might dismiss Mr Mueller, as he fired former FBI director James Comey in May, citing the Russia inquiry in his decision."""  
  
def wordcount(str):  
 # 文章字符串前期处理  
 str_ist = str.replace('\n', '').lower().split(' ')
 count_dict = {}  
 # 如果字典里有该单词则加1，否则添加入字典  
 for str in str_ist:
  if str in count_dict.keys():  
   count_dict[str] = count_dict[str] + 1  
  else:  
   count_dict[str] = 1  
 #按照词频从高到低排列  
 count_list=sorted(count_dict.items(),key=lambda x:x[1],reverse=True)
 return count_list  

s=wordcount(str_context)  
print(s)
```
