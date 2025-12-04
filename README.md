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

![Heatmap](charts/heatmap.png)

⭐ 2. Study Hours Boxplot

This boxplot visualizes the distribution of daily study/work hours among students.
It highlights average study patterns and detects outliers such as students studying very high or very low hours.

![Study Hours Boxplot](charts/boxplot_study_hours.png)

⭐ 3. Social Media Usage Boxplot

This chart shows variations in daily social media time.
It helps identify excessive usage outliers that may negatively impact mental state, focus, and productivity.

![Social Media Boxplot](charts/socialmedia_outliers.png)

⭐ 4. Scatter Plot: Study Hours vs Productivity

This scatter plot shows the relationship between hours studied and the predicted productivity score.
It visually explains whether more study hours actually lead to higher productivity, or if diminishing returns exist.

![Study vs Productivity](charts/scatter_study_productivity.png)

⭐ 5. Steps Walked Distribution

This chart shows how physically active students are.
It also helps identify whether low activity levels align with lower energy or productivity scores.

![Steps Distribution](charts/steps_distribution.png)

📁 All charts are stored inside the charts/ folder

The complete set of visualization files can be found in the charts directory of this repository.
