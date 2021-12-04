# Lesson 1 : Series

## Intro to Attributes

* s.values
* s.index
* s.dtype
* s.is_unique ( is every value unique )
* s.name
* s.size
* s.shape

## Intro to Methods

* s.sum()
* s.mean()
* s.product()
* s.medain()
* s.mode()
* s.describe()
--------------
* s.sort_values()
* s.head()
* s.tail()
* s.sort_index()
* s.get(keys , default = None)
* s["a" : "b"]
* s.count() 
  *  excludes NaN values
* s.idxmax() 
  *  index position that has the smallest value
* s.idxmin() 
  *  index position that has the largets value
* s.value_counts()
  *  Takes all the values and tells how many times each value appers
  *  important method
*  s.apply(fxn)
   *  apply a method all the values of the series
*  s.map(series_2) 
   *  maps values of s to indices of series_2 and returns a new series 


# Lesson 2 : Data Frames

* Whenever a column has NaN values the values in that columns is stored as floating point numbers
----
* df.head()
* df.tail()
* df.describe()
* df.info()
* df.index
* df.values
* df.shape
* df.dtype
* df.columns
* df.axes
----
* df.sum(axis = 1/0)
* Extract a column from df
  - df["Name"]
* Extract Two or more Columns from a df
  * df[["Name", "Number", "Position"]]
* Add new Column to df
  * df["sport"] = "Basketball"
  * df["sport"] = some_series
  * df.insert(pos, column = "sport", value = "Basketball")
  * df.insert(pos, column = "sport", value = maybe a series)
  
* Broadcasting Operations
  * df["Age"] + 5
  * df["Age"] - 5
  * df["Age"] * 5
* Review of `value_counts`
  * It is available only for series
  * extraxt a series and do `value_counts`
* drop NaN values
  * df.dropna(inplace = True)
  * by default any row having NaN will be removed
  * You can change this way using **how** parameter
  * df.dropna(**axis = 1**), any columns having NaN values are dropped
  * df.dropna( **subset = ["Salary"]**), only if NaN is in salary column that particular row is dropped else it is not dropped
* Fill in Null Values with `.fillna()` Method
  * direct df.fillna(0) doesnt make sense all the time
  * Call on each series indivudually
  * df["Salary"].fillna(0, inplace = True)
  * df["College"].fillna("No College", inplace = True)
* The `.astype()` Method
  * Remove all the NaN values
  * df["Salary"].astype("int")
  * df["College"].astype("String")
* `category` data type in Pandas
  * df["Position"].astype("category")
  * If the unique values are very less in number

* `sort_values` on df
    * df.sort_values("Name", ascending = True)
    * Change the NaN position bu using **na_position** parameter
    
* `sort_values` on multiple columns
    * df.sort_values(["name", "Salary"], ascending = [True, False])
    
* `sort_index`
    * df.sort_index( ascending = True , inplace  = True)

* `rank()` Method on Series
    * Remove Null values
    * df["Salary"].rank(ascending = False).astype("int")


## Lesson 3 : Filtering Data

* pd.to_datetime( df["Start Date"] )
    * pass a series to chnage it to the datetime type


* Initially when a Dataset is presented first change the types of columns appropriately for the furthur operations to go smooth


* Instead of manual date time change you can use **parse_dates** parameter in `read_csv()`


##### Filter Based on a Condition

* df["Gender"] == "Male" returns a boolean series

* To extract the rows following a condition pass the boolean series to df
    * df[ df["Gender"] == "Male" ]
   
   
* More than one condition
    * df[( df["Gender"] == Male ) & ( df["Salary"] > 1000000 ) ]
    * df[( df["Gender"] == Male ) |  ( df["Salary"] > 1000000 ) ]
    
    
* `isin()` Method
    * It optimizes the above process
    * df["Team"].isin(["Marketing", "Legal"]) returns a boolean series whenever the column has Marketing ot Legal
  
  
* `.isnull()` and `.notnull()` Methods
    * df["Team"].isnull() returns a boolean series
    * df["Team"].notnull() returns a boolean series
   
   
* `.between()` between lower bound and upper bound
    * df["Salary"].between(60000,700000) returns a boolean series
    * can take dates, times, floats
        

* `.duplicated()` -> boolean array on a series
    * df["First Name"].duplicated( keep = 'last'/ 'first'/ False)
    * False implies all the duplicates are cosidered duplictes
 
 
