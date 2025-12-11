# Real-Time-Student-Productivity-Prediction-System-Using-Machine-Learning
This project builds a real-time system that predicts student productivity using live inputs such as focus level, study hours, sleep, and mood. A machine learning model analyzes the data and provides an instant productivity score to help students improve their study habits and performance
## Steps I Followed

### 1️⃣ Data Collection
- Created a Google Form to collect daily habit and lifestyle data from CSE students.
- Collected responses for:
  - Sleep, wake-up time
  - Steps walked, water intake, exercise
  - Screen time, social media usage
  - Stress, mood, energy levels
  - Study/work hours, time spent outside
  - Goal completion status
- Exported the Google Form responses to a CSV file.

---

### 2️⃣ Loading and Initial Cleaning
- Loaded the CSV file into a pandas DataFrame using Python.
- Dropped the timestamp column (first column) as it was not needed for analysis.

---

### 3️⃣ Converting Text Ranges to Numeric Values
- Converted range-type inputs into numeric averages, for example:
  - `Sleep Hours (Last Night)`:  
    ` "5-6 hours"` → `5.5`
  - `Steps Walked Today(Approx)`:  
    `"8000-10,000"` → `9000`, `"10,000+"` → `10000`
  - `Water Intake(Glasses)`:  
    `"5-6"` → `5.5`, `"7-9"` → `8`
  - `Total Screen Time (Hours Today)`:  
    `"2-4 hours"` → `3`, `"4-6 hours"` → `5`
  - `Work/Study Hours Today (So far)`:  
    values like `"2 hours"`, `"3 hours"`, `"5+ hours"` → numeric hours

---

### 4️⃣ Handling Time-Based Features
- **Wake-up Time**:
  - Converted ranges like `"5-6 AM"`, `"6-7 AM"`, `"7-8 AM"` into average hours:  
    e.g. `"5-6 AM"` → `5.5`, `"7-8 AM"` → `7.5`
  - Mapped `"After 9 AM"` to `9.5`.
- **Time Spent Outside Today**:
  - Detected whether the value was in minutes or hours.
  - Converted:
    - `"30–60 minutes"` → `0.75` hours  
    - `"0–10 minutes"` → `0.083` hours  
    - `"1–2 hours"` → `1.5` hours  
    - `"2+ hours"` → `2` hours.
- **Social Media Usage Today**:
  - Converted minute ranges to hours as well, e.g.  
    `"30-60 min"` → `0.75` hours, `"0-30 min"` → `0.25` hours.

---

### 5️⃣ Encoding Categorical Features
- Encoded categorical/text columns into numeric values for machine learning:
  - `AGE`: `18-20` → `0`, `21-23` → `1`
  - `Gender`: `Male` → `1`, `Female` → `0`
  - `Breakfast`: `Yes` → `1`, `No` → `0`
  - `Exercise Today`:  
    - `No` → `0`  
    - `Yes, light (0-20 min)` → `1`  
    - `Yes, medium (20-45 min)` → `2`  
    - `Yes, intense (45+ min)` → `3`
  - `Caffeine Intake`:  
    `"0 cups"` → `0`, `"1 cup"` → `1`, `"2 cups"` → `2`, `"3 cups"` → `3`
  - `Weather (Your Area Today)`: mapped weather categories (e.g. `Cold`, `Pleasant`, etc.) to integers.
  - `Completed your goal today?`: `Yes` → `1`, `No` → `0`.

---

### 6️⃣ Final Cleaned Dataset
- Verified that all feature columns are numeric (`int` / `float`) using `df.dtypes`.
- Confirmed no unwanted text/object columns remain in the feature set.
- Saved the processed dataset as:  
  `cleaned_student_productivity.csv`

📊 Charts & Visualizations – Explanation

This project includes several visualizations to understand how different lifestyle factors affect student productivity. Each chart reveals meaningful insights from the dataset.

⭐ 1. Correlation Heatmap

This chart shows how strongly each feature is related to others, especially productivity-related factors.
It helps identify which variables (sleep, mood, stress, screen time, study hours, etc.) have the highest impact.


