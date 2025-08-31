# IPL Data Analysis Using Apache PySpark

A comprehensive data analysis project for Indian Premier League (IPL) cricket data using Apache PySpark. This project demonstrates big data processing techniques, SQL operations, and data visualization for cricket analytics.

## 📊 Project Overview

This project analyzes IPL cricket data from multiple seasons to extract meaningful insights about player performance, team strategies, and match outcomes. Using Apache PySpark's distributed computing capabilities, we process large datasets efficiently and generate actionable insights.

## 🏏 Dataset Description

The project works with five main datasets:

### 1. Ball_By_Ball.csv
Contains detailed ball-by-ball information for every delivery in IPL matches:
- Match and over details
- Batting and bowling team information
- Runs scored, extras, and wicket information
- Player IDs for striker, non-striker, bowler, and fielders

### 2. Match.csv
Match-level information including:
- Team details (Team1, Team2)
- Match metadata (date, season, venue, city)
- Toss and match winners
- Win margins and match outcomes
- Man of the Match awards

### 3. Player.csv
Player master data:
- Player demographics (name, date of birth)
- Playing style (batting hand, bowling skill)
- Country information

### 4. Player_match.csv
Player-specific match information:
- Role descriptions and team assignments
- Age at match time
- Captain and wicket-keeper flags
- Man of the Match indicators

### 5. Team.csv
Team master data with team IDs and names

## 🛠️ Technologies Used

- **Apache PySpark**: For distributed data processing
- **Python**: Core programming language
- **Matplotlib**: For data visualization
- **Seaborn**: For statistical data visualization
- **Jupyter Notebook**: For interactive development

## 🚀 Features

### Data Processing
- **Schema Definition**: Custom schemas for all datasets ensuring data type consistency
- **Data Cleaning**: Handling missing values and data normalization
- **Data Transformation**: Creating derived columns and categorical variables

### Analysis Capabilities
1. **Batting Analysis**
   - Top scoring batsmen per season
   - Average runs in winning matches
   - Running totals and cumulative statistics

2. **Bowling Analysis**
   - Most economical bowlers in powerplay overs
   - Wicket-taking patterns
   - Bowling performance metrics

3. **Match Analysis**
   - Toss impact on match outcomes
   - Venue-wise scoring patterns
   - Win margin categorization

4. **Team Performance**
   - Team performance after winning toss
   - Head-to-head statistics
   - Seasonal performance trends

### Advanced Features
- **Window Functions**: Running totals and ranked statistics
- **Complex Aggregations**: Multi-dimensional grouping and analysis
- **Conditional Logic**: Dynamic column creation based on business rules
- **SQL Integration**: Spark SQL for complex analytical queries

## 📈 Key Insights Generated

1. **Venue Impact**: Analysis of how different venues affect scoring patterns
2. **Toss Advantage**: Quantification of toss winning impact on match outcomes
3. **Player Performance**: Individual player statistics in various match situations
4. **Dismissal Patterns**: Most common ways batsmen get out
5. **Powerplay Economics**: Bowler performance in crucial powerplay overs

## 📁 Project Structure

```
├── Ball_By_Ball.csv           # Ball-by-ball match data
├── Match.csv                  # Match-level information
├── Player.csv                 # Player master data
├── Player_match.csv           # Player-match relationship data
├── Team.csv                   # Team master data
├── IPL-data-analysis.ipynb    # Main analysis notebook (⚠️ Update file paths before running)
├── artifacts/                 # Spark artifacts and logs
├── spark-warehouse/           # Spark warehouse directory
└── README.md                  # Project documentation
```

> **⚠️ Important Note**: The notebook contains placeholder paths like `path_to_Ball_By_Ball.csv`. You must replace these with actual file paths to your dataset files before running the analysis.

## 🔧 Setup and Installation

