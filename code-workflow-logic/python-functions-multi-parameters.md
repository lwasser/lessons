---
layout: single
title: 'Write Functions with Multiple Parameters in Python'
excerpt: "A function is a reusable block of code that performs a specific task. Learn how to write functions that can take multiple as well as optional parameters in Python to eliminate repetition and improve efficiency in your code."
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.4
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

<!-- #region -->
(multi-parameter-functions)=
# Write Multi-Parameter Functions 

:::{admonition} What you will learn
:class: tip

* Write and execute custom functions with multiple input parameters in **Python**.
* Write and execute custom functions with optional input parameters in **Python**.
:::


## How to Define a Function with Multiple Parameters in Python

In the [write functions lesson](write-python-functions), you learned about writing **Python** functions. You also learned that a parameter, such as `var_a`, is used to represent the value or object that the function will process.
<!-- #endregion -->

```python
def process_value(value):
    """A function that returns an integer value multiplied by 2"""
    return int(value) * 2

process_value(2.254)
```

However, sometimes, you need additional parameters for the function to run successfully. Like this:

```python
def function_name(data_1, data_2):
    # Function code here
    return some_output
```

<!-- #region -->
When the function is called, a user can provide any value for `data_1` or `data_2` as input for that parameter (e.g., single-value variable, list, {class}`numpy.ndarray`, {class}`pandas.DataFrame` column). 


## Write a Function with Multiple Parameters in Python

Imagine that you want to define a function that will take in two numeric values as inputs, multiply them, and return the product of these input values.  

Begin with the `def` keyword and the function name, just as you have before to define a function:


```python
def multiply_values():
```

Next, provide two placeholder variable names for the input parameters, as shown below. 


```python
def multiply_values(x, y):
```

Add the code to multiply the values and the `return` statement to returns the product of the two values: 

```python
def multiply_values(x, y):
    z = x * y
    return z
```

Last, write a docstring to provide the details about this function, including a brief description of the function (i.e. how it works, purpose) as well as identify the input parameters (i.e. type, description) and the returned output (i.e. type, description).
<!-- #endregion -->
```python
def multiply_values(x, y):
    """Calculate product of two inputs. 
    
    Parameters
    ----------
    x : int or float
    y : int or float

    Returns
    ------
    int or float
    """
    return x * y
```

## Call Custom Functions with Multiple Parameters in Python

Now that you have defined the function `multiple_values()`, you can call it by providing values for the two input parameters.  

```python
# Call function with numeric values
multiply_values(0.7, 25.4)
```

Recall that you can also provide pre-defined variables as inputs, for example, a value for precipitation and another value for a unit conversion value.  

```python
# Average monthly precip (inches) for Jan in Boulder, CO
precip_jan_in = 0.7

# Conversion factor from inches to millimeters
to_mm = 25.4
```

```python
# Call function with pre-defined variables
precip_jan_mm = multiply_values(precip_jan_in, to_mm)

precip_jan_mm
```

While the function is not defined specifically for unit conversions, it completes a generalizable task and can be used for simple unit conversions. 

<!-- #region -->
## Combine Unit Conversion and Calculation of Statistics into One Function

Now imagine that you want to both convert the units of a **numpy** array from millimeters to inches and calculate the mean value along a specified axis for either columns or rows.

Recall the function definition that you previously wrote to convert values from millimeters to inches:

```python
def mm_to_in(mm):
    """Convert input from millimeters to inches. 
    
    Parameters
    ----------
    mm : int or float
        Numeric value with units in millimeters.

    Returns
    ------
   int or float
        Numeric value with units in inches.
    """
    return mm / 25.4
```

You can expand this function to include running a mean along a specified axis for columns or rows, and then use this function over and over on many **numpy** arrays as needed.  

This new function can have descriptive names for the function and the input parameters that describe more clearly what the function accomplishes. 

Begin by defining the function with a descriptive name and the two necessary parameters: 
* the input array with values in millimeters
* the axis value for the mean calculation 

Use placeholder variable names that highlight the purpose of each parameter:


```python
def mean_mm_to_in(data_mm, axis_value):
```

Next, add the code to first calculate the mean of the input array along a specified axis, and then to convert the mean values from millimeters to inches. 

First, add the code line to calculate a mean along a specified axis. 


```python
def mean_mm_to_in(data_mm, axis_value):
    mean_data_mm = np.mean(data_mm, axis=axis_value)    
```


