餐饮数据分析项目

项目概述

本项目通过对餐饮订单数据的分析，从多个维度探索顾客消费行为模式，包括热门菜品、消费时段、日期分布等，为餐厅经营提供数据支持。

环境配置

必备工具
• Git Bash (推荐): 提供接近Linux的命令行体验 [下载地址](https://git-scm.com/downloads)

• Jupyter Lab: Jupyter Notebook的升级版，提供更强大的交互式数据分析环境

  ```bash
  pip install jupyterlab
  ```

Python库依赖
```bash
pip install pandas numpy matplotlib seaborn
```

数据维度分析

订单维度分析
• 最受欢迎菜品: 统计菜品出现频率Top10

• 点菜种类分析: 顾客平均点菜种类数

• 点菜数量分布: 单次订单菜品数量统计

• 消费金额分析:

   • 最高消费订单

   • 平均消费水平

   • 消费金额分布


时间维度分析
• 时段分析:

   • 点菜量集中的时间段

   • 高峰时段识别

• 日期分析:

   • 月度订餐量最大日期

   • 周内就餐人数分布(星期几最忙)


核心技术实现

1. 数据预处理
```python
# 多文件数据拼接
all_data = pd.concat([df1, df2, df3], axis=0)

# 时间字段解析
data['order_time'] = pd.to_datetime(data['timestamp'])
data['hour'] = data['order_time'].dt.hour
data['day'] = data['order_time'].dt.day
data['weekday'] = data['order_time'].dt.weekday
```

2. 分组统计与聚合
```python
# 按菜品分组统计
dish_popularity = data.groupby('dish_name')['order_id'].count().sort_values(ascending=False)

# 按小时统计订单量
hourly_orders = data.groupby('hour')['order_id'].count()
```

3. 数据可视化
```python
# 最受欢迎菜品Top10
top_dishes = dish_popularity.head(10)
plt.figure(figsize=(12,6))
top_dishes.plot(kind='bar')
plt.title('Top 10 最受欢迎菜品')
plt.ylabel('点单量')
plt.xticks(rotation=45)
plt.show()

# 周内订单分布
weekday_order = data.groupby('weekday')['order_id'].count()
weekday_order.plot(kind='bar', figsize=(10,5))
plt.title('一周各天订单量分布')
plt.xlabel('星期(0=周一)')
plt.ylabel('订单量')
plt.show()
```

项目结构
```
restaurant-analysis/
├── data/                    # 原始数据
│   ├── meal_order_detail.xlsx
│   └── ...
├── notebooks/               # Jupyter分析笔记
│   ├── 01_data_cleaning.ipynb
│   ├── 02_dish_analysis.ipynb
│   └── 03_time_analysis.ipynb
├── outputs/                 # 分析结果图表
├── README.md                # 项目说明
└── requirements.txt         # 依赖库列表
```

运行项目
1. 克隆仓库
```bash
git clone https://github.com/yourname/restaurant-analysis.git
cd restaurant-analysis
```

2. 安装依赖
```bash
pip install -r requirements.txt
```

3. 启动Jupyter Lab
```bash
jupyter lab
```

分析示例输出
![菜品Top10示例](outputs/top_dishes.png)
![时段分布示例](outputs/hourly_dist.png)

贡献指南
欢迎提交Issue或Pull Request改进分析维度或可视化效果

许可证
MIT License
