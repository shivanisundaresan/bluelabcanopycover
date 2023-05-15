# BlueLabMetro Canopy Cover Carbon Offset
<img src="https://user-images.githubusercontent.com/113264909/232350711-e53e1769-a29a-4afc-9119-981a8ed2bd84.png" width="400" height="300">


## Who Are We and What Are Our Goals:
We are a group of 6 students at the University of Michigan who are all passionate about sustainability and engineering. We belong to the club BLUElab metro which focuses on sustainability initiatives on campus. With the help of another project team, we planted about 30 trees on campus, and our goal was to create a visualization that represented the carbon offset of those trees in Ann Arbor. 

## Background Information:
To start our project, we needed to research a couple things first. We looked into the types of trees we planted, and found many sources for how to calculate the carbon offset of each tree. We thought a lot about how our work would be utilized in our community so we discussed our project with many stakeholders, and considered how we can make our work accessible. 

## Calculators used:
While there are a wide variety of ways to calculate the carbon offset of trees, we found that using a combination of these two calcuatiors worked best with the data that we acquired. 
1. Tree height/dbh prediction:  https://data.nal.usda.gov/dataset/urban-tree-database
2. Carbon offset calculation: https://www.ecomatcher.com/how-to-calculate-co2-sequestration/ 


'''python
import pandas as pd

# Load data into a pandas DataFrame
df = pd.read_csv('https://gitlab.eecs.umich.edu/mandali/carbon-offset-calculator/-/raw/main/Felch_Park_Data__From_ArborPro__-_Sheet1.csv')

# Get user input for tree species
species = input("Enter the tree species: ")

# Filter DataFrame to only include trees of the specified species
species_df = df[df['Common'].str.contains(species, case=False)]

# Calculate the green weight, dry weight, weight of carbon, and weight of carbon dioxide for each tree
for index, row in species_df.iterrows():
    diameter = row['Exact DBH']
    height = row['Exact Height']
    if diameter < 11:
        above_ground_weight = 0.25 * diameter ** 2 * height
    else:
        above_ground_weight = 0.15 * diameter ** 2 * height
    total_green_weight = 1.2 * above_ground_weight
    dry_weight = 0.725 * total_green_weight
    weight_of_carbon = 0.5 * dry_weight
    weight_of_carbon_dioxide = 3.67 * weight_of_carbon
    print(f"Tree ID: {row['Tree ID']}, Weight of Carbon Dioxide Sequestered: {weight_of_carbon_dioxide:.2f} lbs")

# Calculate the total weight of carbon dioxide sequestered by all trees of the specified species
total_weight_of_carbon_dioxide = species_df.shape[0] * weight_of_carbon_dioxide
print(f"Total Weight of Carbon Dioxide Sequestered by {species_df.shape[0]} {species} Trees: {total_weight_of_carbon_dioxide:.2f} lbs")
'''
