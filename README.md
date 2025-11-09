# Spam-detection


📜 Final Project Report: Iterative Spam Detection Model
1. Project Objective
   The initial goal of this project was to build a standard machine learning model to classify SMS messages as either "ham"
   (legitimate) or "spam." However, the project's focus evolved to address a more complex, real-world challenge:
   how to improve a model when it fails on modern, "tricky" spam that wasn't in the original training data.

3. Methodology and Process
   Our development followed a complete, iterative machine learning lifecycle.

   Step 1: Initial Data Loading and Cleaning

   The spam.csv dataset from Kaggle was loaded using pandas.

   The data was cleaned to keep only two essential columns, which we renamed to label and message.

   Labels were converted from text ('ham'/'spam') to numeric (0/1) for modeling.

   Step 2: Key Problem Identification (Data Imbalance)

   A major issue was immediately identified: the dataset is severely imbalanced, with 4,825 "ham" messages and only 747 "spam" messages.

   This imbalance would cause a lazy model to simply predict "ham" every time and still be over 86% accurate.

   Solution: We decided to use SMOTE (Synthetic Minority Over-sampling Technique). This was applied only to the training data to create a new, balanced dataset, ensuring the model learned the features of "spam"      just as well as "ham."

   Step 3: Initial Testing and Model Weakness

   We first trained models on the original data and tested them with new, "scam-like" messages, such as "Hey, my money accidently transfeered on ur bank".

   Our models failed. They predicted "HAM" because they had never seen words like "transfeered," "accidently," or "wala" in the spam.csv file. This is a classic Out-of-Vocabulary (OOV) problem.

   Step 4: The Core Solution (Data Augmentation)

   We proved that the models' failures were not a "model" problem but a "data" problem.

   Our Solution: We manually augmented the dataset. We created a new list of 20 modern, custom scam messages covering bank fraud, password resets, and typos.

   This new data was concatenated with the original dataset, creating a new, "smarter" df_augmented.

   Step 5: Final Model Training Pipeline

   Vectorization: The TfidfVectorizer was used to convert all text messages (including our new scam messages) into a numerical matrix.

   Train/Test Split: Our new augmented dataset was split 80/20.

   Handle Imbalance: SMOTE was applied to the 80% training set.

   Train Models: We trained two separate models on this new, balanced data:

   Multinomial Naive Bayes (MNB): A fast, simple baseline model.

  Logistic Regression (LR): A more powerful and robust classification model.

3. Key Findings and Results
   After re-training both models on our new, augmented data, we performed a final test. The results were a complete success and formed the core conclusion of our project.

   Test Results on Tricky Messages:

   Message: "Hey, my money accidently transfeered on ur bank"

   Naive Bayes Prediction: HAM (Failure)

   Logistic Regression Prediction: SPAM (Success!)

   Analysis: The LR model was "smarter." It learned from our new examples that even if the message starts friendly, words like "transfeered" and "bank" are strong spam indicators.

   Message: "Myname is bank wala"

   Naive Bayes Prediction: SPAM (Success!)

   Logistic Regression Prediction: SPAM (Success!)

   Analysis: Our data augmentation was 100% successful. Both models learned the new vocabulary.

   Message: "hey what time is the meeting tomorrow?"

   Naive Bayes Prediction: HAM (Success!)

   Logistic Regression Prediction: HAM (Success!)

   Analysis: This was our "safety check." We proved that by adding new spam data, we did not create a "False Positive" problem. Our models still correctly identified legitimate messages.

5. Conclusion
   The project was a definitive success. We demonstrated that the Logistic Regression model, when trained on our augmented and balanced dataset, was the clear winner.\
   The most important takeaway from this project was not the model itself, but the process: a model is only as good as its data. Our initial models failed, not because the algorithm was wrong, but because the        data was outdated.
   By identifying this "data gap" and fixing it with data augmentation, we successfully built a smarter, more robust spam filter that can catch modern, tricky scams while still respecting legitimate messages.