### Prerequisites
- Python 3.7+
- Java 8+ (required for PySpark)
- Apache Spark

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/AdarshRout/IPL-Data-Analysis-Using-Apache-PySpark.git
   cd IPL-Data-Analysis-Using-Apache-PySpark
   ```

2. **Install required packages**
   ```bash
   pip install pyspark matplotlib seaborn pandas jupyter
   ```

3. **Start Jupyter Notebook**
   ```bash
   jupyter notebook
   ```

4. **Update Dataset Paths**
   Before running the analysis, you must update the file paths in the notebook:
   - Open `IPL-data-analysis.ipynb`
   - Replace all placeholder paths with actual paths to your dataset files:
     - `path_to_Ball_By_Ball.csv` → Your actual Ball_By_Ball.csv path
     - `path_to_Match.csv` → Your actual Match.csv path
     - `path_to_Player.csv` → Your actual Player.csv path
     - `path_to_Player_match.csv` → Your actual Player_match.csv path
     - `path_to_Team.csv` → Your actual Team.csv path

5. **Run the analysis notebook**
   Execute the cells sequentially after updating the paths

## 💻 Usage

### Important: Configure File Paths

**Before running any analysis**, you must update the dataset file paths in the notebook:

1. Open `IPL-data-analysis.ipynb`
2. Look for the data loading cells (cells 7, 11, 13, 15, 16)
3. Replace the placeholder paths with your actual file paths:

```python
# Example replacements needed:
ball_by_ball_df = spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("path_to_Ball_By_Ball.csv")
# Replace with:
ball_by_ball_df = spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("C:/your/actual/path/Ball_By_Ball.csv")

# Similarly for all other datasets:
# - path_to_Match.csv
# - path_to_Player.csv  
# - path_to_Player_match.csv
# - path_to_Team.csv
```

### Running the Analysis

1. **Initialize Spark Session**
   ```python
   from pyspark.sql import SparkSession
   spark = SparkSession.builder.appName('IPL-Analysis').getOrCreate()
   ```

2. **Load Data with Schemas**
   The notebook includes predefined schemas for all datasets ensuring data consistency.

3. **Execute Analysis Queries**
   Run the provided SQL queries to generate insights:
   - Top scoring batsmen analysis
   - Economical bowlers in powerplay
   - Toss impact analysis
   - Venue performance metrics

4. **Generate Visualizations**
   Create charts and graphs using matplotlib and seaborn for better insight presentation.

### Sample Analysis Queries

**Top Batsmen by Season:**
```sql
SELECT p.player_name, m.season_year, SUM(b.runs_scored) AS total_runs
FROM ball_by_ball b
JOIN match m ON b.match_id = m.match_id
JOIN player_match pm ON m.match_id = pm.match_id AND b.striker = pm.player_id
JOIN player p ON p.player_id = pm.player_id
GROUP BY p.player_name, m.season_year
ORDER BY m.season_year, total_runs DESC
```

**Economical Bowlers in Powerplay:**
```sql
SELECT p.player_name, AVG(b.runs_scored) AS avg_runs_per_ball
FROM ball_by_ball b
JOIN player_match pm ON b.match_id = pm.match_id AND b.bowler = pm.player_id
JOIN player p ON pm.player_id = p.player_id
WHERE b.over_id <= 6
GROUP BY p.player_name
ORDER BY avg_runs_per_ball
```

## 📊 Sample Visualizations

The project generates several types of visualizations:

1. **Bar Charts**: Most economical bowlers, top scorers
2. **Count Plots**: Toss impact analysis, dismissal type frequency
3. **Horizontal Bar Charts**: Venue-wise scoring analysis

## 🎯 Key Findings

- **Toss Impact**: Analysis reveals the correlation between toss outcomes and match results
- **Venue Factors**: Different venues show varying scoring patterns and advantages
- **Player Performance**: Identification of consistent performers across seasons
- **Bowling Economics**: Powerplay bowling strategies and their effectiveness

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-analysis`)
3. Commit your changes (`git commit -am 'Add new analysis'`)
4. Push to the branch (`git push origin feature/new-analysis`)
5. Create a Pull Request

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 👤 Author

**Adarsh Rout**
- GitHub: [@AdarshRout](https://github.com/AdarshRout)

## 🙏 Acknowledgments

- Indian Premier League for providing comprehensive cricket data
- Apache Spark community for excellent documentation
- Cricket analytics community for inspiration and methodologies

## 📧 Contact

For questions or suggestions, please open an issue on GitHub or contact the author directly.

---

### 🚀 Future Enhancements

- Real-time data processing capabilities
- Machine learning models for match outcome prediction
- Interactive dashboards using Streamlit or Dash
- Advanced player performance metrics
- Team composition optimization analysis
