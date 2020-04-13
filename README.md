Logistics and Supply Chain Analytics
Individual Project:

Demand Forecasting for A Fast-Food Restaurant Chain
Deadline: 10am, March 10, 2020

1) Overview:

The dataset is provided by one of the largest fast-food restaurant chains in the US. It includes (1)
transaction information such as menu items that were purchased and quantities of each item; (2)
ingredient lists for individual menu items; (3) metadata on restaurants, including location, and store
type. The data observation window is from early March, 2015 to 06/15/2015 and includes transactional
data from 2 stores in Berkeley, CA and 2 stores in New York, NY.

Your job is to forecast the daily demand for the next two weeks (from 06/16/2015 to 06/29/2015) to
help the managers make inventory replenishment decisions. In particular, you need to forecast demand
for one specific ingredient: lettuce, for each of the four individual restaurants. You are expected to use
both Holt-Winters and ARIMA methods in generating the forecast. The deliverable of the coursework
includes a written report (submit both rmd file, and pdf/html file), and the forecast results summarized
in a csv file.

Your submission will be evaluated based on the following criteria:

1. Proper application of Holt-Winters model (15%);

2. Proper application of ARIMA model (25%);

3. Performance comparison between Holt-Winters and ARIMA (25%): provide evidence and/or
justification to support your arguments;

4. Accuracy of your forecasts (35%).
(Your results will be compared against the real sales over the two-week period based on mean
squared deviation)

2) Data Description:

Table 1: pos_ordersale
Column Name Data Type Notes
MD5KEY_ORDERSALE String Unique identifier for the order in POS
ChangeReceived Decimal Change received from the sale
OrderNumber Integer Order number, unique to the store
TaxInclusiveAmount Decimal Tax amount added to the price of a transaction
posTaxAmount Decimal Tax value
MealLocation Integer Values:0-Eat in, 1-ToGo
TransactionId Integer Transaction ID number
StoreNumber String Store number.
Corresponds to ’STORE_NUMBER’ in store_restaurant
date Datetime Date of the transaction
Row description: Franchisee point of sale transaction

Table 2: menuitem
Column Name Data Type Notes
MD5KEY_MENUITEM String Unique identifier for the purchased menu item
MD5KEY_ORDERSALE String Unique identifier for the POS order
Corresponds to ’MD5KEY_ORDERSALE’ in pos_ordersale
StoreNumber Integer Store number
Corresponds to ’STORE_NUMBER’ in store_restaurant
date Datetime Date of the transaction
TaxInclusiveAmount Decimal Tax amount added to the price of an item
TaxAmount Decimal Tax value
AdjustedPrice Decimal Price of the item after discount adjustment
DiscountAmount Decimal Amount of discount
Price Decimal Original price
Quantity Integer Quantity of the purchased item
PLU Integer Unique identifier for the recipe associated with this menuitem
Corresponds with ’PLU’ in menu_items
CategoryDescription String Item category description (hierarchy of 3 levels)
DepartmentDescription String More detailed item description
Description String Most detailed item description
Id Integer Unique identifier for associated menu item in menu_items
Row description: Purchased menu item associated with a single transaction in pos_ordersale
Remark: Purchased menu items in menuitem are matched to menu items in menu_items on menuitem.
PLU and menuitem.Id and menu_items.PLU and menu_items.MenuItemId.

Table 3: store_restaurant
Column Name Data Type Notes
STORE_NUMBER String Unique identifier for the store
STORE_ADDRESS1 String First line of store address
STORE_ADDRESS2 String Second line of store address
DISTRIBUTION_REGION String Store’s region
STORE_STATE String Store’s state
STORE_ZIP String Store’s zip code
STORE_TYPE String Indicates type of store
Row description: A store (or restaurant) location

Table 4: menu_items
Column Name Data Type Notes
MenuItemId Integer Unique identifier for the menu item
MenuItemName String Abbreviated description of the menu item
MenuItemDescription String Detailed description of the menu item
PLU String Unique identifier for the recipe associated with this menu item
RecipeId Integer Unique identifier for the recipe.
Corresponds with ’RecipeId’ in recipes
Row description: A menu item associated with a franchisee recipe
Remark: Purchased menu items in menuitem are matched to menu items in menu_items on menuitem.
PLU and menuitem.Id and menu_items.PLU and menu_items.MenuItemId

Table 5: recipes
Column Name Data Type Notes
RecipeId Integer Unique identifier for the recipe
RecipeName String Abbreviated name of the recipe
RecipeDescription String Full name of recipe
Row description: A recipe for a menu item

Table 6: recipes_ingredient_assignments
Column Name Data Type Notes
RecipeId Integer Unique identifier for the recipe.
Corresponds with ’RecipeId’ in recipes
IngredientId Integer Unique identifier for the ingredient.
Corresponds with ’IngredientId’ in ingredients
Quantity Decimal Quantity of specific ingredient used in that recipe
Row description: A single recipe

Table 7: recipe_sub_recipe_assignments
Column Name Data Type Notes
RecipeId Integer Unique identifier for the recipe.
Corresponds with ’RecipeId’ in recipes
SubRecipeID Integer Unique identifier for the sub-recipe.
Corresponds with ’SubRecipeID’ in sub_recipes
Factor Decimal Quantity of specific SubRecipeID used in RecipeID
Row description: A single sub-recipe

Table 8: sub_recipes
Column Name Data Type Notes
SubRecipeId Integer Unique identifier for the sub-recipe
SubRecipeName String Name of sub-recipe
SubRecipeDescription String Description of sub-recipe
Row description: Sub-recipe associated with a recipe

Table 9: sub_recipe_ingr_assignments
Column Name Data Type Notes
SubRecipeId Integer Unique identifier for the sub-recipe.
Corresponds with ’SubRecipeId’ in sub_recipes
IngredientId Integer Unique identifier for the ingredient.
Corresponds with ’IngredientId’ in ingredients
Quantity Decimal Quantity of ingredient used in the sub-recipe
Row description: A single ingredient within a sub-recipe

Table 10: ingredients
Column Name Data Type Notes
IngredientId Integer Unique identifier for the ingredient
IngredientName String Ingredient full name
IngredientShortDescription String Ingredient short description
PortionUOMTypeId Integer Portion unit of measure
Corresponds with ’PortionUOMTypeId’ in portion_uom_types
Row description: An ingredient used in a franchisee recipe

Table 11: portion_uom_types
Column Name Data Type Notes
PortionUOMTypeId Integer Unique identifier for the unit of measurement
PortionTypeDescription String Text description of unit of measurement
Row description: Portion (or unit of measurement) for an ingredient
