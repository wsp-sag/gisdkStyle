gisdkStyle
==========

Style guide and syntax files for GISDK development.

## Syntax Files

TransCAD's GISDK scripting language is a powerful proprietary language used almost exclusively for travel demand modeling. Because the user community is fairly small, coding standards and conventions are not as well-developed as C, Java, R, or Python. We hope to change this. 

In the `syntax/` folder you will find syntax files that we have created and/or collected to write GISDK script in a variety of text editors. Currently we host working files for:
  
  - *vim*: place in your `~/vimfiles/syntax/` folder, and add the following to your `.vimrc`:
    autocm BufRead,BufNewFile *.rsc set filetype=gisdk

  - *Notepad++*
  - *UltraEdit*

Others will be added as we receive them.

## Style Guide 

These are styles and conventions that we have begun to implement in our work at PB. They are subject to change and/or evolution as more developers join the projects. We invite others involved with TransCAD development to participate.

### Script Layout

A single GISDK script should accomplish only one primary purpose, though it may contain more than one `Macro` definition if they are related to the model step. It is preferable to write multiple scripts than to create an overly long process.

### Code Structure

Lines should be limited to 80 characters. Broken lines should wrap to the beginning of the current bracket or parenthesis.

**Good**
    return(RunMacro("CreateAllStreetSkims", street_layer_file, outputs_dir,
                    iteration_number, scenario_dir))
**Bad**
    return(RunMacro("CreateAllStreetSkims", street_layer_file, outputs_dir,
      iteration_number, scenario_dir))
**worse**
    return(RunMacro("CreateAllStreetSkims", street_layer_file, outputs_dir, iteration_number, scenario_dir))


### Naming


