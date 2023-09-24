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
+ use this to execute the query:
  
      c.execute(sql_query)
      conn.commit()
  
+ created a second query to add more information into the table
+ executed the query
+ **optional:** check if the queries have been populated into the table:

      query = """

        SELECT *
        from icecream;

        """

      c.execute(query)
      print(c.fetchall())
  
+ create an engine to connect to the database:
  
      engine = create_engine('sqlite:///health.db')
  
+ display the table:
  
      icecream = pd.read_sql(query, conn)
      icecream

### Automatic table creation process

Pulling data from a preexisting dataset

+ Modifying the column names in icecream to fit the column names of the selected dataset:
  
      columnNames = list(df_msmc)
      idVars = columnNames[:5]
      valueVars = columnNames[5:]

      icecream_modified = df_msmc.melt(id_vars=idVars, value_vars=valueVars)

      icecream_modified.columns 

      icecream_modified.rename(columns={'icecream_name': 'ChargeDescription',
                                  'icecream_type': 'LongDescription',
                                  'flavor':'BillingCode',
                                  'servings_per_box':'RevenueCodeDRGType',
                                  'cost_per_box': 'GrossCharge'}, inplace=True)

      icecream_modified

+ replacing the information in table with the modified table information:

      icecream_modified.to_sql('icecream', conn, if_exists='replace')

+ **Optional:** testing modified table by creating queries to pull information from it:

      modified_query = """
        select * 
        from icecream
        where RevenueCodeDRGType = '900'
        limit 200;
      """
      check = pd.read_sql(modified_query, conn)
      check