* `drop_duplicates()`  applicable on a DF
    * by default drops only rows that are completely the same
    * df.drop_duplicates( subsets , keep ) 
    
    
* `.unique()` and `nunique()` on a series
    * gives unique values -> `.unique()`
    * gives number of unique values -> `.nunique()`
   

## Lesson 3 : Data Extraction

* `set_index()` and `reset_index()`
    * df.set_index( keys = "Film" ) , makes Film column the index
    * df.reset_index(), back to the numerical indexing
    * you can drop the exisiting index using **drop**
    
    
* Retrive Rows using `.loc[]` 
    * df.loc["A index name"]
    * Remember Indexes could be the same ( no problem )
    * supports list slicing, df.loc["Diamonds Are Foreevr": "Saccred Eye"]
    * Right end point is included
    * All the python slicing methods works
    
    
* Retrieve Rows using index location
    * df.iloc[1:5]
    * df.iloc[1:15:3]


* second Arguments to `loc` and `iloc`
    * df.loc["Arow_name", "Acol_name"]
    * df.loc["Arow_name", ["a1col", "a2col"]]
    * you can slice in the both the indices
    * same things apply for **iloc**
   
   
* Set a new value for a specific cell
    * df.loc["Hello","bye"] = "Something"
    * df.loc["A", ["B", "C"]] = a list



* Set Multiple Values in DataFrame
    * When you do df[df["A"] == b] this creates a new dataframe altogether and is not the original dataframe
    * df.loc[mask] this doesnt create a new dataframe rather this is just a slice from original dataframe
    * df.loc[mask, "A"] = anything
    * This is the correct method
   
   


* Remame Index labels or Column Labels
    * df.remane(mapper = dict, axis = 0), dict is a mapping function.
    * df.remane( index = dict ), same dict
    * df.rename( columns = dict ), same dict
    * for a bulk remane use, df.columns = [list]
    * for a bulk remane use, df.rows = [list]
    
    
    
* delete Rows or columns in a Dataframe
    * df.drop( labels , axis )
        * labels are the row indices
        * axis is the rows/columns
     * df.pop("Actor"), returns the Actor Col and also removes it from the dataframe
     * del df["Director"]
     

* Create Random Sample
    * df.sample(n = 5), returns a random row
        * n rows are returned
        * frac is the percentage of 
        * axis = 0/1
      
      
* `.nsmallest()` and `.nlargest()`
    * df.nlargest(3, columns = "Box Office")
    * df.nsmallest(3 , columns = "Box Office")


* Filtering with `.where()` method
    * df.where(mask), it returns the whole df but keeps NaN in all the rows where the row is not filtered
    

* Filtering with `.query()` Method
    * For this to work the columns names should not have spaces
    * but this looks very wierd I dont want to use it
  
 
* Apply Method with Row Values
    * create a function fxn(row) , this takes each row as a argument and gives a value
    * df.apply(fxn, axis = 'columns'), the columns here is a little bit confusing just read up Documentation



* Create a copy of DataFrame with `.copy()`
    * directors["A View to kill"] this is chuck of origianl dataframe and effects the original
    * df.copy()
    * df["Director"].copy()
    

## Lesson 5 : Working Text

* Common String Methods
    * `.lower()` 
    * `.upper()`
    * `.title()` -> first char of each word is captilized and all others are made lower
    * `len()`
    *  when called on a column the syntax is as follows
    * df["A"].str.lower()
    * str prefic must be given before using the method
    * df["A"].str.upper()
    * df["A"].str.title()


* `.str().replace()`
    * "Hello World".replace("l","!") -> replaces all the instances of l with !
    * df["D"].str.replace("MANGT", "Management")
    * df["A"].str.replace(",","")
    
    
* Filtering with String Method
    * df["A"].str.contains("Hello") -> returns true if it contains the substring
    * df["A"].str.startswith("Hello") -> only starts with Hello
    * df["A"].str.endswith("Hello") -> only ends with Hello


* `strip()` & `lstirip()` & `rstrip()`
    * removes whitespaces from beggining, last, or both accordingly
    * df["A"].str.lstritp()
    * df["B"].str.rstrip()
    
    
* String methods on Index and Columns
    * df.index.str.strip().str.title()


