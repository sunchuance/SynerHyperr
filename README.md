# SynerHyperr
SynerHyper: Predicting Anticancer Drug Synergy for Lung Cancer Using Uni-Mol-Enhanced Hypergraph Neural Networks and Multimodal Fusion

基于超图神经网络的药物协同作用预测系统，使用Uni-Mol提取药物分子特征，结合细胞系基因表达数据进行协同作用预测。

## 环境要求

- **操作系统**: Linux (推荐 Ubuntu 18.04+) / Windows WSL2
- **GPU**: NVIDIA GPU with CUDA 11.0+ (可选，CPU也可运行)
- **内存**: 建议 16GB+
- **硬盘**: 至少 5GB 可用空间

## 快速安装,激活环境,输入输出数据格式

```bash
# 1. 克隆或下载项目
git clone <your-repo-url>
cd drug-synergy-predictor

# 2. 创建conda环境
conda create -n unimol python=3.8 -y
conda activate unimol

# 3. 安装依赖
pip install -r requirements.txt

# 4. 下载预训练模型
目录里面

使用说明
基本用法
bash
## 激活环境
conda activate unimol

## 运行预测
python predict_standalone.py --input 你的数据.xlsx --output 预测结果.csv

# 或直接运行（使用默认文件名）
python predict_standalone.py
## 参数说明
参数	说明	默认值
--input	输入Excel文件路径	input_example_data.xlsx
--output	输出CSV文件路径	prediction_results.csv
--model_dir	模型文件目录	当前目录
--no_cuda	强制使用CPU	False
完整示例
bash
# 使用GPU加速
python predict_standalone.py \
    --input ./data/my_drug_combinations.xlsx \
    --output ./results/my_predictions.csv \
    --model_dir ./models/

# 使用CPU
python predict_standalone.py \
    --input ./data/my_drug_combinations.xlsx \
    --output ./results/my_predictions.csv \
    --no_cuda
## 输入数据格式
Excel文件结构
需要准备一个Excel文件（.xlsx格式），包含以下列：

列名	说明	示例
drug_row	药物1名称	Paclitaxel
drug_col	药物2名称	Cisplatin
drug_row_SMILES	药物1的SMILES字符串	CC(=O)OC1=CC(CC2=C...
drug_col_SMILES	药物2的SMILES字符串	[Cl-].[Cl-].N.N.[Pt+2]
cell_line_name	细胞系名称	NCI-H460
## 示例数据
drug_row	drug_col	drug_row_SMILES	drug_col_SMILES	cell_line_name
Paclitaxel	Cisplatin	CC(=O)OC1=CC...	[Cl-].[Cl-]...	NCI-H460
Docetaxel	Carboplatin	CC(=O)OC1=CC...	C1C2C3C4...	A549
支持的细胞系
系统支持以下细胞系（需在表达数据文件中存在）：

NCI-H460, NCI-H226, NCI-H522, EKVX, HOP-92, HOP-62

A549, MCF7, PC-3, DU145

及其他CCLE数据库中的细胞系

## 输出结果说明
CSV输出文件
列名	说明
Drug_1	药物1名称
Drug_2	药物2名称
Cell_Line	细胞系名称
Synergy_Probability	协同作用概率（0-1），值越高表示协同可能性越大
Predicted_Synergy	二分类预测结果（1=协同，0=不协同）
结果解读
Synergy_Probability > 0.7: 高度可能协同

0.5 < Synergy_Probability ≤ 0.7: 可能协同

Synergy_Probability ≤ 0.5: 不太可能协同

## 项目文件说明
text
drug-synergy-predictor/
├── predict_standalone.py      # 主预测脚本
├── hypergraph_model.pth       # 超图神经网络模型（需下载）
├── autoencoder_model.pth      # 自编码器模型（需下载）
├── expression_filtered_4079.csv # 细胞系表达数据
├── requirements.txt           # Python依赖列表
├── input_example_data.xlsx    # 示例输入文件
└── README.md                  # 使用说明
