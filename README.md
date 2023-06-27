# BaoLuo LawAssistant - 宝罗法律助理

欢迎来到 [BaoLuo LawAssistant](https://github.com/xuanxuanzl/BaoLuo-LawAssistant) 项目！这个项目旨在提供专业的中文法律咨询服务，并分享在大模型在范司法行业领域微调的经验，以帮助社区开发更多优质的专用领域的大模型。

## 项目简介

 [BaoLuo LawAssistant](https://github.com/xuanxuanzl/BaoLuo-LawAssistant)  是一个中文法律大模型，使用开源法律领域的约100万条数据进行微调，能够提供法律法规检索、法律咨询、案情分析、罪名预测等服务。
本项目模型版本。
- **[BaoLuo-LawAssistant-sftglm-6b](https://huggingface.co/xuanxuanzl/BaoLuo-LawAssistant-sftglm-6b)** 基于Encoder-Decoder结构基座模型做的P-Tuning微调


该模型旨在为法律从业者、学生和普通用户提供准确、可靠的法律咨询服务。我们将分享在大模型基础上微调的经验和最佳实践，以帮助社区开发更多优秀的中文法律大模型，推动中文法律智能化的发展。

## 功能和特点

- **专业法律知识**：BaoLuo LawAssistant 经过100W法律数据集上的微调，拥有较为丰富的中文法律知识和理解能力，能够回答相关法律问题。

- **法律咨询服务**：通过与 BaoLuo LawAssistant 进行交互，您可以提出具体的法律问题，模型将根据您的输入提供详细和准确的回答，为您提供法律咨询和支持。

- **法律案例及其他**：BaoLuo LawAssistant 适用于部分法律相关领域的应用，包括法律法规检索包括但不限于民法典、合同法、劳动法、知识产权、民事诉讼、刑事法等，包括案情分析、罪名预测等应用。

## 环境搭建

具体使用帮助或者疑问可查看如下两个开源项目：
1. [NCZkevin](https://github.com/NCZkevin/chatglm-web)

2. [Chanzhaoyu](https://github.com/Chanzhaoyu/chatgpt-web)


### Node

`node` 需要 `^16 || ^18` 版本（`node >= 14`
需要安装 [fetch polyfill](https://github.com/developit/unfetch#usage-as-a-polyfill)
），使用 [nvm](https://github.com/nvm-sh/nvm) 可管理本地多个 `node` 版本

```shell
node -v
```

### PNPM

如果你没有安装过 `pnpm`

```shell
npm install pnpm -g
```

### Python

`python` 需要 `3.8` 以上版本，进入文件夹 `/service` 运行以下命令

```shell
pip install --no-cache-dir -r requirements.txt
```

## 开发环境启动项目

### 后端服务

#### 硬件需求

| **量化等级**   | **最低 GPU 显存**（推理） | **最低 GPU 显存**（高效参数微调） |
| -------------- | ------------------------- | --------------------------------- |
| FP16（无量化） | 13 GB                     | 14 GB                             |
| INT8           | 8 GB                     | 9 GB                             |
| INT4           | 6 GB                      | 7 GB                              |

```shell
# 使用知识库功能需要在启动API前运行
python gen_data.py
# 进入文件夹 `/service` 运行以下命令
python main.py
```
还有以下可选参数可用：

- `device` 使用设备,cpu或者gpu
- `quantize` 量化等级。可选值：16，8，4，默认为16
- `host` HOST，默认值为 0.0.0.0
- `port` PORT，默认值为 3002

也就是说可以这样启动（这里修改端口的话前端也需要修改，建议使用默认端口）
```shell
python main.py --device='cuda:0' --quantize=16 --host='0.0.0.0' --port=3002
```

### 前端网页

根目录下运行以下命令

```shell
# 前端网页的默认端口号是3000，对接的后端服务的默认端口号是3002，可以在 .env 和 .vite.config.ts 文件中修改
pnpm bootstrap
pnpm dev
```

## 模型文件下载
1. **P-Tuning基础模型**。首先下载[ChatGLM下载](https://github.com/THUDM/ChatGLM-6B)，如果要使用2必须下载此模型。
2. **P-Tuning微调模型**。[BaoLuo-LawAssistant-sftglm-6b模型及权重](https://huggingface.co/xuanxuanzl/BaoLuo-LawAssistant-sftglm-6b)，此模型需要结合ChatGlm使用。

## 主要配置文件说明
1. **[修改网站基本参数](prompts-zh.json)**
2. **[提示词网络路径配置](src/assets/recommend.json)**
3. **[配置界面参数](src/locales/zh-CN.ts)**
4. **[关于模型代码配置](service/main.py)**

## 模型存在不足

- 基准模型采用的性能不高，导致回复响应时间较长，下一步采用效率更高的基础模型。
- 各服务功能的数据分布不均衡。
- 各服务数据的重要指令设计不足。
- 结合外部知识增强提升模型输出的准确度方面有欠缺。

## 项目贡献
1. 感谢作者 [NCZkevin](https://github.com/NCZkevin/chatglm-web)
2. 感谢作者 [Chanzhaoyu](https://github.com/Chanzhaoyu/chatgpt-web)和所有做过贡献的人
3. 感谢作者 [ChatGLM](https://github.com/THUDM/ChatGLM-6B)

## 赞助
如果你觉得这个项目对你有帮助，请给我点个Star。

## License
本项目中的代码采用MIT协议，涉及模型开源协议详见下载中说明。
MIT © [LeiZi](./license)
