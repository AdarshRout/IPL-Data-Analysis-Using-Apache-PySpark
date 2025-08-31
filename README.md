# IPL Data Analysis Using Apache PySpark 🏏

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue)](https://www.python.org/)
[![PySpark](https://img.shields.io/badge/PySpark-3.0%2B-orange)](https://spark.apache.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-yellow)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A comprehensive data analysis project that explores Indian Premier League (IPL) cricket data using Apache PySpark for distributed data processing and advanced analytics.

## 📊 Project Overview

This project performs in-depth analysis of IPL cricket data spanning multiple seasons, utilizing the power of Apache PySpark for big data processing. The analysis covers various aspects of cricket performance including player statistics, team dynamics, match outcomes, and strategic insights.

### Key Features
- **Big Data Processing**: Handles large-scale cricket datasets with 150,000+ ball-by-ball records
- **Advanced Analytics**: Complex aggregations, window functions, and SQL queries
- **Data Visualization**: Interactive charts and graphs using Matplotlib and Seaborn
- **Performance Insights**: Player rankings, team analysis, and strategic recommendations
- **Scalable Architecture**: Built for handling growing datasets with Spark's distributed computing

## 📈 Dataset Description

The project uses five interconnected datasets containing comprehensive IPL data:

| Dataset | Records | Size | Description |
|---------|---------|------|-------------|
| `Ball_By_Ball.csv` | 150,452 | 24MB | Detailed ball-by-ball match data including runs, wickets, extras |
| `Player_match.csv` | 13,994 | 2.6MB | Player performance data for each match |
| `Match.csv` | 638 | 112KB | Match-level information including teams, venues, results |
| `Player.csv` | 498 | 36KB | Player profiles with batting/bowling styles and country |
| `Team.csv` | 14 | 4KB | Team information and identifiers |

### Data Schema Highlights
- **Ball-by-Ball Data**: Match ID, over/ball details, batting/bowling teams, runs scored, wickets, extras
- **Match Data**: Teams, venues, toss details, match winners, margins of victory
- **Player Data**: Personal information, playing style, country representation
- **Performance Metrics**: Batting averages, bowling figures, match contributions

## 🚀 Getting Started

### Prerequisites
- Python 3.7 or higher
- Java 8 or 11 (required for PySpark)
- Jupyter Notebook
- Minimum 4GB RAM (8GB recommended for optimal performance)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AdarshRout/IPL-Data-Analysis-Using-Apache-PySpark.git
   cd IPL-Data-Analysis-Using-Apache-PySpark
   ```

2. **Install required packages**
   ```bash
   pip install pyspark
   pip install jupyter
   pip install matplotlib seaborn pandas
   ```

3. **Start Jupyter Notebook**
   ```bash
   jupyter notebook
   ```

4. **Open and run the analysis**
   - Open `IPL-data-analysis.ipynb`
   - Execute cells sequentially to perform the analysis

### Quick Start
```python
from pyspark.sql import SparkSession

# Initialize Spark Session
spark = SparkSession.builder.appName('IPL-Analysis').getOrCreate()

# Load data
ball_by_ball_df = spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("Ball_By_Ball.csv")
match_df = spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("Match.csv")
```

## 🔍 Analysis Highlights

The project includes comprehensive analysis across multiple dimensions:

### 1. **Player Performance Analysis**
- Top scoring batsmen per season
- Most economical bowlers in powerplay overs
- Player performance in winning vs losing matches
- Batting averages and strike rates analysis

### 2. **Team Performance Metrics**
- Team win/loss ratios by season
- Home vs away performance analysis
- Toss impact on match outcomes
- Team performance after winning toss

### 3. **Match Dynamics**
- Run scoring patterns across different overs
- Powerplay vs death over analysis
- Venue-specific performance trends
- Seasonal performance variations

### 4. **Advanced Analytics**
- **Window Functions**: Running totals and moving averages
- **Aggregations**: Complex grouping and statistical measures
- **SQL Queries**: Advanced joins and subqueries for insights
- **Time Series Analysis**: Performance trends over multiple seasons

## 📊 Key Insights & Findings

Based on the comprehensive analysis, several key insights emerge:

- **Toss Impact**: Teams winning the toss show varying success rates depending on venue conditions
- **Player Consistency**: Top performers maintain consistent averages across different match situations
- **Powerplay Economics**: Certain bowlers demonstrate exceptional economy rates during powerplay overs
- **Seasonal Trends**: Performance patterns vary significantly across different IPL seasons

## 🛠️ Technology Stack

- **Apache PySpark**: Distributed data processing and analytics
- **Python**: Core programming language
- **Jupyter Notebook**: Interactive development environment
- **Matplotlib & Seaborn**: Data visualization libraries
- **Pandas**: Data manipulation and analysis
- **SQL**: Advanced querying capabilities

## 📁 Project Structure

```
IPL-Data-Analysis-Using-Apache-PySpark/
│
├── IPL-data-analysis.ipynb    # Main analysis notebook (44 cells)
├── Ball_By_Ball.csv          # Detailed ball-by-ball data
├── Match.csv                 # Match information
├── Player.csv                # Player profiles
├── Player_match.csv          # Player match statistics
├── Team.csv                  # Team information
├── .gitignore               # Git ignore file
└── README.md                # Project documentation
```

## 🔧 Configuration Notes

- **Memory Settings**: For large datasets, configure Spark with adequate memory:
  ```python
  spark = SparkSession.builder \
      .appName('IPL-Analysis') \
      .config('spark.executor.memory', '4g') \
      .config('spark.driver.memory', '2g') \
      .getOrCreate()
  ```

- **File Paths**: Update CSV file paths in the notebook based on your local setup
- **Performance Tuning**: Adjust partition size based on your system's capabilities

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Setup
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🏆 Acknowledgments

- Indian Premier League for providing comprehensive cricket data
- Apache Spark community for the powerful distributed computing framework
- Cricket analytics community for insights and methodologies

## 📞 Contact

**Adarsh Rout** - [GitHub Profile](https://github.com/AdarshRout)

Project Link: [https://github.com/AdarshRout/IPL-Data-Analysis-Using-Apache-PySpark](https://github.com/AdarshRout/IPL-Data-Analysis-Using-Apache-PySpark)

---

⭐ **Star this repo if you found it helpful!** ⭐