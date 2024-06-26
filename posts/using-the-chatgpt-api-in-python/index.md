# Using the ChatGPT API in Python

ChatGPT&#39;s API is officially released and can be used in Python.
&lt;!--more--&gt;

{{&lt; link href=&#34;https://openai.com/blog/introducing-chatgpt-and-whisper-apis&#34; content=&#34;Introducing ChatGPT API&#34; title=&#34;Introducing ChatGPT API&#34; card=true &gt;}}

After registering an OpenAI account, create an API Key in [https://platform.openai.com/account/api-keys](https://platform.openai.com/account/api-keys). You can see in [https://platform.openai.com/account/usage](https://platform.openai.com/account/usage) that there is a free trial usage of $18 in the account, which expires on April 1.

This time the released ChatGPT model gpt-3.5-turbo is the same as the model used in the ChatGPT product. In addition, gpt-3.5-turbo-0301 has also been released, and this model is at least supported until June 1.

The complete API usage guide can be found here:

{{&lt; link href=&#34;https://platform.openai.com/docs/guides/chat&#34; content=&#34;ChatGPT API Usage Guide&#34; title=&#34;ChatGPT API Usage Guide&#34; card=true &gt;}}

In short, to use the ChatGPT API in Python, you need to install the `openai` Python package.

``` shell
# If you haven&#39;t installed openai, you can use the following command to install
pip install openai
# If you have installed openai, use the following command to update
pip install openai --upgrade
```
Then, `import openai`, and then use the `openai.Completion.create` function to call the API.

Here is a simple Python script I wrote that can have a multi-turn conversation with ChatGPT.

``` python
import os
import openai

# here you need to replace the API key with your own
os.environ[&#34;OPENAI_API_KEY&#34;] = &#34;sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx&#34;
openai.api_key = os.getenv(&#34;OPENAI_API_KEY&#34;)

messages = [
    {&#34;role&#34;: &#34;system&#34;, &#34;content&#34;: &#34;You are a helpful assistant.&#34;},
]

# this function is used to call the API
def get_response(messages):
    completion = openai.ChatCompletion.create(
        model=&#34;gpt-3.5-turbo&#34;,
        messages=messages,
    )
    return completion.choices[0].message.content  # type: ignore


while True:
    try:
        print(&#34;type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation&#34;)
        user_content = input(&#34;You: &#34;)
        if user_content == &#34;quit&#34;:
            break
        elif user_content == &#34;new&#34;:
            messages = [
                {&#34;role&#34;: &#34;system&#34;, &#34;content&#34;: &#34;You are a helpful assistant.&#34;},
            ]
            print(&#34;new conversation started\n&#34;)
            continue
        else:
            messages.append({&#34;role&#34;: &#34;user&#34;, &#34;content&#34;: user_content})
            response = get_response(messages)
            print(&#34;Assistant:&#34;, response &#43; &#34;\n&#34;)
            # append the response to the messages list for the next turn
            messages.append({&#34;role&#34;: &#34;assistant&#34;, &#34;content&#34;: response})
    except Exception as e:
        print(e)
```

The output is as follows:

{{&lt; admonition type=example open=true &gt;}}
*type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation*  
**You**: What is the biggest animal in the world?  
**Assistant**: The biggest animal in the world is the blue whale. It can grow up to 100 feet long and weigh as much as 200 tons.  

*type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation*  
**You**: Please write a poem about blue whales.  
**Assistant**: Majestic and mighty,  
The blue whale swims through the sea,  
Largest creature on earth,  
Behold its great beauty.  

A vast and gentle giant,  
Graceful in every move,  
Plunge deep into the ocean,  
Embrace the whale and groove.  

With a heart that&#39;s enormous,  
And lungs as large as a car,  
Sing to the depths of the ocean,  
Your melodic, haunting bar.  

A creature so magnificent,  
Awe inspiring, and grand,  
Nowhere else found on earth,  
A true wonder of the land.  

Let us protect this great whale,  
So that it may flourish and thrive,  
For a world without the blue whale,  
Is a world less truly alive.  

*type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation*  
**You**: new  
*new conversation started*  

*type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation*  
**You**: 世界上最大的动物是什么？  
**Assistant**: 世界上最大的动物是蓝鲸。它们可以长达30米长，重达173吨，是地球上已知最大的动物。  

*type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation*  
**You**: 请写一首关于蓝鲸的诗。  
**Assistant**: 在深深的海洋里  
有一种生物，比海洋还大  
它游荡于大海之中  
它的名字叫做蓝鲸  

蓝鲸身长三十米  
重达一百七十三吨  
它们是地球上最大的动物  
不同寻常的存在  

它们的歌声遥远而美丽  
在海洋里有时听得见  
它们善良而又神秘  
是这片蔚蓝海洋之主  

蓝鲸，你的身影  
在海洋中，如此崇高  
你的力量与恩宠  
在人间，永世留存  

*type &#39;quit&#39; to exit, type &#39;new&#39; to begin a new conversation*  
**You**: quit
{{&lt; /admonition &gt;}}

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/using-the-chatgpt-api-in-python/  

