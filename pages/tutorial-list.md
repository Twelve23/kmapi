---
layout: page
title: "Grocery List Tutorials"
description: "How to create a list"
group: 'tutorial'
---
{% include JB/setup %}


* [creating a grocery list](#create-list)
* [adding a shopping item](#create-item)
* [batch adding items](#batch-create-item)
* [removing lists](#delete-list)
* [removing an item](#delete-item)
* [get a list](#get-list)
* [get all lists](#get-all-lists)
* [sample list response](#sample-list)

-----------------

### <a id="create-list">&nbsp;</a>Creating a list



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/list' \
		-H "Authorization: Bearer [USER_TOKEN]"

successful response:

	{
		"success":"create_list",
		"id":[list_id],
		"data":{
			"id":[list_id],
			"user_id":[user_id],
			"name":null,
			"location_id":0,
			"location":null,
			"created":1367017548,
			"modified":1367017548,
			"items":[],
			"stores":[]
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#16" target="blank">full reference</a>

-----------------


### <a id="create-item">&nbsp;</a>Adding an item to the list



request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/list/[list_id]/item' \
		-d ingredient_id=45 \
		-d ingredient_custom=0 \
		-d quantity=5 \
		-d unit_text=lbs \
		-d recipe_id=50763 \
		-d store_id=12 \
		-d brand_item_id=5 \
		-d brand=Darigold \
		-d note=big+size \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"list_item_add",
		"success_message":"Item(s) were added to grocery list",
		"id":[list_item_id]
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#19" target="blank">full reference</a>

-----------------


### <a id="batch-create-item">&nbsp;</a>Batch adding an item to the list



data parameter in json format:

	[
		{
			"list_id":"[list_id]"
			"ingredient_id":"[ingredient_id]",
			"ingredient_custom":"0",
			"quantity":"5",
			"unit_text":"lbs",
			"recipe_id":"[recipe_id]",
			"store_id":"[store_id]",
			"brand_item_id":"[brand_item_id]",
			"brand":"Darigold",
			"note":"big size"
		},
		...
	]

request:

	curl -X POST 'http://devapi.kitchenmonki.com/v2/list/[list_id]/item' \
		-d data=[form encoded json data parameter] \
		-H "Authorization: Bearer [USER_TOKEN]" \
		-H "Content-Type: application/x-www-form-urlencoded"

successful response:

	{
		"success":"list_item_add",
		"success_message":"Item(s) were added to grocery list",
		"id":[list_item_id]
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#19" target="blank">full reference</a>

-----------------


### <a id="delete-list">&nbsp;</a>Deleting a list



request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/list/[list_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_list",
		"id":"[list_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#18" target="blank">full reference</a>

-----------------

### <a id="delete-item">&nbsp;</a>Deleting list items



request:

	curl -X DELETE 'http://devapi.kitchenmonki.com/v2/list/[list_id]/item' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"delete_list_item",
		"id":"[list_id]"
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#21" target="blank">full reference</a>

-----------------


### <a id="get-list">&nbsp;</a>Get a list



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/list/[list_id]' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"success":"get_grocery_list",
		"user_id":[user_id],
		"data":{
			"id":[list_id],
			"name":null,
			"location_id":0,
			"location":null,
			"created":1363740879,
			"modified":1363740879,
			"items":[
				{
				...
				}
			]
		}
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#15" target="blank">full reference</a>

-----------------


### <a id="get-all-lists">&nbsp;</a>Get all lists



request:

	curl -X GET 'http://devapi.kitchenmonki.com/v2/list/all' \
		-H "Authorization: Bearer [USER_TOKEN]" \

successful response:

	{
		"user_id":[user_id],
		"data":[
			{
				"id":[list_id],
				"user_id":[user_id],
				"name":null,
				"created":1366830792,
				"modified":1366830792
			},
			...
		]
	}

<a href="http://km.local/api_docs/console?access_token=835fede3570d6eeee08ae94c5bd64d50#35" target="blank">full reference</a>

-----------------


### <a id="sample-list">&nbsp;</a>Sample list response in json format



	{
		"success":"get_grocery_list",
		"user_id":[user_id],
		"data":{
			"id":[list_id],
			"name":null,
			"location_id":[location_id],
			"location":null,
			"created":1363740879,
			"modified":1363740879,
			"items":[
				{
					"id":[list_item_id],
					"ingredient":{
						"id":[ingredient_id],
						"name":"Frozen Chicken Wing",
						"name_plural":"Chicken Wings",
						"name_nomenclature":"Chicken, Frozen Wing",
						"measure_type_id":[unit_id],
						"custom":false,
						"category_id":[category_id]
					},
					"ingredient_formatted":"12 oz brand4 Frozen Chicken Wing,",
					"recipe_id":[],
					"store_id":[store_id],
					"brand_item_id":[brand_item_id],
					"brand_item":{
						"id":[brand_item_id],
						"brand_family_id":[brand_family_id],
						"user_id":1,
						"brand_text":"",
						"brand_family":{
							"id":[brand_family_id],
							"name":"brand4"
						}
					},
					"brand":"",
					"note":null,
					"quantity":12,
					"unit_text":"oz",
					"aisle":{
						"id":"[aisle_id]",
						"name":"Frozen Foods"
					}
				},
				...
			],
			"stores":[
				[...]
			]
		}
	}
