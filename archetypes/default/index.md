---
draft: true
title: '{{ replace .Name "-" " " | humanize | title }}'
author:
recipe_image:
images: []
date: '{{ .Date }}'
# The type of meal or course your recipe is about. For example: "dinner", "entree", or "dessert".
# The region associated with your recipe. For example, "French", Mediterranean", or "American".
tags: []
servings: 4
prep_time: 15 # in minutes
prep_increment: minutes # set to minutes or hours
cook: true # If we are cooking this, leave true, if we are cooling set to false
cook_increment: minutes # set to minutes or hours
cook_time: 8 # in minutes or hours
---

## Ingredients

#### Ingredient Subheading

- First Ingredient
- Second Ingredient [^1]
- Third Ingredient
- Fourth Ingredient
- Fifth Ingredient

## Directions

1. Step One
   1. Sub Step One
1. Step Two
1. Step Three
1. Step Four
1. Step Five
1. Step Six
