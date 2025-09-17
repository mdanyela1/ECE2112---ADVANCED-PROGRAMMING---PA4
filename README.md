# ECE2112---ADVANCED-PROGRAMMING---PA4
# SACABEN, MARIA DANIELA C. 2ECE-C

# ECE Board Exam Data Analysis Project
# Overview
This project demonstrates data wrangling and data visualization with storytelling using the dataset `board2.csv`, which contains mock results of students in the ECE Board Exam subjects.

The objective is to:
1. Create filtered DataFrames based on given conditions.
2. Perform exploratory analysis to evaluate how track, gender, and hometown affect the average scores of students.
3. Provide visual storytelling through bar charts to highlight patterns and insights.

# Dataset Information

<img width="805" height="570" alt="image" src="https://github.com/user-attachments/assets/1f8a4970-3a28-415e-825a-681e4a5e7eca" />

# Step 1: Importing Libraries
`import pandas as pd`
`import matplotlib.pyplot as plt`

# Step 2: Loading the Dataset

#Load dataset
`df = pd.read_csv("board2.csv")`

#Preview first rows
`print(df.head())`

# Step 3: Data Wrangling (Creating Subsets)
# a. Vis DataFrame
- Condition: Students from Visayas with Math < 70.
- Columns: `Name`, `Gender`, `Track`, `Math`

`Vis = df[(df["Math"] < 70) & (df["Hometown"] == "Visayas")]`
`Vis = Vis[["Name", "Gender", "Track", "Math"]]`
`print("V DataFrame:")`
`print(Vis)`

Sample Output:

<img width="379" height="111" alt="image" src="https://github.com/user-attachments/assets/cb25d8ca-9f0b-495e-9b5a-ca9da2d2d74d" />

# b. Instru DataFrame
- Condition: Students in Instrumentation, from Luzon, with Electronics > 70.
- Columns: `Name`, `GEAS`, `Electronics`

`Instru = df[(df["Electronics"] > 70) & `
            `(df["Track"] == "Instrumentation") & `
           ` (df["Hometown"] == "Luzon")]`
`Instru = Instru[["Name", "GEAS", "Electronics"]]`
`print("\nInstru DataFrame:")`
`print(Instru)`

Sample Output: 

<img width="258" height="124" alt="image" src="https://github.com/user-attachments/assets/30068dcf-5e0a-493c-8f4c-08fc91cf0bc6" />

# c. Mindy (Min) DataFrame
- Condition: Female students from Mindanao, with Average ≥ 55.
- Columns: `Name`, `Track`, `Electronics`, `Average`

`df["Average"] = df[["Math", "GEAS", "Electronics"]].mean(axis=1)`

`Min = df[(df["Average"] >= 55) & `
         `(df["Hometown"] == "Mindanao") & `
        ` (df["Gender"] == "Female")]`
`Min = Min[["Name", "Track", "Electronics", "Average"]]`
`print("\nMin DataFrame:")`
`print(Min)`

Sample Output:

<img width="470" height="133" alt="image" src="https://github.com/user-attachments/assets/a58bf61c-20cf-407b-a16c-85838a30c372" />

# Visualization & Storytelling

#Average grade for each student
`df["Average"] = df[["Math", "GEAS", "Electronics"]].mean(axis=1)`

#Group by Track, Gender, and Hometown
`avg_by_track = df.groupby("Track")["Average"].mean()`
`avg_by_gender = df.groupby("Gender")["Average"].mean()`
`avg_by_home = df.groupby("Hometown")["Average"].mean()`

#Plot results
`plt.figure(figsize=(15,5))`

#Average by Track
`plt.subplot(1,3,1)`
`avg_by_track.plot(kind="bar", color="skyblue", edgecolor="black")`
`plt.title("Average Grade by Track")`
`plt.ylabel("Average Grade")`

#Average by Gender
`plt.subplot(1,3,2)`
`avg_by_gender.plot(kind="bar", color="salmon", edgecolor="black")`
`plt.title("Average Grade by Gender")`

#Average by Hometown
`plt.subplot(1,3,3)
`avg_by_home.plot(kind="bar", color="lightgreen", edgecolor="black")`
`plt.title("Average Grade by Hometown")`

`plt.tight_layout()`
`plt.show()`

Sample Output:

<img width="1382" height="431" alt="image" src="https://github.com/user-attachments/assets/2bc09873-f83f-4fff-b090-342cf42ecbe0" />

# Insights from Visualization
1. By Track
- Some tracks (e.g., Instrumentation or Microelectronics) tend to have higher averages compared to Communication.
- Suggests specialization influences performance in board-related subjects.
2. By Gender
- Both male and female students show comparable average scores, with only slight differences.
- Gender is not a strong predictor of performance.
3. By Hometown
- Luzon/Visayas students may have slightly higher averages compared to Mindanao.
- Could indicate differences in educational resources or preparation background.

# How to Run the Project
1. Ensure you have Python 3.x installed.
2. Install dependencies:
   `pip install pandas matplotlib`
3. Place `board2.csv` in the same directory as the script.
4. Run the script:
   `python ece_board_analysis.py`
















