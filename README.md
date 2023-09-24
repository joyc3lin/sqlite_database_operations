# sqlite_database_operations
HHA 504 week 3 assignment 

## Datasets: 

Two hospital price transparency machine readible files were used. One from New York Presbytarian provided by the professor and the second from Mount Sinai Medical Center. 

## Exploratory Data Analysis Process

+ Cleaned datasets to ensure that no errors would occur during data analysis
  + looked at type of data in columns
  + determined if any datasets were missing data
  + deleted rows with missing data
  + removed duplicate rows and columns
  + cleaned column names to remove white spaces and special characters
+ Checked distribution of datasets by their respective revenue code
+ Looked at mean, median, mode, range, variance, standard deviation, and IQR of multiple columns from both datasets.
+ added conclusions drawn at the end

## SQLite database setup process

+ First created a local database named health.db:

       conn = sqlite3.connect('health.db')
       c = conn.cursor()

+ created a table named icecream with 5 columns within health.db:
  + each column has its data type listed next to it
  
        c.execute("""
            CREATE TABLE icecream
                 (
                 icecream_name text,
                icecream_type text,
                flavor text,
                servings_per_box real, 
                cost_per_box real
              );
        """)
       conn.commit()     

+ created a query to insert information into the table:
  
      sql_query = """

      INSERT INTO icecream (
       'icecream_name',
       'icecream_type',
       'flavor',
       'servings_per_box',
       'cost_per_box'
       )
       values (
         'Dazs-genhaa',
         'bars',
         'vanilla',
         8,
         10
       );     


"""


