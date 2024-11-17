# English Premier League Football Analytics Project

## Overview
This project leverages Apache Spark Streaming and Spark MLLib to process and analyze real-time football match data from the English Premier League. It consists of two main components:

1. **Data Processing (`master.py`)**: Handles real-time streaming of match events, processes player and match statistics, and computes key metrics.
2. **Analytics Interface (`ui.py`)**: Provides post-processing analytics, such as clustering players, calculating chemistry statistics, and predicting match outcomes using machine learning.

## Features
- **Real-Time Data Processing**:
  - Processes live match data streams using Spark Streaming.
  - Tracks individual player metrics, including:
    - Goals, fouls, shots on target, and pass accuracy.
    - Chemistry and performance trends.
  - Aggregates and updates metrics for the entire stream.

- **Post-Match Analytics**:
  - Clustering players based on performance using K-Means (Spark MLLib).
  - Match prediction using trained machine learning models.
  - Chemistry analysis to evaluate player relationships and team dynamics.
  - Player and match data queries with JSON-based output.

## Architecture
1. **Real-Time Data Processing** (`master.py`):
   - Sets up a Spark Streaming pipeline to process match events from a socket stream.
   - Reads and processes data from input CSV files (`players.csv`, `teams.csv`).
   - Updates player and team statistics in real-time.
   - Supports fault-tolerant streaming with checkpointing.

2. **Analytics and Interface** (`ui.py`):
   - Reads processed data for further analysis.
   - Implements machine learning models like K-Means for clustering players based on performance metrics.
   - Predicts match outcomes using Spark MLLib's regression techniques.
   - Exports results as JSON for easy integration with external systems.

## Usage

### Running the Real-Time Data Processing
1. Start a socket server on port `6100` to feed match data.
2. Run the streaming script:
   ```bash
   python master.py
   ```
3. The script will process data streams and update metrics in real-time.

### Performing Post-Match Analytics
1. Run the analytics interface:
   ```bash
   python ui.py
   ```
2. Use the following functions for analytics:
   - **Player Profile**: Query specific player data by name.
   - **Match Details**: Retrieve match details by label.
   - **Clustering**: Cluster players into groups based on performance metrics.
   - **Match Prediction**: Predict match outcomes using processed data.

## File Descriptions
- **`master.py`**:
  - Handles real-time streaming and processing of match events.
  - Reads input files (`players.csv`, `teams.csv`) and initializes metrics for players and teams.
  - Updates metrics such as goals, pass accuracy, and fouls during the match.

- **`ui.py`**:
  - Provides an interface for querying and analyzing processed data.
  - Implements clustering and prediction algorithms using Spark MLLib.
  - Outputs results to JSON files for integration or visualization.

## Example Outputs
- Player Profile:
  ```json
  {
      "Id": "1",
      "name": "John Doe",
      "number_of_goals": 5,
      "pass_accuracy": 87.5,
      "role": "Midfielder"
  }
  ```
- Match Details:
  ```json
  {
      "match_id": "EPL123",
      "teams": ["Team A", "Team B"],
      "score": "2-1",
      "man_of_the_match": "John Doe"
  }
  ```
