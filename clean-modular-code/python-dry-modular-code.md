---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.16.4
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

```{raw-cell}
---
editable: true
raw_mimetype: ''
slideshow:
  slide_type: ''
---
---
title: 'DRY Code and Modularity'
excerpt: "DRY (Do Not Repeat Yourself) code supports reproducibility by removing repetition and making code easier to read. Learn about key strategies to write DRY code in Python."
authors: ['Leah Wasser', 'Jenny Palomino']
---
```

+++ {"editable": true, "slideshow": {"slide_type": ""}}

(dry-code)=
# Write DRY, modular Python code

:::{admonition} What you will learn
:class: tip

* Define the DRY principle.
* List key strategies for writing DRY code in Python.
* Explain how these strategies help you write DRY code.
:::

## Don't Repeat Yourself (DRY)

The DRY approach to programming refers to writing functions and automating repeated sections of code. If you perform the same task multiple times in your code, consider a function or a loop to make your workflow more
efficient.


:::{figure} /images/clean-code/copy-pasta-code-dry.png
:alt: "Image showing four stacked elbow macaroni shapes labeled ‘Ctrl + V’ with each stack having a slight variation in the middle noodle. The variations include a smiling face, a frowning face, and a green and pink noodle."
:::


## Don't repeat yourself: remove repetition in your code

### Why write efficient code

DRY code relates to reproducible science because one component of reproducibility is writing code that is easy to read. If your code is easy to read, it will be easier for your future self to understand that code. It will also be easier for your colleagues to work with and contribute to your code. This is important, but there is an even more selfish reason to consider writing efficient code.

Efficient coding will make your life easier, too.

:::{figure-md} package-decision-tree

<img src="/images/clean-code/clean-code-being-lazy-hadley-wickham.png" alt="An image that shows a visual representation of a tweet with Hadley Wickham's profile picture on it. It says: Reproducibility is actually all about being as lazy as possible." width="700px">

Reproducibility can mean being as lazy as possible. When you can avoid repeating steps and code, you should do just that. Source: [Twitter/X](https://twitter.com/hadleywickham/status/598532170160873472).
:::

### Don’t Repeat Yourself: DRY

DRY (Don’t Repeat Yourself) is a principle of software development. The focus of DRY is to avoid the repetition of information.

Why?

One main reason is that when you write code that performs the same tasks repeatedly, any modification of one task requires the same change to be made to every place that you use that task! Editing every instance of a task is a lot of work.

By implementing DRY code approaches, you can make your code:

1. easier to follow and read (for yourself as well as others), thereby supporting reproducibility
2. easier to update because you only have to update your code once, rather than everywhere that code block is used

## Strategies for writing DRY code

Below you will learn about three commonly used strategies associated with writing clean code:

1. Write a function when a task is repeated over and over.
2. Create loops that iterate over repetitive tasks.
3. Use conditional statements to control the flow of if and when code is executed.

The above three approaches are often used together when writing
code.

### Write functions to document and simplify repeated tasks

A [function](write-functions) is a reusable block of code that performs a specific task. Functions have inputs and outputs. Functions can help you to both eliminate repetition and improve efficiency in your code through modularity. If you have been using Python for any period of time, you have already used built-in Python functions.

For example, `print()` is a function used to write output to the Python console (or a Jupyter Notebook). If you have used Pandas, `pd.read_csv()` is a function that reads a text file into Python in a dataframe format. The `print()` and `read_csv()` functions are useful to you as a Python programmer because you do not need to know the specific lines of code that are required to `print()`. All that you need to know is how to call the print command: `print("My text here")`.

Below, you have a custom function with a custom name.

```python
def convert_to_kelvin(temperature_fahr):
    """Convert temperature in Fahrenheit to kelvin.

    Parameters:
    -----------
    temperature_fahr: int or float
        The temperature in Fahrenheit.
    
    Returns:
    -----------
    The temperature in kelvin.
    """
    return ((temperature_fahr - 32) * (5 / 9)) + 273.15
```

This function converts temperature in Fahrenheit to kelvin. You can
learn more about it by reading its documentation (docstring).

Now, imagine that you need to perform this calculation over and over.

```python
temp = 55
new_temp = ((temp - 32) * (5 / 9)) + 273.15

temp2 = 46 
new_temp_k = ((temp2 - 32) * (5 / 9)) + 273.15
```

In the example above, you are repeating the same calculation twice.

In this example:

1. if the calculation needs to change, you need to change it twice
2. it's not necessarily clear what the calculation is doing unless you know the calculation itself.

The example below is cleaner because now you are replacing a repeated calculation with a function. If this function is well-defined with a docstring that describes what it does, it is easier
to both understand and use. If you need to change the calculation itself, you can do so once in the function. Then, you rerun your code.

```python
temp = 55
new_temp = convert_to_kelvin(temp)

temp2 = 46 
new_temp_k = convert_to_kelvin(temp2)
```

The task above could be further simplified using loops which will be discussed below. Writing modular code allows you to subdivide tasks of a workflows into organized units of code that can be reused by yourself and others, often without them needing to know the specific details of the code.

### Write loops in Python To simplify iterative repetitive tasks

A loop executes a sequence of operations repeatedly in a specified order.

Loops can help you eliminate repetition in code by replacing
duplicate lines of code with an iteration. This means that you can
iteratively execute the same code line or block until it reaches a specified endpoint.

For example, consider the following lines of code:

```python
print(avg_monthly_precip)
print(months)
print(precip_2002_2013)
```

This code could be replaced by a loop that iterates over a list of variable names and executes the `print()` function until it reaches the end of the list:

```python
variables = [avg_monthly_precip, months, precip_2002_2013]
for variable in variables:
    print(variable)
```

You can create lists of variables, filenames, or other objects like data structures upon which you want to execute the same code. These lists can then be used as variables in loops.

### Conditional Statements

A conditional statement is used to determine whether a certain condition exists before code is executed. Conditional Statements can improve the efficiency of your code by providing you with the ability to control the flow of your code, such as when or how code is executed.  

For example, conditional statements can be used to check that a certain variable or file exists before code is executed, or to continue code if some criteria is met such as a calculation resulting in a specific value.

In the example below, you can combine a loop and a conditional statement to only print the variable value if the value is greater than 20.  

```python
avg_monthly_precip=100
months=20
precip_2002_2013=30

variables = [avg_monthly_precip, months, precip_2002_2013]

# This list comprehension loops over each variable and prints the value if it is greater than 20
[print(variable) for variable in variables if variable> 20]
```

+++ {"editable": true, "slideshow": {"slide_type": ""}}

## Practice Applying PEP 8 To Your Code

Take a look at the code below.

* Create a list of all of the things that could be improved to make the code easier to read / work with.
* Identify changes to specific items that would help the code adhere to the PEP 8 style guide.

<!--

Format Issues:
* missing spaces in between comments
* comments aren't useful to help me understand what is happening
* white space

Object Naming Issues
* didn't use useful object names that describe the object
* one very long object name
* used a mixture of underscore and case that will be easy to confused 

-->

+++ {"editable": true, "slideshow": {"slide_type": ""}}

## Additional Resources

* <a href="https://www.python.org/dev/peps/pep-0008/" target="_blank">The PEP 8 Style Guide</a>.

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
---
# Create variable
variable=3*6
meanvariable = variable

#calculate something important
mean_variable = meanvariable * 5

# last step of the workflow
finalthingthatineedtocalculate = mean_variable + 5
```
