# Experiment 10 (`exp7.pdf`): Sentiment Analysis of Product Reviews Using TextBlob

## 🎯 Aim

To load product review text, perform sentiment polarity analysis using the `TextBlob` library, classify reviews into **Positive**, **Negative**, or **Neutral** categories, and visualize the overall sentiment distribution using a Matplotlib bar chart.

## 📝 Dataset & Classification Rules

The dataset consists of **10 sample product review strings** evaluated on a sentiment polarity scale ranging from $-1.0$ (most negative) to $+1.0$ (most positive):

* **Positive Sentiment:** $\text{Polarity} > 0.1$
* **Negative Sentiment:** $\text{Polarity} < -0.1$
* **Neutral Sentiment:** $-0.1 \le \text{Polarity} \le 0.1$

| # | Product Review | Polarity Score | Classified Sentiment |
| :---: | :--- | :---: | :---: |
| **1** | *"The product is amazing and works perfectly!"* | `0.80` | Positive |
| **2** | *"Very disappointed with the battery life."* | `-0.98` | Negative |
| **3** | *"Quality is okay but could be improved."* | `0.50` | Positive |
| **4** | *"Absolutely fantastic! Exceeded my expectations."* | `0.50` | Positive |
| **5** | *"Not worth the price at all."* | `-0.15` | Negative |
| **6** | *"Packaging was good and delivery was on time."* | `0.70` | Positive |
| **7** | *"The screen resolution is poor and camera is bad."* | `-0.55` | Negative |
| **8** | *"Loved the design and the features offered."* | `0.70` | Positive |
| **9** | *"Average product, nothing special."* | `0.10` | Neutral / Positive* |
| **10** | *"Excellent performance and great value for money!"* | `1.00` | Positive |

*\*Note: Due to floating-point representation in Python (`0.10357... > 0.1`), review #9 evaluates slightly above `0.1` and is classified as Positive.*

## ⚙️ Algorithm

1. **Start** the program.
2. **Import Libraries**: Import `TextBlob` from the `textblob` package for Natural Language Processing (NLP) sentiment analysis and `matplotlib.pyplot` as `plt` for bar chart visualization.
3. **Create Review Dataset**: Define a Python list `reviews` containing 10 sample customer product review strings.
4. **Initialize Sentiment Counters**: Set `positive = 0`, `negative = 0`, and `neutral = 0` to track category counts.
5. **Analyze & Classify Each Review**:
   * Iterate through each `review` in `reviews`.
   * Create a `TextBlob(review)` object and extract `polarity = analysis.sentiment.polarity`.
   * Classify the review:
     * If $\text{polarity} > 0.1$, label as `"Positive"` and increment `positive`.
     * Else if $\text{polarity} < -0.1$, label as `"Negative"` and increment `negative`.
     * Else, label as `"Neutral"` and increment `neutral`.
   * Display the review text, rounded polarity score, and assigned sentiment label.
6. **Display Summary Counts**: Print the total count of Positive, Negative, and Neutral reviews.
7. **Visualize Sentiment Distribution**:
   * Plot a bar chart using `plt.bar()` with sentiment categories on the X-axis and review counts on the Y-axis.
   * Add a title, axis labels, and render the chart via `plt.show()`.
8. **Stop** the program.

### 📋 Pseudocode

```text
BEGIN
    IMPORT TextBlob, matplotlib.pyplot AS plt

    INITIALIZE reviews ← LIST OF 10 product review strings
    positive ← 0, negative ← 0, neutral ← 0

    FOR EACH review IN reviews DO
        analysis ← TextBlob(review)
        polarity ← analysis.sentiment.polarity

        IF polarity > 0.1 THEN
            sentiment ← "Positive"
            positive ← positive + 1
        ELSE IF polarity < -0.1 THEN
            sentiment ← "Negative"
            negative ← negative + 1
        ELSE
            sentiment ← "Neutral"
            neutral ← neutral + 1
        ENDIF

        PRINT review, ROUND(polarity, 2), sentiment
    ENDFOR

    PRINT "Positive Reviews:", positive
    PRINT "Negative Reviews:", negative
    PRINT "Neutral Reviews:", neutral

    PLOT BAR_CHART(["Positive", "Negative", "Neutral"], [positive, negative, neutral])
    SHOW PLOT()
END
```

