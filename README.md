## Report & Analysis

  <summary>Contents</summary>
  <ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#dpp">Data Preprocessing</a></li>
    <li><a href="#cte">Compiling, Training, & Evaluation</a></li>
    <li><a href="#results">Results</a></li>
    <li><a href="#summary">Summary</a></li>
  </ol>

### Overview
<a name="overview"></a>
The goal of this project was to build a binary classification model using Tensorflow and Keras to predict the success of organizations funded by Alphabet Soup, a nonprofit.

### Data Preprocessing
<a name="dpp"></a>
- **Model target**: Success of funded organizations
  - "IS_SUCCESSFUL"
- **Features used in the model**: 
  - "NAME"
  - "APPLICATION_TYPE"
  - "AFFILIATION"
  - "CLASSIFICATION"
  - "USE_CASE"
  - "ORGANIZATION"
  - "STATUS"
  - "INCOME_AMT"
  - "SPECIAL_CONSIDERATIONS"
  - "ASK_AMT"

- "EIN" was not useful for prediction since it's an ID number, so I removed it.
- "NAME" was initially removed for the first model, then added back.
- "APPLICATION_TYPE" and "CLASSIFICATION" column values were binned, which reduced variability in those features (basically helped reduce noise, which helps the model's accuracy. This is why better binning gave the 2nd model a boost in accuracy).
- All categorical values were converted to numeric (1's & 0's for binary classification)
- I used a 60-40 train/ test split (60% of data for training, 40% for testing/ predicting)
- I scaled the data using StandardScaler 

### Compiling, Training, & Evaluation
<a name="cte"></a>
**Neurons, layers, and activation functions**:
- Model 1: 1 hidden layer w/ 30 neurons and ReLU6 activation function, and the output layer had 1 neuron w/ sigmoid activation function, which is useful for binary classification.

- Model 2: A sequential model with 2 hidden layers consisting of 20 and 10 neurons, both with reLU6 activation function, and a 1 neuron output layer w/ sigmoid activation function.

- Both models used binary_crossentropy function to measure loss and accuracy as the primary performance metric.

- Both models were run for 10 epochs, since the rate of change in accuracy was not really worth the extra time it took to run the model for 20, 50 or 100 epochs.

### Results
<a name="results"></a>
- **Model 1 performance**: loss: 0.5611 - accuracy: 0.7290

- **Changes made to model**: 
    - Made changes to binning of "CLASSIFICATION" and "APPLICATION_TYPE"
    - Re-added "NAME" feature column
    - Slightly modified neural network structure by adding 1 hidden layer. Total number of neurons (30) was the same for both models

- **Model 2 performance**: loss: 0.3962 - accuracy: 0.8119

### Summary
<a name="summary"></a>

- **Performance**: Improved model accuracy by ~8.29%


Changing the binning of the APPLICATION_TYPE and CLASSIFICATION features reduced noise in those features and made the model perform better.

Interestingly, organization name had an effect on model performance. This makes some intuitive sense, since an organization's name is the first piece of information that is judged when considering it in any context. So, organizations with names that are more familiar or associated with things someone deems positive might be more likely to receieve funding or to move further in the funding process. This effect is also present in the job application process, to the point that many companies remove names from resumes before a human reads them in order to reduce racial bias.

To identify the exact difference adding the NAME feature had on model performance, I would have to get weights for each feature before & after running the model - maybe in a future project.
