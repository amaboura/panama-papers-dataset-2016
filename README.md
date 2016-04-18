# Panama Papers Dataset 2016
Structured data about Panama papers collected from the official ICIJ website 
### How were the data collected ?
I wrote a detailed explanation [here](COLLECTION.md)
### Dataset structure
```
├── de.csv
├── en.csv
├── es.csv
├── fr.csv
├── pt.csv
└── viz-data
    ├── 014fe3bc.json
    ├── 02664021.json
    ├── 034793d9.json
    ├── 08cc5165.json
    ├── 0a1122ef.json
    ├── 0a3cf4fd.json
    ├── 0dae973f.json
	 ...
	 ...
	 ...
	├── fb706ef9.json
    ├── fb7f4be3.json
    └── ff9bbc4d.json
└── csv-viz-data
    ├── 014fe3bc-nodes.csv
    ├── 014fe3bc-edges.csv
    ├── 02664021-nodes.csv
     ...
     ...
     ...
    ├── fb7f4be3-edges.csv
    ├── ff9bbc4d-nodes.csv
    └── ff9bbc4d-edges.csv
└── iPython NB
    ├── Panama Project.ipynb
```

### Explore the data
the main data provided by ICIJ can be found in CSV file, that is available in 4 languages

#### Main files
The CSV file is broken down to the following columns

```
story-title
story-subtitle
story-image-if-linked-person
story-narrative
story-category-code
story-priority
story-region-codes
story-country-1-code
story-country-1-name
story-country-2-code
story-country-2-name
story-document-1-title
data-person-1-name
data-person-1-description-if-politician
data-person-1-relationship,
data-person-1-image
data-person-1-viz-publish
data-person-1-comment
```

#### Visualization data
ICIJ report provided a set of visualizations that you can browser through this [link](https://panamapapers.icij.org/the_power_players/)

Data content for these visualizations is a graph structure, each graph is encoded to a JSON file, named after the ``` data-person-1-viz-publish ``` attribute found in the main CSV file.

#### Visualization nodes and edges csv data
The JSON data is normalized and the nodes and edges data is given in different csvs.

#### iPython Notebook
An iPyhton notebook to load and normalize the json data and play around with it.

#### Disclaimer
I have nothing to do with ICIJ, This is just a small project i started to see if i can get the published data, and do some cool stuff with it.

#### Credit
All the data are coming from the official [ICIJ website](https://panamapapers.icij.org/graphs/)

#### Contribute
This is a data dump, CSV and JSON files are not organized and cleaned, feel free to send a PR if you want to do that ;) 