⭐ 2. Study Hours Boxplot

This boxplot visualizes the distribution of daily study/work hours among students.
It highlights average study patterns and detects outliers such as students studying very high or very low hours.


⭐ 3. Social Media Usage Boxplot

This chart shows variations in daily social media time.
It helps identify excessive usage outliers that may negatively impact mental state, focus, and productivity.


⭐ 4. Scatter Plot: Study Hours vs Productivity

This scatter plot shows the relationship between hours studied and the predicted productivity score.
It visually explains whether more study hours actually lead to higher productivity, or if diminishing returns exist.


⭐ 5. Steps Walked Distribution

This chart shows how physically active students are.
It also helps identify whether low activity levels align with lower energy or productivity scores.


📁 All charts are stored inside the charts/ folder

The complete set of visualization files can be found in the charts directory of this repository.

📌 Model, Prediction & Recommendation System (Today’s Work)

This section contains all the work completed today, focused on building the machine learning model, creating a user-input prediction system, and generating personalized habit recommendations for students.

✅ 1. Model Training (Decision Tree Regressor)

Today, I implemented the machine learning part of the project.
Three models were tested earlier (Linear Regression, KNN, and Decision Tree), and after evaluation, the Decision Tree Regressor performed the best based on:

R² Score

MAE (Mean Absolute Error)

RMSE (Root Mean Squared Error)

The Decision Tree model captures non-linear relationships between habits and productivity, making it the best fit for this dataset.

✅ 2. Prediction Function

A custom prediction function was created which takes the student’s daily lifestyle inputs and predicts their Productivity Score.

The function:

Accepts input values

Creates a structured DataFrame

Uses the trained model to generate a productivity score

Displays the final output

This allows the model to be used in real time by teachers or students.

✅ 3. User Input System (Interactive)

An interactive system was added where the user enters:

Sleep hours

Sleep quality

Study hours

Mood level

Stress level

Screen time

Exercise

Water intake

Steps walked

Social media usage

Caffeine intake

After entering values, the model immediately predicts the student’s productivity for the day.

✅ 4. Personalized Habit Recommendation Engine

A recommendation system was developed to help students improve their productivity based on their lifestyle data.

The system analyzes:

Sleep patterns

Screen time

Stress levels

Exercise activity

Water intake

Study routine

Steps walked

Mood & energy levels

Caffeine usage

Based on these values and the predicted productivity score, it provides personalized suggestions, such as:

Improve sleep to 7–8 hours

Reduce screen time

Practice Pomodoro study technique

Increase hydration

Add daily exercise

Reduce caffeine intake

Lower stress through short breaks or relaxation

This makes the project practical and actionable.

✅ 5. Final Output Example

After entering daily lifestyle information, the user receives:

📌 Predicted Productivity Score

A numeric score based on habits.

📌 Personalized Recommendations

A list of clear suggestions to improve productivity.

This turns the project from just a prediction model into a habit-improvement tool.

✔ “A Decision Tree Classifier is used to categorize students into Low, Medium, or High Productivity classes based on their daily lifestyle habits.”

If you want a slightly more detailed version:

✔ “The project uses a Decision Tree Classification model to predict the student’s productivity level (Low/Medium/High) from behavioral features such as sleep quality, stress, mood, energy, and screen time.”

Or a very short version:

✔ “Implemented a Decision Tree Classifier to classify students into productivity levels.”

🟦 Clustering Analysis

To understand hidden patterns in student productivity behavior, two unsupervised machine learning algorithms were applied:

K-Means Clustering

Hierarchical Clustering (Agglomerative)

These algorithms group students based on the similarity of their study habits, sleep duration, screen time, breakfast habits, and physical activity.

🔹 1. K-Means Clustering

K-Means is a partition-based clustering algorithm that divides the dataset into K clusters. Each cluster is formed around a centroid, which is the mean position of all points in that group.

Why K-Means?

Simple and fast

Works well for medium-sized datasets

Generates clear, separable clusters

Features Used

