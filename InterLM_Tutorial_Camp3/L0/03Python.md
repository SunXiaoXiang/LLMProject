
### python任务1（编写wordcount）

![示例图片](https://github.com/SunXiaoXiang/LLMProject/blob/main/InterLM_Tutorial_Camp3/L0/imgs/python/01.png)

备注：勘误 教程中的示例output：
{'hello': 1,'world!': 1,'this': 1,'is': 3,'an': 1,'example': 1,'word': 1, 
'count': 2,'fun': 1,'Is': 1,'it': 2,'to': 1,'words': 1,'Yes': 1,'fun': 1  }
并不正确
标准答案应该为
{'hello': 1, 'world': 1, 'this': 1, 'is': 4, 'an': 1, 'example': 1, 'word': 1, 
'count': 2, 'fun': 3, 'it': 2, 'to': 1, 'words': 1, 'yes': 1}
错误点，部分单词未转小写，is 出现2次，总次数对；fun 出现2次，总次数应为3（教案为2）；yes应为小写。

### python任务2（在本地vscode中远程debug代码）

![示例图片](https://github.com/SunXiaoXiang/LLMProject/blob/main/InterLM_Tutorial_Camp3/L0/imgs/python/01.png)

进阶：使用pytest 完成单元测试用例编写。

![示例图片](https://github.com/SunXiaoXiang/LLMProject/blob/main/InterLM_Tutorial_Camp3/L0/imgs/python/02.png)

![示例图片](https://github.com/SunXiaoXiang/LLMProject/blob/main/InterLM_Tutorial_Camp3/L0/imgs/python/03.png)




