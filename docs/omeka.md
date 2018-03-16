## initial api get

http://[your-omeka-url]/api/items?item_set_id=[your-item-set-id]

Create an open refine project from link created

1. Click Create Project
2. Select Web Addresses (URLS)
3. Enter api web link
- http://[your-omeka-url]/api/items?item_set_id=[your-item-set-id]
4. At bottom left of page, "Parse data as" - "JSON files"
5. Click near highest curly bracket '{' towards top of page
6. Create project at by clicking button at top of page


http://omeka.cdil.us/api/items?item_set_id=109

## Refine copy paste actions

The full step by step open refine options can be found at [refine-omeka.txt](refine-omeka.txt])

These steps do two main things: 

1. They fetch URLS from the Omeka-S Api-- here's a [tutorial](https://github.com/OpenRefine/OpenRefine/wiki/Fetching-URLs-From-Web-Services)

2. They join multiple values in subject and contributor spaces. If you see a number of rows that are mostly blank underneath fuller "records," you'll need to join these 'multi-valued cells' --> One record with multiple rows. You can do this on each column by selecting the <b>Edit cells > join multi-valued cells</b>" 

[More info](https://onlinejournalismblog.com/2014/05/30/how-to-combine-multiple-rows-in-a-dataset-where-text-is-split-across-them-open-refine/])

If your output doesn't have multiple entries in those spots, you can remove those steps from the text file. 

Those steps look like this: 

 '''{
    "op": "core/multivalued-cell-join",
    "description": "Join multi-valued cells in column __anonymous__ - dcterms:subject - __anonymous__ - @value",
    "columnName": "__anonymous__ - dcterms:subject - __anonymous__ - @value",
    "keyColumnName": "__anonymous__ - @id",
    "separator": ";  "
  },
  {
    "op": "core/multivalued-cell-join",
    "description": "Join multi-valued cells in column __anonymous__ - dcterms:contributor - __anonymous__ - @value",
    "columnName": "__anonymous__ - dcterms:contributor - __anonymous__ - @value",
    "keyColumnName": "__anonymous__ - @id",
    "separator": "; "
  },'''

You can also change all the "dcterms:contributor" to another dcterms type and those records should be joined into the single row. 

## Get CSV



## csv headers



itemlink	object-id	subjects	contributors	type	title	format	coverage	language	source	longitude	latitude	image-hash	date	creator