* `.split()`
    * "Hello my name is Boris".split(" ") -> ['Hello', 'my','name','is','Boris']
    * df["A"].str.split(",")
    * df["A"].str.split(",").str.get(0) -> gets 1st element from each list
    * **get** and **split** are complementaory
   
 
* `.split()`
    * **expand** parameter generates a dataframe rather than a series
    * **n** parameter determins maximum number of splits we can do

## Lesson 6 : Multi Index

* use set_index and pass it a index to get multi index
    * Use the column with least unique values to be the outer most level
    * The order in the array  effects the indexing
    * sort_indices sorts each layer
    * df.index returns array of tuples
    * so we need two ids to idexntify a value
    
* `get_level_index()` 
    * df.index.get_level_index(0) returns the index values at that level. 


* Change the names of the indexes
    * df.index.set_names(names , Level , inplace ) 
    * names is a list or a label
    * Level is the level which you want to change


* `sort_index()`
    * You can sort each level or only a single level using the appropriate parameters
    * But when the higher levels are individually sorted the grouping by lower levels will not remian intact
    
    
* Extract Rows from MultiIndex
        * important
        
    * Remeber `.loc` for normal dfs, the first argument is a row index and the second index is a column index
    * The same syntax is preferred here
    * So the first index must be a tuple( not list ) of required multiIndex and second index must be a label or a list of column names
    * There is not such problem with `iloc` accessor
    * Every row is given a unique index number wrt row
    
    
* Remember that there could be multiIndex in Columns as well as in Rows. So all of this appleis to column multi index as well. 


* Each of the entries in `loc` accessor must be a tuple when dealing with multi Indices


* `swaplevel`
    * df.swaplevel() swaps levels 
    
* `stack()` 
    * Takes the column values and makes them into index values
    

* `to_frame()` 
    * converts series into dataframe
    
    
* `unstack()`
    * Takes the index and makes it into a column
    * You can use a combination of stack and unstack to methods to get the shape you want
    * you can pass in arguments to say which layer should be unstacked outer most layer is 0th layer
    * inner most layer is -1
    * you can also pass in a list to move multiple layers at once
    * you can use **fill_na** parameter to fill in the NaN values
    
   
* `pivot()`
    * you can align/ condense along the common values
    * practice this for more efficieny
    * choose the index values , column values and values which needs to be at their intersection
    
    
* `pivot_table()` method
    * you can aggregate on a column based on a different column grouping
    * very impotant method
    
    
* `pd.melt()`
     * opposite of melt
     * all the indxes are melted into a single row
```
## Pivot Table Illustration
df  = pd.read_csv("pandas/salesmen.csv" , parse_dates=["Date"])
df["Salesman"] = df["Salesman"].astype("category")
df.head(3)

df.pivot(index = "Date" , columns= "Salesman" , values="Revenue" )

## Pivot Table Illustration
food = pd.read_csv("pandas/foods.csv")
food.head()

food.pivot_table(values = "Spend", index = ["Gender","Item"], columns="City")
```
## Lesson 7 : Groupby 

* Ideal thing to groupby is the column having less unique values


* df.groupby("Sector")
    * It creates a lot of smaller data frames that are created by using the column Sector 
   
   
* len(groupby_obj) -> number of groups. Each corresponding to a unique value of the coumn


* `sectors.size()` -> number of rows in each group
    * it is similar to value counts() method

* `sectors.first()` -> extracts first row of each group


* `sectors.last()` -> extracts last row of each group


* `sectors.groups` -> returns a dictionary, keys are unique value, values are list of index values corresponding to orginal dataframe


* Retrieve a group using `get_group()`
    * sectors.get_group("Energy") -> gives a dataframe that has Energy in sector column
    
    
* `sectors.max()` -> from each group it gives the max of each group on the last column


* `sectors.sum()` -> gives sum across each column of every group


* `sectors.mean()` -> gives mean across each column of every group


* `sectors["Revenue"].sum()` -> gives sum across only Revenue column ( rather than the whole group )


* Grouping by multiple columns
    * d.groupby(["A"], ["B"] )
    * it is grouped by first A and then by B
    
    
* `.agg()`
   * sectors.agg(dict)
   * dict has column names as key and aggregates as values
   * you can also apply multiple operations to different columns by using list


* Iterate through all the groups 
    * 
    ```
    for sector.data in sectors()
        df.append(data.nlargest(1, "Revenue"))
    ```