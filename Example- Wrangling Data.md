### lets us discuss how class WranglingData(Stage) is used in EPL example to predit the data
# WranglingData(Stage)

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


