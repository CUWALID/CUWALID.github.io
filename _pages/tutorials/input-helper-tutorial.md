---
title: "Input Helper Tutorial"
layout: single
permalink: /tutorials/input-helper/

sidebar:
  nav: "tutorials"
---

<a href="/tools/#input-helper" class="btn btn--primary">Input Helper</a>

The input helper is a webpage that can help you create the JSON files necessary to run the models within the CUWALID System. This is useful for people who have not worked with code or JSON files before. The website is intuitive and easy to use with descriptions on each of the variables and options.

## Tutorial

The first thing you need to do is select which input you would like to create, through the dropdown menu highlighted in the blue box as shown in the figure below:

{% include figure popup=true image_path="/assets/images/input_helper/input_type.png" alt="Image of selecting the input type" %}

Optionally, if you already have a JSON, you can upload this and the options will be filled out for you based on your file. This is useful if you just need to make a few changes but don't want to go through every option again. The figure below shows how you can do this:

{% include figure popup=true image_path="/assets/images/input_helper/template.png" alt="Image of uploading a template file" %}

From here, choosing the inputs is as easy as reading the title and description, changing the input (i.e. checkbox or text input). Defaults are provided for your convenience. When a title is shown in the colour 'red', this shows it is a required variable for the model to run.

Once you have selected all your input types, there is a final option to create the name for your output file as shown in the figure below:

{% include figure popup=true image_path="/assets/images/input_helper/output_name.png" alt="Image of output file name input" %}

The large blue 'Export JSON' Button will create the file and download it on your PC for you to use.

Below this an example of your input written in JSON format is provided so you can check it all looks correct without having to download it.