# English Premier League (EPL) Match Analytics with Spark and HDFS

This project processes live-streamed English Premier League (EPL) match data using **Spark Streaming** and **HDFS** for fault-tolerant storage. The processed data includes match details, player ratings, chemistry between players, and more. These outputs are used for analytics and match predictions through a query interface. The complete details of the process can be found in [REPORT](./REPORT.md)

## Features
1. Real-time data ingestion and processing using **Spark Streaming**.
2. Scalable, distributed storage with **HDFS** for intermediate and final outputs.
3. Fault-tolerant computations with **Spark checkpointing**.
4. Detailed analytics and match predictions.

## Requirements
### System Prerequisites
- Python 3.8 or higher
- Hadoop (HDFS) installed and running locally
- Java 8 or higher
- Apache Spark
- Virtual environment for Python dependencies

## Project Setup

### 1. HDFS Setup
#### Install and Configure HDFS
- Ensure Hadoop is installed on your system. If not, install it using [Apache Hadoop installation guide](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html).
- Start and verify the running of HDFS
- Create Required HDFS Directories
```bash
hdfs dfs -mkdir -p /input
hdfs dfs -mkdir -p /output
```

### 2. Streaming Service
Start the **streaming service** to generate live EPL match data:
```bash
python stream.py
```
This will stream data to port `6100` for Spark Streaming to process.

### 3. Process the streamed data and stores intermediate and final results in HDFS:
1. Start the Spark application by running:
   ```bash
   python master.py
   ```
2. The program will:
   - Read streamed data from the streaming service.
   - Process the data in real time.
   - Store outputs to HDFS directories under `/output/`.

Expected output directories in HDFS:
- `/output/players2.json`
- `/output/player_ratings.json`
- `/output/players_chemistry.json`
- `/output/matches_details.json`


### 4. Running the query interface
The **query interface** uses the processed data from HDFS for analytics and prediction.

Get the inputs reqdy for queries, 
- `inp_player.json` for player profile queries.
- `inp_match.json` for match information.
- `inp_predict.json` for match predictions.
  
1. Start the interface:
   ```bash
   python query_interface.py
   ```

The system will generate the corresponding output files
- `out_player.json` for player profiles.
- `out_match.json` for match insights.
- `out_predict.json` for match prediction results.

## Workflow Summary
1. Set up and start HDFS.
2. Start the streaming service (`stream.py`) for live EPL match data.
3. Run `master.py` to process streamed data with Spark and store results in HDFS.
4. Start the UI (`query_interface.py`) for analytics and predictions.