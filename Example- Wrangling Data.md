### lets us discuss how class WranglingData(Stage) is used in EPL example to predit the data
# class WranglingData(Stage):

To create different Modulues and frameworks stages( ) are used and it also has multiple classes

It extends the stage class and acts as a skelton for other classess
      
        class WranglingData(Stage):
           
           def __init__(self):
          self.processed_data = pd.DataFrame()

#### let us see different functions involving Wranglingdata(stage)

There are 4 Functions which are used in Wranglingdata(stage)
##### clean_empty_data
      def clean_empty_data(self):
       self.processed_data.dropna(inplace=True)

This function clean the row containing empty field, that means this function deletes the row in the data folder if it contains any empty
field. Remove the row with the missing value of any attributes.

##### categorical_team_to_ordinal_value
        def categorical_team_to_ordinal_value(self, team):
        elite_team = ["""'Man United'""", 'Liverpool', 'Arsenal', 'Chelsea', 'Tottenham']
        semi_elite_team = ["""'Man City'""", 'Everton', """'Aston Villa'""", 'Newcastle', 'Wolves']
        pro_team = ["""'Nottingham Forest'""", 'Blackburn', """'Sheffield Wednesday'""", 'Sunderland',
                  """'Leeds United'"""]
        semi_pro_team = ["""'West Brom'""", """'West Ham'""", """'Sheffield United'""", 'Leicester', 'Portsmouth']

This categorical_team to ordinal value is used tp convert log value in the data tables to integer value and This function assign the
rank of each team.

##### normalize_data

     def normalize_data(self):
     columns_to_standardize = [['HomeTeam', 'AwayTeam', 'HS', 'AS', 'HST', 'AST', 'HF', 'AF', 'HC', 'AC', 'HR', 'AR']]

       for each_col in columns_to_standardize:
          self.processed_data[each_col] = normalize(self.processed_data[each_col])

This function normalizes the features on the columns_to_normalize. that means in the data obtained for data prediction the values for    some of the matches are too high and for some its too low,to make it between (0-1) the data is normailzed. This process can be useful if you plan to use a quadratic form such as the dot-product or any other kernel to quantify the similarity of any pair of samples.

##### shift_column

        def shift_column(self):
         temp_store = self.processed_data.pop('FTR')
         self.processed_data['FTR'] = temp_store
         
  This function shift column from middle to the last of the dataframe, for the training and testing purpose where 30 of it is testing and 70% is training. The training set contains a known output and the model learns on this data in order to be generalize to other data later on. We have the test dataset (or subset) in order to test our model's prediction on this subset.

### lets us discuss how class ModellingAndPrediction(Stage) is used in EPL example

# class ModellingAndPrediction(Stage):
In this stage the data is being predicted, Which includes three functions 

##### def prediction_report

     def prediction_report(self, real, prediction):
        h = 0
        a = 0
        d = 0
        for x in prediction:
            if x == "H":
                h = h + 1
            elif x == "A":
                a = a + 1
            else:
                d = d + 1
        print("Total home win: {0}".format(h))
        print("Total away win: {0}".format(a))
        print("Total draw: {0}".format(d))
        
It defines the total number of home wins and away wins in the prediction property, this function helps in predciting the total win 
This is the confusion matrix of Home win, Away win or Draw. It takes the avaerge of the home wins in two condidtions such as real results and predicted results.

##### def train_test_data

     feature_columns = ['HomeTeam', 'AwayTeam', 'HS', 'AS', 'HST', 'AST', 'HF', 'AF', 'HC', 'AC', 'HR', 'AR']

        x_data = self.processed_data[feature_columns]
        y_data = self.processed_data['FTR']

Function to create the training and test data,The data we use is usually split into training data and test data. The training set contains a known output and the model learns on this data in order to be generalized to other data later on. We have the test dataset (or subset) in order to test our model's prediction on this subset.

##### def combine_result
     def combine_result(self, x_test, y_test, y_predicted):
        print("this is the x test data {}".format(type(x_test)))
        print("this is the y result data {}".format(type(y_test)))
        print("this is the predicted data {}".format(type(y_predicted)))

It combines the test data and train data to predit value.

### lets us discuss how class DisplayOutput(Stage) is used in EPL example

# class DisplayOutput(Stage):
This class is used to display the outputs, there are no constructers overwriting the exciting & re-create the new one.
It incodes the value 0.1

This class consists of 2 functions,
##### def display_histogram

    def display_histogram(self, histo_data):
        print(type(histo_data))
        histo_values = histo_data.values
        print(type(histo_values))
        plt.hist(histo_values)
        plt.show()
        print("Display histogram is working fine.")
        
 The display histogram converts the data in the tables into histogram, and displays the output in the representation of the distribution of numerical data. It is an estimate of the probability distribution of a continuous variable.
 
##### def label_encoding

    def label_encoding(self, result_data):
        ftr_encoder = LabelEncoder()
        result_data['FTR_encoded'] = ftr_encoder.fit_transform(result_data.FTR)
        result_data['Predicted_FTR_encoded'] = ftr_encoder.fit_transform(result_data.Predicted_FTR)
        return result_data

Label encoding converts the labels into numeric form so as to convert it into the machine-readable form. Machine learning algorithms can then decide in a better way on how those labels must be operated. It is an important pre-processing step for the structured dataset in supervised learning.

