---
layout: page
title: "Create a recipe"
description: "How to create a recipe"
---
{% include JB/setup %}


### Creating a recipe

data parameter in json format:

    { 'title': 'Ham Sandwich' }
    
curl request:

    curl -X POST 'http://kmapi.local/v2/recipe' \
        -H "Authorization: Bearer 835fede3570d6eeee08ae94c5bd64d50"