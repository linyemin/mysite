********************
本地搭建ChatGLM
********************

ChatGLM 是一个面向中文的开源对话模型。以下是详细的步骤来搭建你自己的本地 ChatGLM 环境。如果你遇到任何问题，可以参考官方文档或社区支持。

准备工作
============
在开始之前，你需要确保你的计算机满足以下要求：

- 64位操作系统（如 Windows、Linux 或 macOS）
- 至少 8GB 的内存
- NVIDIA GPU（推荐，但不是必须）以及对应的 CUDA 驱动支持

步骤摘要
============
1. 安装 Python
2. 创建虚拟环境
3. 安装依赖项
4. 下载 ChatGLM 模型
5. 运行模型并进行测试

详细步骤
============

安装 Python
---------------
1. 首先，需要安装 Python（推荐使用 Python 3.8 及以上版本）。你可以从 Python 官网 (https://www.python.org/downloads/) 下载并安装相应的版本。

2. 安装完成后，确保 Python 和 pip 已正确安装，使用以下命令进行检查:


   `python --version`
   `pip --version`

创建虚拟环境
-----------------
1. 使用 `venv` 创建虚拟环境，这样可以更好地管理依赖项:

   `python -m venv chatglm_env`

2. 激活虚拟环境:
在 Windows 上使用:


   `.\chatglm_env\Scripts\activate`

在 macOS/Linux 上使用:

   `source chatglm_env/bin/activate`

安装依赖项
---------------
1. 安装 ChatGLM 所需的依赖项:

   `pip install torch torchvision transformers`

如果你有 NVIDIA GPU 并且想要使用 GPU 加速，可以参考 PyTorch 官网 (https://pytorch.org/get-started/locally/) 的安装指南安装带有 CUDA 支持的 PyTorch 版本。

下载 ChatGLM 模型
--------------------------
1. 从官方仓库下载 ChatGLM 模型和代码，可以使用 `git` 克隆官方仓库:


   `git clone https://github.com/THUDM/ChatGLM.git`

2. 进入模型目录:

   `cd ChatGLM`

运行模型并进行测试
-------------------------
1. 加载 ChatGLM 模型并进行测试。以下是一个简单的测试脚本（保存为 `test_chatglm.py`）:

.. code-block:: python

  from transformers import AutoModelForCausalLM, AutoTokenizer

  model_name = "THUDM/chatglm-6b"
  tokenizer = AutoTokenizer.from_pretrained(model_name)
  model = AutoModelForCausalLM.from_pretrained(model_name)

  # 测试输入
  input_text = "你好，世界！"
  inputs = tokenizer(input_text, return_tensors="pt")

  # 生成回复
  outputs = model.generate(
      inputs["input_ids"], max_length=50, do_sample=True, top_p=0.95, top_k=60
  )

  # 输出结果
  result = tokenizer.decode(outputs[0], skip_special_tokens=True)
  print(result)

2. 运行测试脚本:

   `python test_chatglm.py`


如果一切设置正确，你应该能看到 ChatGLM 模型的回复结果。

最终，你应该有一个完全运行的本地 ChatGLM 环境。祝你使用愉快！