Next, add the code line to convert the mean array from millimeters to inches. In this case, the `return` statement should return the mean array in inches.


```python
def mean_mm_to_in(data_mm, axis_value):
    mean_data_mm = np.mean(data_mm, axis=axis_value)
    mean_data_in = mean_data_mm / 25.4 
        
    return mean_data_in
    
```

Note that the function could be written to convert the values first and then calculate the mean. However, given that the function will complete both tasks and return the mean values in the desired units, it is more efficient to calculate the mean values first and then convert just those values, rather than converting all of the values in the input array. 

````{tip}
Typically functions should have a [single purpose](https://en.wikipedia.org/wiki/Separation_of_concerns), and be [composed](https://en.wikipedia.org/wiki/Function_composition_(computer_science)) to implement higher-order operations. The above function would normally be written without wrapping {func}`numpy.mean` like this:

```python
mm_to_in(np.mean(data, axis=axis_value))
```

The purpose of this lesson is to introduce function parameters, so let's focus on that for now and save design principles for another lesson :).
````


Last, include a docstring to provide the details about this function, including a brief description of the function (i.e. how it works, purpose) as well as identify the input parameters (i.e. type, description) and the returned output (i.e. type, description).
<!-- #endregion -->

```python
def mean_mm_to_in(data_mm, axis_value):
    """Calculate mean values of input array along a specified
    axis and convert values from millimeters to inches.
    
    Parameters
    ----------
    data_mm : numpy array
        Numeric values in millimeters.
    axis_value : int
        0 to calculate mean for each column.
        1 to calculate mean for each row.

    Returns
    ------
    numpy array
        Mean values of input array in inches.
    """    
    mean_data_mm = np.mean(data_mm, axis=axis_value)
    return mean_data_mm / 25.4
```

Now that you have defined `mean_mm_to_in()`, you can call the function with the appropriate input parameters.

Create some data and test your new function with different input values for the `axis_value` parameter.

```python
# Import necessary package to run function
import numpy as np
```

```python
# 2d array of average monthly precip (mm) for 2002 and 2013 in Boulder, CO
precip_2002_2013_mm = np.array([[27.178, 11.176, 38.1, 5.08, 81.28, 29.972, 
                                 2.286, 36.576, 38.608, 61.976, 19.812, 0.508],
                                [6.858, 28.702, 43.688, 105.156, 67.564, 15.494,  
                                 26.162, 35.56 , 461.264, 56.896, 7.366, 12.7]
                               ])
```

```python
# Calculate monthly mean (inches) for precip_2002_2013
monthly_mean_in = mean_mm_to_in(data_mm=precip_2002_2013_mm, 
                                    axis_value=0)

monthly_mean_in
```

```python
# Calculate yearly mean (inches) for precip_2002_2013
yearly_mean_in = mean_mm_to_in(data_mm=precip_2002_2013_mm, 
                                   axis_value=1)

yearly_mean_in
```

## Define Optional Input Parameters for a Function 

Your previously defined function works well if you want to use a specified axis for the mean.

However, notice what happens when you try to call the function without providing an axis value, such as for a one-dimensional array.

```python
# 1d array of average monthly precip (mm) for 2002 in Boulder, CO
precip_2002_mm = np.array([27.178, 11.176, 38.1,  5.08, 81.28, 29.972,  
                           2.286, 36.576, 38.608, 61.976, 19.812, 0.508])
```

<!-- #region -->
```python
# Calculate mean (inches) for precip_2002
monthly_mean_in = mean_mm_to_in(data_mm=precip_2002_mm)
```

You get an error that the `axis_value` is missing:

```python
TypeError: mean_mm_to_in() missing 1 required positional argument: 'axis_value'
```
<!-- #endregion -->

<!-- #region -->
What if you want to make the function more generalizable, so that the axis value is optional?

You can do that by specifying a default value for `axis_value` as `None` as shown below:

```python
def mean_mm_to_in(data_mm, axis_value=None):
```

The function will assume that the axis value is `None` (i.e. that an input value has not been provided by the user), unless specified otherwise in the function call.

However, as written, the original function code uses the axis value to calculate the mean, so you need to make a few more changes, so that the mean code runs with an axis value if a value is provided or runs without an axis value if one is not provided.

Luckily, you have already learned about conditional statements, which you can now add to your function to run the mean code with or without an axis value as needed. 

Using a conditional statement, you can check if `axis_value` is equal to `None`, in which case the mean code will run without an axis value. 

```python
def mean_mm_to_in(data_mm, axis_value=None):
    
    if axis_value is None:
        mean_data_mm = np.mean(data_mm) 
```

The `else` statement would mean that `axis_value` is not equal to `None` (i.e. a user has provided an input value) and thus would run the mean code with the specified axis value.

```python
def mean_mm_to_in(data_mm, axis_value=None):
    
    if axis_value is None:
        mean_data_mm = np.mean(data_mm)        
    else:
        mean_data_mm = np.mean(data_mm, axis=axis_value)
```

The code for the unit conversion and the `return` remain the same, just with updated names:

```python
def mean_mm_to_in(data_mm, axis_value=None):
    if axis_value is None:
        mean_data_mm = np.mean(data_mm)        
    else:
        mean_data_mm = np.mean(data_mm, axis=axis_value)
        
    return mean_data_mm / 25.4
```

Last, include a docstring to provide the details about this revised function. Notice that the axis value has been labeled optional in the docstring. 
<!-- #endregion -->

```python
def mean_mm_to_in(data_mm, axis_value=None):
    """Calculate mean values of input array and convert values 
    from millimeters to inches. If an axis is specified,
    the mean will be calculated along that axis. 

    
    Parameters
    ----------
    data_mm : numpy array
        Numeric values in millimeters.
    axis_value : int (optional)
        0 to calculate mean for each column.
        1 to calculate mean for each row.

    Returns
    ------
    numpy array
        Mean values of input array in inches.
    """   
    if axis_value is None:
        mean_data_mm = np.mean(data_mm)        
    else:
        mean_data_mm = np.mean(data_mm, axis=axis_value)
    
    return mean_data_mm / 25.4 
```

Notice that the function will return the same output as before for the two-dimensional array `precip_2002_2013_mm`.

```python
# Calculate monthly mean (inches) for precip_2002_2013
monthly_mean_in = mean_mm_to_in(data_mm=precip_2002_2013_mm, 
                                    axis_value=0)

monthly_mean_in
```

However, now you can also provide a one-dimensional array as an input without a specified axis and receive the appropriate output.

```python
# Calculate mean (inches) for precip_2002
monthly_mean_in = mean_mm_to_in(data_mm=precip_2002_mm)

monthly_mean_in
```

<!-- #region -->
## Combine Download and Read Input of Data Files into One Function

You can also write multi-parameter functions to combine other tasks into one function, such as downloading and reading data files into a **pandas** dataframe.

Think about the code that you need to include in the function:
1. download data file from URL: {func}`et.data.get_data(url=file_url) <earthpy.data.get_data>`
2. read data file into **pandas** dataframe: {func}`pd.read_csv(path) <pandas.read_csv>`

From this code, you can see that you will need two input parameters for the combined function:
1. the URL to the data file
2. the path to the downloaded file

Begin by specifying a function name and the placeholder variable names for the necessary input parameters. 

```python
def download_input_df(file_url, path):  
```

Next, add the code for download and the import. 

```python
def download_input_df(file_url, path):  
    et.data.get_data(url=file_url)  
    df = pd.read_csv(path)
```

However, what if the working directory has not been set before this function is called, and you do not want to use absolute paths? 

Since you know that the `get_data()` function creates the `earth-analytics` directory under the home directory if it does not already exist, you can safely assume that this combined function will also create that directory.

As such, you can include setting the working directory in the function, so that you do not have to worry about providing absolute paths to the function:

```python
def download_input_df(file_url, path):    
    
    et.data.get_data(url=file_url)      
    os.chdir(os.path.join(et.io.HOME, "earth-analytics"))    
    df = pd.read_csv(path)
    
    return df
```

Last, include a docstring to provide the details about this function, including a brief description of the function (i.e. how it works, purpose) as well as identify the input parameters (i.e. type, description) and the returned output (i.e. type, description).
<!-- #endregion -->

```python
def download_imnput_df(file_url, path):   
    """Download file from specified URL and import file
    into a pandas dataframe from a specified path. 
    
    Working directory is set to earth-analytics directory 
    under home, which is automatically created by the
    download. 

    
    Parameters
    ----------
    file_url : str
        URL to CSV file (http or https).
    path : str
        Path to CSV file using relative path
        to earth-analytics directory under home.        

    Returns
    ------
    df : pandas dataframe
        Dataframe imported from downloaded CSV file.
    """ 
    
    et.data.get_data(url=file_url)      
    os.chdir(os.path.join(et.io.HOME, "earth-analytics"))    
    df = pd.read_csv(path)
    
    return df
```

Now that you have defined the function, you can import the packages needed to run the function and define the variables that you will use as input parameters.

```python
# Import necessary packages to run function
import os
import pandas as pd
import earthpy as et
```

```python
# URL for average monthly precip (inches) for 2002 and 2013 in Boulder, CO
precip_2002_2013_df_url = "https://ndownloader.figshare.com/files/12710621"

# Path to downloaded .csv file with headers
precip_2002_2013_df_path = os.path.join("data", "earthpy-downloads", 
                                        "precip-2002-2013-months-seasons.csv")
```

Using these variables, you can now call the function to download and import the file into a **pandas** dataframe. 

```python
# Create dataframe using download/import function
precip_2002_2013_df = download_input_df(
    file_url = precip_2002_2013_df_url, 
    path = precip_2002_2013_df_path)

precip_2002_2013_df
```

<!-- #region -->
###  Making Functions More Efficient Does Not Always Mean More Parameters

Note that you previously defined `download_input_df()` to take in two parameters, one for the URL and for the path, and the function works well to accomplish the task.

However, with a little investigation into the `et.data.get_data()` function, you can see that the output of that function is actually a path to the downloaded file!

```python
help(et.data.get_data)
```
In the docstring details provided, you can see that the full path to the downloaded data is returned by the function:

```
Returns
-------
path_data : str
    The path to the downloaded data.
```

This means that you can redefine `download_input_df()` to be more efficient by simply using the output of the `et.data.get_data()` function as the input to the `pd.read_csv()` function. 

Now, you actually only need one parameter for the URL and you do not have to define the working directory in the function, in order to find the appropriate file.
<!-- #endregion -->

```python
def download_input_df(file_url):   
    """Download file from specified URL and input file
    into a pandas dataframe. 
    
    The path to the downloaded file is automatically 
    generated by the download and is passed to the 
    pandas function to create a new dataframe. 
    
    Parameters
    ----------
    file_url : str
        URL to CSV file (http or https).       

    Returns
    ------
    df : pandas dataframe
        Dataframe imported from downloaded CSV file.
    """ 

    df = pd.read_csv(et.data.get_data(url=file_url))
    
    return df
```

Your revised function now executes only one line, rather than three lines! Note that the docstring was also updated to reflect that there is only one input parameter for this function. 

Now you can call the function with just a single parameter for the URL. 

```python
# Create dataframe using download/import function
precip_2002_2013_df = download_input_df(file_url = precip_2002_2013_df_url)

precip_2002_2013_df
```

<!-- #region -->

## Practice Writing Multi-Parameter Functions for Pandas Dataframes

You have a function that combines the mean calculation along a specified axis and the conversion from millimeters to inches for a **numpy** array. 

How might you need to change this function to create a similar function for **pandas** dataframe, but now converting from inches to millimeters?

For the mean, you can run summary statistics on pandas using a specified axis (just like a **numpy** array) with the following code:

```python
df.mean(axis=axis_value) 
```

With the axis value `0`, the code will calculate a mean for each numeric column in the dataframe.

With the axis value `1`, the code will calculate a mean for each row with numeric values in the dataframe.

Think about which code lines in the existing function `mean_mm_to_in()` can be modified to run the equivalent code on a **pandas** dataframe.

Note that the `df.mean(axis=axis_value)` returns the mean values of a dataframe (along the specified axis) as a **pandas** series.


<!-- #endregion -->


## Practice Writing Multi-Parameter Functions for Numpy Arrays

You also have a function that combines the data download and import for a **pandas** dataframe, you can modify the function for other data structures such as a **numpy** array. 

How might you need to change this function to create an equivalent for **numpy** arrays?

Think about which code lines in the existing function `download_input_df()` can be modified to write a new function that downloads and imports data into a **numpy** array.

To begin, you may want to write one function for a 1-dimensional array and another function for a 2-dimensional array.

To advance in your practice, you can think about adding a conditional statement that would check for the file type (.txt for a 1-dimensional array .csv for a 2-dimensional array) before executing the appropriate import code. 