## 🛠️ Functions and Methods Used

| Category | Function / Attribute | Purpose / Description |
| :--- | :--- | :--- |
| **Sentiment Analysis** | `TextBlob(text)` | Wraps a text string in a TextBlob NLP object for linguistic analysis |
| | `.sentiment.polarity` | Computes a floating-point sentiment polarity score in the range $[-1.0, +1.0]$ |
| **Formatting & Math** | `round(polarity, 2)` | Rounds raw polarity scores to 2 decimal places for clean console output |
| **Visualization (Matplotlib)** | `plt.figure()`, `plt.bar()` | Initializes a figure window and renders a color-coded vertical bar chart |
| | `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.show()` | Configures chart title, axis labels, and displays the final visualization |

## 💻 Program / Code

```python
# Sentiment Analysis on Product Reviews using TextBlob
from textblob import TextBlob
import matplotlib.pyplot as plt

# Step 1: Create a list of sample product reviews
reviews = [
    "The product is amazing and works perfectly!",
    "Very disappointed with the battery life.",
    "Quality is okay but could be improved.",
    "Absolutely fantastic! Exceeded my expectations.",
    "Not worth the price at all.",
    "Packaging was good and delivery was on time.",
    "The screen resolution is poor and camera is bad.",
    "Loved the design and the features offered.",
    "Average product, nothing special.",
    "Excellent performance and great value for money!"
]

# Step 2: Initialize counters
positive = 0
negative = 0
neutral = 0

# Step 3: Analyze sentiment for each review
print("---- Sentiment Analysis Results ----")
for review in reviews:
    analysis = TextBlob(review)
    polarity = analysis.sentiment.polarity

    if polarity > 0.1:
        sentiment = "Positive"
        positive += 1
    elif polarity < -0.1:
        sentiment = "Negative"
        negative += 1
    else:
        sentiment = "Neutral"
        neutral += 1

    print(f"Review: {review}")
    print(f"Polarity: {round(polarity, 2)} | Sentiment: {sentiment}\n")

# Step 4: Display summary
print("---- Summary ----")
print("Positive Reviews:", positive)
print("Negative Reviews:", negative)
print("Neutral Reviews:", neutral)

# Step 5: Plot sentiment distribution
labels = ['Positive', 'Negative', 'Neutral']
values = [positive, negative, neutral]

plt.figure(figsize=(6, 4))
plt.bar(labels, values, color=['green', 'red', 'blue'])
plt.title("Sentiment Distribution of Product Reviews")
plt.xlabel("Sentiment Type")
plt.ylabel("Number of Reviews")
plt.show()
```

## 🖥️ Sample Output

```text
---- Sentiment Analysis Results ----
Review: The product is amazing and works perfectly!
Polarity: 0.8 | Sentiment: Positive

Review: Very disappointed with the battery life.
Polarity: -0.98 | Sentiment: Negative

Review: Quality is okay but could be improved.
Polarity: 0.5 | Sentiment: Positive

Review: Absolutely fantastic! Exceeded my expectations.
Polarity: 0.5 | Sentiment: Positive

Review: Not worth the price at all.
Polarity: -0.15 | Sentiment: Negative

Review: Packaging was good and delivery was on time.
Polarity: 0.7 | Sentiment: Positive

Review: The screen resolution is poor and camera is bad.
Polarity: -0.55 | Sentiment: Negative

Review: Loved the design and the features offered.
Polarity: 0.7 | Sentiment: Positive

Review: Average product, nothing special.
Polarity: 0.1 | Sentiment: Positive

Review: Excellent performance and great value for money!
Polarity: 1.0 | Sentiment: Positive

---- Summary ----
Positive Reviews: 7
Negative Reviews: 3
Neutral Reviews: 0
```

## ✅ Result

The program successfully loads a list of sample product reviews, applies `TextBlob` sentiment polarity scoring to classify each review's emotional tone, prints summary counts, and visualizes the overall distribution with a Matplotlib bar chart.

## 🚀 How to Run

1. Install `textblob` and `matplotlib` (if not already installed):
   ```bash
   pip install textblob matplotlib
   ```
2. Run the script:
   ```bash
   python exp7_sentiment_analysis.py
   ```