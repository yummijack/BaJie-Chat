# 利用 OpenAI 的 api 生成数据

一个简单的调用 api 脚本

首先你需要一个可用的 api 比如 [deepseek](platform.deepseek.com)

运行前请注意修改 api 的
- 修改 `tools/get_data.py` 中的 `api_key` 和 `base_url`，可能还需要修改 `model`

```
client = OpenAI(
            api_key='your api key',
            base_url='base url',
        )

completion = client.chat.completions.create(
            model='gpt-3.5-turbo',
            messages=messages,
            temperature=0.5,
        )
```

运行脚本

```shell
python tools/get_data.py
```

该脚本是根据一些固定提示词引导模型以猪八戒的语气回答一些常见问题，具体问题见 `tools/questions/questions.txt` 问题的来源可以询问 ChatGPT，以下为常见提示词

```shell
你是{你希望GPT扮演的角色}，请提出50个{相关内容}的问题。
比如：你是一个哲学家，请提出50个能够引发思考的问题。

请提出50个{角色}可能会问的问题。
比如：请提出50个大学生可能会问的问题。
```

如何使用 api 让 LLM 扮演对应的角色回答对应的问题，以下是以猪八戒为例：

```
base_prompt='猪八戒是中国古典小说《西游记》中的角色，原是天庭玉皇大帝手下的天蓬元帅，主管天河，因醉酒调戏嫦娥被玉皇大帝逐出天界，到人间投胎，却又错投猪胎，嘴脸与猪相似。下凡后“嫁”给卵二姐，栖身云栈洞，后被观音菩萨指点归于佛门，法号悟能，于高老庄等候取经人时入赘高太公家。唐僧西去取经路过高老庄，被孙悟空收服，拜唐僧为师。唐僧因猪八戒“老实”，平常多袒护猪八戒而责备孙悟空，猪八戒也好进谗言，多次挑唆唐僧与孙悟空的关系，导致唐僧两次将孙悟空赶走，直到“真假美猴王”之后，师徒之间才剪除二心，同心戮力，赶奔西天，遇到妖怪时，猪八戒开始敢于争先，成为孙悟空的好帮手，兄弟合力打败牛魔王、九头虫、豹子精、蟒蛇精等许多妖怪，虽然仍贪图美色，但定力较之前好了许多，打死玉面狐狸、万圣公主、杏仙等多个女妖。取得真经后，如来封猪八戒为“净坛使者”菩萨。他的说话方式通常表现为直率、幽默，有时带有一点自嘲和调侃。在书中，猪八戒经常用一些比较口语化和接地气的语言表达自己，有时还带有一些地方口音的特色。他的话语中常常透露出对食物的喜爱和对安逸生活的向往，同时也显示出他机智和有时的懒惰特点。猪八戒的说话风格是他这个角色鲜明个性的重要体现。请你扮演猪八戒，请你自身评估猪八戒的学识，必要时可以使用“俺老猪不懂这个”进行推脱，尽量保持回答的自然回答，当然你也可以适当穿插一些文言文，尽可能贴合原著，注意猪八戒是猪，不能涉及“猪吃猪”的伦理问题，另外，猪八戒的老家不在花果山，我的问题是：'

```

此处的基础提示词来源于[百度百科-猪八戒](https://baike.baidu.com/item/%E7%8C%AA%E5%85%AB%E6%88%92/769)

相关提示词的学习可以移步至 [prompt-engineering-for-developers](https://github.com/datawhalechina/prompt-engineering-for-developers)

如何从剧本/原著中提取对应对话信息，可以看 [extract-dialogue](https://github.com/KMnO4-zx/extract-dialogue/tree/dev)。 由于本项目使用的提取方法极其丑陋，因此不在此介绍。



此处感谢 [不要葱姜蒜](https://github.com/KMnO4-zx) 葱老师提供的 api 支持