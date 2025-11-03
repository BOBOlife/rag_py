# RAG Python 项目

这是一个基于 Python 的检索增强生成（RAG）项目，演示了如何使用向量数据库和嵌入模型来构建一个简单的文档检索系统。

## 项目概述

本项目实现了一个完整的 RAG 流程，包括：
- 文档分块处理
- 中文文本嵌入生成
- 向量数据库存储
- 相似度检索
- 结果重排序

## 技术栈

- **Python 3.12+**
- **sentence-transformers**: 用于生成中文文本嵌入
- **chromadb**: 向量数据库，用于存储和检索文档向量
- **google-genai**: Google 生成式 AI 集成
- **python-dotenv**: 环境变量管理

## 项目结构

```
rag_python/
├── README.md              # 项目说明文档
├── doc.md                 # 示例文档（迪迦奥特曼故事）
├── main.ipynb             # 主要实现代码（Jupyter Notebook）
├── pyproject.toml         # 项目配置和依赖管理
├── .env                   # 环境变量配置
├── .gitignore             # Git 忽略文件
└── .python-version        # Python 版本指定
```

## 功能特性

### 1. 文档处理
- 将文档按段落分割成块
- 支持中文文本的分块处理

### 2. 嵌入生成
- 使用 `shibing624/text2vec-base-chinese` 模型生成 768 维中文文本嵌入
- 支持批量嵌入生成

### 3. 向量存储
- 使用 ChromaDB 作为向量数据库
- 支持文档、嵌入和 ID 的关联存储

### 4. 检索功能
- 基于向量相似度的文档检索
- 支持指定返回结果数量（top-k）

### 5. 结果重排序
- 使用 CrossEncoder 对检索结果进行重排序
- 提高检索结果的相关性

## 快速开始

### 1. 环境准备

确保你的系统已安装 Python 3.12 或更高版本。

### 2. 安装依赖

```bash
# 使用 uv 安装依赖（推荐）
uv sync

# 或使用 pip 安装
pip install -r requirements.txt
```

### 3. 运行项目

打开 `main.ipynb` 文件，按顺序运行各个代码单元格：

1. **文档分块**: 将 `doc.md` 文件分割成段落块
2. **嵌入生成**: 为每个文本块生成向量嵌入
3. **向量存储**: 将文档和嵌入存储到 ChromaDB
4. **相似度检索**: 根据查询检索相关文档片段
5. **结果重排序**: 使用 CrossEncoder 优化检索结果

## 使用示例

### 基本检索

```python
# 检索与"怪兽想干什么？"相关的文档片段
query = "怪兽想干什么？"
retrieved_chunks = retrieve(query, 5)
```

### 重排序检索

```python
# 对检索结果进行重排序
reranked_chunks = rerank(query, retrieved_chunks, 3)
```

## 配置说明

### 环境变量

在 `.env` 文件中配置相关 API 密钥和参数：

```env
# Google AI API 配置
GOOGLE_API_KEY=your_google_api_key_here

# 其他配置参数
EMBEDDING_MODEL=shibing624/text2vec-base-chinese
CROSS_ENCODER_MODEL=cross-encoder/mmarco-mMiniLMv2-H384-v1
```

### 模型配置

- **嵌入模型**: `shibing624/text2vec-base-chinese` - 专门针对中文优化的文本嵌入模型
- **重排序模型**: `cross-encoder/mmarco-mMiniLMv2-H384-v1` - 用于结果重排序的交叉编码器

## 示例文档

项目包含一个示例文档 `doc.md`，讲述了一个关于迪迦奥特曼和戴拿奥特曼的搞笑故事。这个故事被用作演示文档检索功能的测试数据。

## 扩展功能

### 添加新的文档

1. 将新文档添加到项目目录
2. 修改 `main.ipynb` 中的文件路径
3. 重新运行分块和嵌入流程

### 更换嵌入模型

1. 在 `pyproject.toml` 中添加新的模型依赖
2. 修改 `main.ipynb` 中的模型名称
3. 重新生成嵌入

### 自定义重排序

1. 选择合适的 CrossEncoder 模型
2. 修改 `rerank` 函数中的模型名称
3. 调整重排序参数

## 注意事项

1. **内存使用**: ChromaDB 默认使用内存模式，重启后数据会丢失
2. **模型大小**: 中文嵌入模型较大，首次下载需要时间
3. **性能考虑**: 批量处理大量文档时注意内存使用
4. **API 限制**: 使用 Google AI 时注意 API 调用限制

## 许可证

本项目采用 MIT 许可证。

## 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目。

## 联系方式

如有问题或建议，请通过 GitHub Issues 联系。