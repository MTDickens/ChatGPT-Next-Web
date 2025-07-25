<div align="center">

<img src="./docs/images/head-cover.png" alt="icon"/>

<h1 align="center">ChatGPT Next Web LangChain</h1>

一键免费部署你的跨平台私人 ChatGPT 应用, 支持 GPT3, GPT4 & Gemini Pro 模型。（基于 LangChain 实现插件功能）

[![Web][Web-image]][web-url]

[网页版](https://n3xt.chat) / [反馈](https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues) / [Discord](https://discord.gg/QPrKZFwWn8) / QQ群: `763467624`

[web-url]: https://n3xt.chat/
[download-url]: https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/releases
[Web-image]: https://img.shields.io/badge/Web-PWA-orange?logo=microsoftedge
[Windows-image]: https://img.shields.io/badge/-Windows-blue?logo=windows
[MacOS-image]: https://img.shields.io/badge/-MacOS-black?logo=apple
[Linux-image]: https://img.shields.io/badge/-Linux-333?logo=ubuntu

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FHk-Gosuto%2FChatGPT-Next-Web-LangChain&env=OPENAI_API_KEY,CODE&project-name=chatgpt-next-web-langchain&repository-name=ChatGPT-Next-Web-LangChain)

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain)

</div>

> [!WARNING]
> 本项目插件功能基于 [OpenAI API 函数调用](https://platform.openai.com/docs/guides/function-calling) 功能实现，转发 GitHub Copilot 接口或类似实现的模拟接口并不能正常调用插件功能！
>
> [实验性] 新增 claude 模型函数调用支持。
>
> 由于 Anthropic 不提供嵌入模型，请添加 RAG 功能的 ollama 嵌入模型配置，如不配置，**WebBrowser** 和 **PDFBrowser** 插件将无法使用。

![cover](./docs/images/gemini-image-generation.png)

![cover](./docs/images/thinking-example.png)

![cover](./docs/images/rag-example-2.jpg)

![plugin-example](./docs/images/plugin-example.png)

![wiki-plugin](./docs/images/wiki-plugin-example.png)

![dall-e-plugin](./docs/images/dalle-plugin-example.png)

## 主要功能

- 支持**gpt-image-1** 图像生成模型

- 支持**gemini** (gemini-2.0-flash-exp) 文生图多模态模型

- 支持**深度思考**
  
- 支持**通用搜索**（非插件模型支持联网搜索）
  
  - 环境变量：
    - `TAVILY_API_KEY`
  
  - 申请地址：https://tavily.com
  
- RAG 功能

  - 配置请参考文档 [RAG 功能配置说明](./docs/rag-cn.md)

- 除插件工具外，与原项目保持一致 [ChatGPT-Next-Web 主要功能](https://github.com/Yidadaa/ChatGPT-Next-Web#主要功能)

- 支持 TTS （文本转语音）
  - （免费） Edge TTS https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/266
    - 环境变量（可选）：`EDGE_TTS_VOICE_NAME`
  - （收费） OpenAI TTS https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/208

- 支持语音输入，需要使用 HTTPS 访问 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/208

- 支持 GPT-4V(视觉) 模型
  - ~~需要配置对象存储服务，请参考 [对象存储服务配置指南](./docs/s3-oss.md) 配置~~
  - 已同步上游仓库视觉模型调用方式（压缩图片），这里还是会有撑爆 LocalStorage 的风险 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/77#issuecomment-1846410078 ，后面如果出现类似问题会再适配对象存储来存储图像。

- 基于 [LangChain](https://github.com/hwchase17/langchainjs) 实现的插件功能，目前支持以下插件，未来会添加更多
  - 搜索（优先级：`GoogleCustomSearch > SerpAPI > BingSerpAPI > ChooseSearchEngine > DuckDuckGo`）

    - [GoogleCustomSearch](https://api.js.langchain.com/classes/langchain_tools.GoogleCustomSearch.html)

      - 环境变量：
        - `GOOGLE_PLUGIN_API_PROXY_PREFIX` 与 `DDG_API_PROXY_PREFIX` 变量使用方法一致
        - ~~`GOOGLE_API_KEY`~~ `GOOGLE_SEARCH_API_KEY`
        - `GOOGLE_CSE_ID`
      - 申请参考：[说明](https://stackoverflow.com/questions/37083058/programmatically-searching-google-in-python-using-custom-search)

    - [SerpAPI](https://api.js.langchain.com/classes/langchain_tools.SerpAPI.html)

      - 环境变量：`SERPAPI_API_KEY`
      - 申请地址：[SerpApi: Google Search API](https://serpapi.com/)

    - [BingSerpAPI](https://api.js.langchain.com/classes/langchain_tools.BingSerpAPI.html)

      - 环境变量：`BING_SEARCH_API_KEY`
      - 申请地址：[Web Search API | Microsoft Bing](https://www.microsoft.com/en-us/bing/apis/bing-web-search-api)

    - ChooseSearchEngine（作者：[hang666](https://github.com/hang666)）

      - 环境变量：
        - `CHOOSE_SEARCH_ENGINE`
        - `GOOGLE_PLUGIN_API_PROXY_PREFIX` 与 `DDG_API_PROXY_PREFIX` 变量使用方法一致，只会对 google 进行代理

        可选项如下：

        - google
        - baidu

      - 说明：此项为直连搜索引擎，免去api试用量小的烦恼，但可能因为网络问题导致无法使用

      - ⚠ 注意：已知在 vercel 环境下会出现调用不稳定的情况 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/89#issuecomment-1868887904

    - DuckDuckGo

      - 环境变量：`DDG_API_PROXY_PREFIX`

        配置后将在 DuckDuckGo 插件相关接口前拼接配置内容，如：`DDG_API_PROXY_PREFIX=https://example.com/` 则最终请求为：`https://example.com/https://duckduckgo.com`

        可以结合类似 1234567Yang/cf-proxy-ex 这类代理项目来实现 DuckDuckGo 插件相关接口的代理

  - 计算
    - [Calculator](https://api.js.langchain.com/classes/langchain_tools_calculator.Calculator.html)
    - [WolframAlpha](https://api.js.langchain.com/classes/langchain_tools.WolframAlphaTool.html)
      - 环境变量：`WOLFRAM_ALPHA_APP_ID`
      - 申请地址：[Wolfram LLM API](https://developer.wolframalpha.com/)
    
  - 网络请求
    - [WebBrowser](https://api.js.langchain.com/classes/langchain_tools_webbrowser.WebBrowser.html)
      - 需要使用 `text-embedding-ada-002` 嵌入模型
    - PDFBrowser
      - 需要使用 `text-embedding-ada-002` 嵌入模型
      - ⚠ 仅在非 vercel 环境部署时可用 ⚠

  - 其它
    - [Wiki](https://api.js.langchain.com/classes/langchain_tools.WikipediaQueryRun.html)
    - DALL-E 3
      - DALL-E 3 插件需要配置对象存储服务，请参考 [对象存储服务配置指南](./docs/s3-oss.md) 配置
      - 如无需图像转存则可以配置  `DALLE_NO_IMAGE_STORAGE=1` ，此时将直接将 DALL-E 服务返回的临时 URL 用于图像显示，注意：该链接具有时效性
      - 默认使用 `dall-e-3` 模型，如果想使用 `dall-e-2` ，可以配置环境变量 `DALLE_MODEL=dall-e-2`
    - StableDiffusion
      - 本插件目前为测试版本，后续可能会有较大的变更，请谨慎使用
      - 使用本插件需要一定的专业知识，Stable Diffusion 本身的相关问题不在本项目的解答范围内，如果您确定要使用本插件请参考 [Stable Diffusion 插件配置指南](./docs/stable-diffusion-plugin-cn.md) 文档进行配置
      - StableDiffusion 插件需要配置对象存储服务，请参考 [对象存储服务配置指南](./docs/s3-oss.md) 配置
    - Arxiv
    - B站相关插件（作者：[fred913](https://github.com/fred913)）
      - bilibili 视频信息获取（建议使用以下插件时同时启用本插件）
      - bilibili 视频搜索
        - 需配置环境变量 `BILIBILI_COOKIES`
      - bilibili 听歌识曲
        - 需提前部署 [bilivid-metaprocess-server](https://github.com/fred913/bilivid-metaprocess-server) 并配置环境变量 `BILIVID_METAPROCESS_SERVER_ADDRESS`
      - bilibili视频总结
        - 需配置环境变量 `BILIBILI_COOKIES`

- 支持 gemini-pro, gemini-pro-vision 模型
  - 以下功能目前还不支持
    - **插件功能**
  - 如何启用
    - 配置密钥 `GOOGLE_API_KEY` ，key 可以在这里获取：https://ai.google.dev/tutorials/setup
    - 配置自定义接口地址（可选） `GEMINI_BASE_URL`，可以使用我的这个项目搭建一个基于 vercel 的代理服务：[vercel-ai-proxy](https://github.com/Hk-Gosuto/vercel-ai-proxy)
  - 常见问题参考：[Gemini Prompting FAQs](https://js.langchain.com/docs/integrations/chat/google_generativeai#gemini-prompting-faqs)
  - ~~gemini-pro-vision 模型需要配置对象存储服务，请参考 [对象存储服务配置指南](./docs/s3-oss.md) 配置~~
  - ⚠ gemini-pro-vision 注意事项 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/203 ：
    - 每次对话必须包含图像数据，不然会出现 `Add an image to use models/gemini-pro-vision, or switch your model to a text model.` 错误。
    - 只支持单轮对话，多轮对话会出现 `Multiturn chat is not enabled for models/gemini-pro-vision` 错误。

- 非 Vercel 运行环境下支持本地存储

  - 如果你的程序运行在非 Vercel 环境，不配置 `S3_ENDPOINT` 和 `R2_ACCOUNT_ID` 参数，默认上传的文件将存储在 `/app/uploads` 文件夹中


## 开发计划

- [x] 支持使用 DuckDuckGo 作为默认搜索引擎

  不配置时默认使用 `DuckDuckGo` 作为搜索插件。

- [x] 插件列表页面开发

- [x] 支持开关指定插件

- [x] 支持 Agent 参数配置（ ~~agentType~~, maxIterations, returnIntermediateSteps 等）

- [x] 支持 ChatSession 级别插件功能开关

  仅在使用非 `0301` 和 `0314` 版本模型时会出现插件开关，其它模型默认为关闭状态，开关也不会显示。

  最新版本中已经移除上面两个模型。

- [x] 支持语音输入 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/208

- [x] 支持其他类型文件上传 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/77

- [ ] 支持 Azure Storage https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/217

- [ ] 支持 Fooocus-API 插件 https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/58

- [ ] 支持在 UI 配置插件需要的 Key https://github.com/Hk-Gosuto/ChatGPT-Next-Web-LangChain/issues/70

## 开始使用

1. 准备好你的 [OpenAI API Key](https://platform.openai.com/account/api-keys);
2. 点击右侧按钮开始部署：
   [![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FHk-Gosuto%2FChatGPT-Next-Web-LangChain&env=OPENAI_API_KEY,CODE&project-name=chatgpt-next-web-langchain&repository-name=ChatGPT-Next-Web-LangChain)，直接使用 Github 账号登录即可，记得在环境变量页填入 API Key 和[页面访问密码](#配置页面访问密码) CODE；
3. 部署完毕后，即可开始使用；
4. （可选）[绑定自定义域名](https://vercel.com/docs/concepts/projects/domains/add-a-domain)：Vercel 分配的域名 DNS 在某些区域被污染了，绑定自定义域名即可直连。

## FAQ

[简体中文 > 常见问题](./docs/faq-cn.md)

[English > FAQ](./docs/faq-en.md)

[Azure OpenAI](./docs/azure-openai-cn.md)

## 配置页面访问密码

> 配置密码后，用户需要在设置页手动填写访问码才可以正常聊天，否则会通过消息提示未授权状态。

> **警告**：请务必将密码的位数设置得足够长，最好 7 位以上，否则[会被爆破](https://github.com/Yidadaa/ChatGPT-Next-Web/issues/518)。

本项目提供有限的权限控制功能，请在 Vercel 项目控制面板的环境变量页增加名为 `CODE` 的环境变量，值为用英文逗号分隔的自定义密码：

```
code1,code2,code3
```

增加或修改该环境变量后，请**重新部署**项目使改动生效。

## 环境变量

> 本项目大多数配置项都通过环境变量来设置，教程：[如何修改 Vercel 环境变量](./docs/vercel-cn.md)。

### `OPENAI_API_KEY` （必填项）

OpanAI 密钥，你在 openai 账户页面申请的 api key。

### `CODE` （可选）

访问密码，可选，可以使用逗号隔开多个密码。

**警告**：如果不填写此项，则任何人都可以直接使用你部署后的网站，可能会导致你的 token 被急速消耗完毕，建议填写此选项。

### `BASE_URL` （可选）

> Default: `https://api.openai.com`

> Examples: `http://your-openai-proxy.com`

OpenAI 接口代理 URL，如果你手动配置了 openai 接口代理，请填写此选项。

> 如果遇到 ssl 证书问题，请将 `BASE_URL` 的协议设置为 http。

### `OPENAI_ORG_ID` （可选）

指定 OpenAI 中的组织 ID。

### `HIDE_USER_API_KEY` （可选）

如果你不想让用户自行填入 API Key，将此环境变量设置为 1 即可。

### `DISABLE_GPT4` （可选）

如果你不想让用户使用 GPT-4，将此环境变量设置为 1 即可。

### `ENABLE_BALANCE_QUERY` （可选）

如果你想启用余额查询功能，将此环境变量设置为 1 即可。

### `GOOGLE_API_KEY` （可选）

Google Gemini Pro Api Key.

### `GEMINI_BASE_URL` （可选）

Google Gemini Pro Api Url.

### `AZURE_URL` （可选）

> 形如：https://{azure-resource-url}/openai/deployments
>
> ⚠️ 注意：这里与原项目配置不同，不需要指定 {deploy-name}，将模型名修改为 {deploy-name} 即可切换不同的模型
>
> ⚠️ DALL-E 等需要 openai 密钥的插件暂不支持 Azure

Azure 部署地址。

### `AZURE_API_KEY` （可选）

Azure 密钥。

### `AZURE_API_VERSION` （可选）

Azure Api 版本，你可以在这里找到：[Azure 文档](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference#chat-completions)。

### `NEXT_PUBLIC_DISABLE_AUTOGENERATETITLE` （可选）

如果你不想让用户使用自动生成标题功能，将此环境变量设置为 1 即可。

### `NEXT_PUBLIC_DISABLE_SENDMEMORY` （可选）

如果你不想让用户使用历史摘要功能，将此环境变量设置为 1 即可。

### `ANTHROPIC_API_KEY` （可选）

anthropic claude Api Key.

### `ANTHROPIC_API_VERSION` （可选）

anthropic claude Api version.

### `ANTHROPIC_URL` （可选）

anthropic claude Api Url.

### `DISABLE_FAST_LINK` （可选）

如果你想禁用从链接解析预制设置，将此环境变量设置为 1 即可。

For Azure: use `modelName@azure=deploymentName` to customize model name and deployment name.
> Example: `+gpt-3.5-turbo@azure=gpt35` will show option `gpt35(Azure)` in model list.
> If you only can use Azure model, `-all,+gpt-3.5-turbo@azure=gpt35` will `gpt35(Azure)` the only option in model list.

For ByteDance: use `modelName@bytedance=deploymentName` to customize model name and deployment name.
> Example: `+Doubao-lite-4k@bytedance=ep-xxxxx-xxx` will show option `Doubao-lite-4k(ByteDance)` in model list.

### `CUSTOM_MODELS` （可选）

> 示例：`+qwen-7b-chat,+glm-6b,-gpt-3.5-turbo,gpt-4-1106-preview=gpt-4-turbo` 表示增加 `qwen-7b-chat` 和 `glm-6b` 到模型列表，而从列表中删除 `gpt-3.5-turbo`，并将 `gpt-4-1106-preview` 模型名字展示为 `gpt-4-turbo`。
> 如果你想先禁用所有模型，再启用指定模型，可以使用 `-all,+gpt-3.5-turbo`，则表示仅启用 `gpt-3.5-turbo`

用来控制模型列表，使用 `+` 增加一个模型，使用 `-` 来隐藏一个模型，使用 `模型名=展示名` 来自定义模型的展示名，用英文逗号隔开。

在Azure的模式下，支持使用`modelName@azure=deploymentName`的方式配置模型名称和部署名称(deploy-name)
> 示例：`+gpt-3.5-turbo@azure=gpt35`这个配置会在模型列表显示一个`gpt35(Azure)`的选项。
> 如果你只能使用Azure模式，那么设置 `-all,+gpt-3.5-turbo@azure=gpt35` 则可以让对话的默认使用 `gpt35(Azure)`

在ByteDance的模式下，支持使用`modelName@bytedance=deploymentName`的方式配置模型名称和部署名称(deploy-name)
> 示例: `+Doubao-lite-4k@bytedance=ep-xxxxx-xxx`这个配置会在模型列表显示一个`Doubao-lite-4k(ByteDance)`的选项

### `DEFAULT_MODEL` （可选）

更改默认模型

### `USE_REMOTE_MODELS` （可选）

如果你想使用远程模型列表，可以设置为 1 即可

可以与 `CUSTOM_MODELS` 参数一起使用

建议配合 `one-api` 类似的中转项目使用

### `WHITE_WEBDAV_ENDPOINTS` （可选）

如果你想增加允许访问的webdav服务地址，可以使用该选项，格式要求：
- 每一个地址必须是一个完整的 endpoint
> `https://xxxx/xxx`
- 多个地址以`,`相连

### `DEFAULT_INPUT_TEMPLATE` （可选）

自定义默认的 template，用于初始化『设置』中的『用户输入预处理』配置项

### `EDGE_TTS_VOICE_NAME` （可选）

配置 Edge TTS 使用的语音声音，默认为：zh-CN-YunxiNeural
可访问 https://learn.microsoft.com/zh-cn/azure/ai-services/speech-service/language-support?tabs=tts#supported-languages 查看支持的参数

### `USE_OPENAI_ENDPOINT_FOR_ALL_MODELS` （可选）

配置所有模型都使用 OpenAI 路由，在使用类似 `one-api` 的中转项目时会很有用
将此环境变量设置为 1 即可

### `DEEPSEEK_API_KEY` (可选)

DeepSeek Api Key

### `DEEPSEEK_URL` (可选)

DeepSeek Api Url

### `SILICONFLOW_API_KEY` （可选）

硅基流动 API Key

### `SILICONFLOW_URL` （可选）

硅基流动 API URL

### `TAVILY_API_KEY`

Tavily API Key 用于通用搜索功能
获取地址：https://tavily.com

### `TAVILY_MAX_RETURNS` （可选）

通用搜索功能返回的最大结果数，默认为 10

## 部署

### 容器部署 （推荐）

> Docker 版本需要在 20 及其以上，否则会提示找不到镜像。

> ⚠️ 注意：docker 版本在大多数时间都会落后最新的版本 1 到 2 天，所以部署后会持续出现“存在更新”的提示，属于正常现象。
>
> 也可以使用镜像 `gosuto/chatgpt-next-web-langchain:nightly`，该镜像为每日更新。

```shell
docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY="sk-xxxx" \
   -e CODE="页面访问密码" \
   gosuto/chatgpt-next-web-langchain
```

你也可以指定 proxy：

```shell
docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY="sk-xxxx" \
   -e CODE="页面访问密码" \
   --net=host \
   -e PROXY_URL="http://127.0.0.1:7890" \
   gosuto/chatgpt-next-web-langchain
```

如果你的本地代理需要账号密码，可以使用：

```shell
-e PROXY_URL="http://127.0.0.1:7890 user password"
```

如果你需要指定其他环境变量，请自行在上述命令中增加 `-e 环境变量=环境变量值` 来指定。

## 同步聊天记录（UpStash）

| [简体中文](./docs/synchronise-chat-logs-cn.md) | [English](./docs/synchronise-chat-logs-en.md) | [Italiano](./docs/synchronise-chat-logs-es.md) | [日本語](./docs/synchronise-chat-logs-ja.md) | [한국어](./docs/synchronise-chat-logs-ko.md)


## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Hk-Gosuto/ChatGPT-Next-Web-LangChain&type=Date)](https://star-history.com/#Hk-Gosuto/ChatGPT-Next-Web-LangChain&Date)

## 捐赠

<a href="https://www.buymeacoffee.com/gosuto" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

## 感谢

<img src="https://resources.jetbrains.com/storage/products/company/brand/logos/jb_beam.png" alt="JetBrains Logo (Main) logo." height='120'>

感谢 [jetbrains](https://www.jetbrains.com/) 为本项目提供的 [开源许可证](https://www.jetbrains.com/community/opensource/)

## 开源协议

[MIT](https://opensource.org/license/mit/)


[![Powered by DartNode](https://dartnode.com/branding/DN-Open-Source-sm.png)](https://dartnode.com "Powered by DartNode - Free VPS for Open Source")