Study Hours

Sleep Hours

Screen Time

Breakfast (Yes/No)

Physical Activity (Yes/No)

📉 Elbow Method (Choosing K)

To determine the optimal number of clusters, the Elbow Method was used.
This method plots WCSS (Within-Cluster Sum of Squares) against different values of K.

✔ Interpretation of the Graph:

WCSS drops sharply from K = 1 to K = 3

After K = 3, the reduction becomes gradual

This indicates the “elbow point” at K = 3

🔍 Meaning:

When K = 3, clusters are well-separated while avoiding overfitting.
This suggests the dataset naturally forms three distinct groups of students based on productivity-related behaviors.

🔹 2. Hierarchical Clustering

Hierarchical clustering builds a tree-like structure called a dendrogram that shows how data points merge step by step.

The Agglomerative approach was used, which starts by treating every data point as a single cluster and then merges the closest clusters until only one remains.

Why Hierarchical Clustering?

Does not require specifying K initially

Provides a full visual hierarchy of clusters

Helps understand relationships between groups

🌳 Dendrogram (Cluster Visualization)

The dendrogram displays vertical lines representing the distance at which clusters merge.

✔ Interpretation of the Graph:

Major merges happen at three main branches

Cutting the dendrogram at an appropriate height (~12 units distance) results in 3 distinct clusters

This perfectly aligns with the K-Means elbow result

🔍 Meaning:

Hierarchical Clustering also suggests the presence of three meaningful groups, confirming the K-Means findings.

🟧 3. Comparison Between K-Means and Hierarchical Clustering
Aspect	K-Means	Hierarchical
Type	Partition-based	Tree-based
Needs K initially?	Yes	No
Visualization	Uses Elbow plot	Dendrogram
Speed	Faster	Slower
Best for	Larger datasets	Smaller datasets
Output	Centroids + clusters	Full hierarchy of clusters
✔ Result Consistency

Both algorithms independently suggested 3 clusters, adding confidence to the stability and reliability of the grouping.

🟩 4. Final Clustering Conclusion

Both K-Means and Hierarchical Clustering consistently identified 3 meaningful clusters among students.
These clusters likely represent different productivity lifestyles, such as:

Cluster 0: High study hours, good sleep, low screen time

Cluster 1: Moderate study/sleep habits

Cluster 2: Low study, high screen time, low physical activity

These patterns help identify different types of students and can be used later to provide tailored recommendations.

## 📘 app.py — Main Application File

The `app.py` file is the core of the Student Productivity Prediction System.
It handles the user interface, input processing, model loading, predictions,
and personalized recommendations using Streamlit.

### 🔹 Key Functions of app.py

1. **Loads all trained machine learning models**
   - `linear_reg.pkl` → Predicts productivity score
   - `tree_classifier.pkl` → Predicts productivity level (Low/Medium/High)
   - `scaler.pkl` → Standardizes input data for regression
   - `kmeans.pkl` & `kmeans_scaler.pkl` → Assigns behavioral cluster

2. **Collects user inputs through Streamlit sidebar**
   The user provides lifestyle details such as:
   - Sleep hours
   - Sleep quality
   - Caffeine intake
   - Exercise status
   - Screen time
   - Stress, mood, and energy levels
   - Study hours
   - Social media usage
   - Water intake
   - Steps walked

3. **Runs prediction only when the user clicks the "Predict" button**
   This prevents unnecessary calculations and makes the UI cleaner.

4. **Processes data and generates outputs**
   - Productivity Score (numeric)
   - Productivity Level (Low / Medium / High)
   - Cluster Group (0, 1, 2)
   - Personalized recommendations based on user habits

5. **Implements safety rules**
   Example:
   If the user sleeps more than 10 hours but studies very little,
   the model automatically adjusts the prediction and warns the user.

6. **Displays all results in a clean and organized format**

### 🧠 Summary
`app.py` is responsible for:
- User interaction  
- Sending inputs to ML models  
- Interpreting predictions  
- Providing recommendations  
- Building the main interface of the web app  

