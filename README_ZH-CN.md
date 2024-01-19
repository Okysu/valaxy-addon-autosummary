# Valaxy-addon-autosummary

<div class="language-switcher">
  <a href="README.md">English</a>
  <a href="README_ZH-CN.md">简体中文</a>
</div>

<style>
.language-switcher {
  text-align: center;
}
.language-switcher a {
  margin: 0 10px;
}
</style>

## 概要

![WOW](https://source.yby.zone/upload/images/1705667938_o0VGDYLJwTL.png)

手写文章摘要！？太麻烦了！这是一款适用于Valaxy的插件，可以自动生成文章摘要。

## 使用方法

首先需要将需要使用AI摘要的文章修改`frontmatter`中的`excerpt_type`字段，值为`ai`。

```yaml
excerpt_type: ai
```

把本仓库下的`autoSummary.ts`随便放到一个你喜欢的文件夹下。如果你不喜欢这个插件的名称，你可以把文件名改成你喜欢的名字。

然后在Valaxy的配置文件（`valaxy.config.ts`）中添加这个插件
```ts
import { startAISummary } from "./autoSummary";

export default defineValaxyConfig<UserThemeConfig>({
  // ... 其他的一些配置

  hooks: {
    "build:before": async () => {
      console.log("start auto summary");
      await startAISummary();
    },
  },
});
```

如果你使用Vercel等平台部署，你需要在这些平台的设置页面设置好以下两个环境变量：

- `OPENAI_BASE_URL`：OpenAI的API地址，一般是`https://api.openai.com/`，为空时默认使用这个地址。
- `OPENAI_API_KEY`：OpenAI的API Key。

如果你只使用本地部署，你需要在你的环境变量中设置好这两个环境变量。

## 注意事项

本插件使用的依赖，Valaxy已经为你安装好了，你不需要再安装。

所以你只需要把`autoSummary.ts`放到你的项目中，然后在Valaxy的配置文件中添加这个插件就可以了。

当文章有`excerpt`的时候，本插件不会对文章进行摘要。

## 模型参数调整

你可以在`autoSummary.ts`中修改模型参数，以达到你想要的效果。

```ts
const data = {
  model: "gpt-3.5-turbo",
  messages: prompt, // 这个不需要更改
  max_tokens: 300,
  temperature: 0.9,
  top_p: 1,
  frequency_penalty: 0,
  presence_penalty: 0.3,
  stop: ["\n"],
};
```

如果输出效果不佳可能是`prompt`的问题，你可以修改`openaiConfig.prompt`的内容，以达到你想要的效果。


## 我没有Open AI的API Key

可以去小于同学的，也是我的平台，[For fun via AI.](https://ai.coolers.fun/register?aff=Af6f)注册一个账号，新用户送的额度足够你生成好多好多文章摘要了。