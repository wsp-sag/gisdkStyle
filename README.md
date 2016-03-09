gisdkStyle
==========

Style guide and syntax files for GISDK development.

## Syntax Files

TransCAD's GISDK scripting language is a powerful proprietary language used almost exclusively for travel demand modeling. Because the user community is fairly small, coding standards and conventions are not as well-developed as C, Java, R, or Python. We hope to change this.

In the `syntax/` folder you will find syntax files that we have created and/or collected to write GISDK script in a variety of text editors. Currently we host working files for:

  - *vim*: place in your `~/vimfiles/syntax/` folder, and add the following to your `.vimrc`:
  ```sh
    autocm BufRead,BufNewFile *.rsc set filetype=gisdk
  ```
  - *Notepad++*
  - *UltraEdit*

Others will be added as we receive them.

## Style Guide

Properly written code is easier to read, follow, debug, and improve. Taking a small amount of time to write clean code will save you and others a significant amount of time in the future.

These are styles and conventions that we have begun to implement in our work at PB. They are subject to change and/or evolution as more developers join the projects. We invite others involved with TransCAD development to participate.



### Script Layout

A single GISDK script should accomplish only one primary purpose, though it may contain more than one `Macro` definition if they are related to the model step. It is preferable to write multiple scripts than to create an overly long process.

### Line structure

Lines should be limited to 80 characters and only execute one statement or function. Lines longer than this are difficult to view in terminals, the GISDK debugger, or side-by-side. Function inputs should ideally occupy their own line, indented within the function brackets. An acceptable (but not ideal) alternative is to break the line to the opening bracket.

**Best**

    return(
      RunMacro("CreateAllStreetSkims",
        street_layer_file,
        outputs_dir,
        iteration_number,
        scenario_dir
      )
    )

**OK**

    return(RunMacro("CreateAllStreetSkims", street_layer_file, outputs_dir,
                    iteration_number, scenario_dir))

**Bad**

    return(RunMacro("CreateAllStreetSkims", street_layer_file, outputs_dir,
      iteration_number, scenario_dir))

**Worst**

    return(RunMacro("CreateAllStreetSkims", street_layer_file, outputs_dir, iteration_number, scenario_dir))

Indents should be two spaces, and never tabs.


### Operators
Operators, such as `+`, `=`, etc. should always have a space on both sides. Commas should have a whitespace after, but never before.

**Good**

    x = y + 1

**Bad**

    x=y+1

### Naming


### Commenting

Comments should adequately describe the code using meaningful language.
Borrowing from [Google's Python documentation style](https://google-styleguide.googlecode.com/svn/trunk/pyguide.html#Comments):

>Complicated operations get a few lines of comments before the operations commence. Non-obvious ones get comments at the end of the line.

```
    /* We use a weighted dictionary search to find out where i is in
     the array.  We extrapolate position based on the largest num
     in the array and the array size and then do binary search to
     get the exact number. */

    if i & (i-1) == 0:        // true iff i is a power of 2
```
Unlike their recommendation, do not assume that the reader of your code will understand GISDK better than you.  Many clients are new to GISDK, or even script in general.  As a result, it is OK to explain the code if numerous loops or complicated arrays are constructed.

### Looping

Unlike Python or R, GISDK does not support the following looping syntax:

    for i in array

In order to keep looping simple and easy to modify, do not use subscripts throughout the loop.  Instead, define variables using subscripts at the beginning of the loop only.  This makes the code easier to understand and modify for the next user.

**Good**
```
TimeOfDay = {"AM", "MD", "PM"}
for t = 1 to TimeOfDay.length do
  tod = TimeOfDay[t]

  FileName = tod + "_trips.bin"
end
```
**Bad**
```
TimeOfDay = {"AM", "MD", "PM"}
for t = 1 to TimeOfDay.length do
  FileName = TimeOfDay[t] + "_trips.bin"
end
```
