This page is still under progress...

# Apache Spark learnings
### Some tips and other things I learned while working with Spark which could save your time.

I have been working with Spark 2.1 with Python and using Dataframes rather than RDDs. Dataframes are new, and difficult because you don't have readymade answers on tech forums. I will be adding my learnings to this documentation as and when I come across new things.

1. Pandas is not available in PySpark. This means, you can't just convert your Spark Dataframe to a Pandas dataframe to perform pandas operations.

2. Fetching data from a row object of a dataframe:
When using a select query to get data from a column of a dataframe, a list of "row" objects is returned. To be able to use the elements of that list, you need to iterate over it.
`subset_dataframe = 
