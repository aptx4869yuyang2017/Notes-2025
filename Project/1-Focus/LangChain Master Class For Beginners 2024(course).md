---
up: 
related: 
created: 2024-08-15
tags: 
type: "[[Course]]"
finished:
---

![](https://s1.vika.cn/space/2024/08/15/e02bd1842331496080bd9ac12449aab1)

##  1 创建环境


## 2 聊天模型 Chat Models

```python
# Chat Model Documents: https://python.langchain.com/v0.2/docs/integrations/chat/
# OpenAI Chat Model Documents: https://python.langchain.com/v0.2/docs/integrations/chat/openai/


import os
from langchain_openai import ChatOpenAI

api_key = os.environ.get('OPENAI_API_KEY_AIHUBMIX')
api_base = os.environ.get('OPENAI_API_BASE')


# Create a ChatOpenAI model
model = ChatOpenAI(model="gpt-3.5-turbo", openai_api_key=api_key)

# Invoke the model with a message
result = model.invoke("What is 81 divided by 9?")
# print("Full result:")
# print(result)
print("Content only:")
print(result.content)
```




## 3 提示词模板 Prompt Templates

[Site Unreachable](https://youtu.be/yF9kGESAi3M?t=2040)

 


## 4 Chains 链

[LangChain Master Class For Beginners 2024 [+20 Examples, LangChain V0.2] - YouTube](https://youtu.be/yF9kGESAi3M?t=2773)

![](https://s1.vika.cn/space/2024/08/16/a29582d08b6c46529f23aadd98ad9c5c)




## 5 RAG Retrieval-Augmented Generation

[Site Unreachable](https://youtu.be/yF9kGESAi3M?t=4579)


![40b3d9333f6f43ceb771fe83087793b2|414](https://s1.vika.cn/space/2024/08/16/40b3d9333f6f43ceb771fe83087793b2)

![](https://s1.vika.cn/space/2024/08/16/a0d01a9ad9064a7a8499401fe17786c9)

![fbffa669327e404b990d16f746360fad|589](https://s1.vika.cn/space/2024/08/16/fbffa669327e404b990d16f746360fad)
## 6 代理人与工具 Agents & Tools