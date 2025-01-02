-
- {{query (and (page-property :document [[Project]]) (page-property :status "#inprogress"))}}
  query-properties:: [:page :identity :archetype :metric :year :area :document :status]
- Todo
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :status "#todo"))}}
	  query-sort-by:: year
	  query-sort-desc:: false
	  query-properties:: [:page :identity :archetype :metric :year :document :status]
- Future
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[future]]) (not (page-property :template)))}}
	  query-properties:: [:page :identity :year :status]
- 2025
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2025]]))}}
	  query-properties:: [:page :identity :archetype :metric :year :document :status]
- 2024
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2024]]))}}
	  query-properties:: [:page :identity :year :status]
- 2023
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2023]]))}}
	  query-properties:: [:page :identity :year :status]
- 2022
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2022]]))}}
	  query-properties:: [:page :status :year :identity]
- 2021
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2021]]))}}
- 2020
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2020]]))}}
- 2019
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2019]]))}}
- 2018
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2018]]))}}
- 2017
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2017]]))}}
	  query-properties:: [:page :status :year :identity]
- 2016
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2016]]))}}
	  query-properties:: [:page :status :year :identity]
- 2015
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2015]]))}}
	  query-properties:: [:page :status :year :identity]
- 2014
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2014]]))}}
- 2013
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2013]]))}}
- 2012
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2012]]))}}
- 2011
  collapsed:: true
	- {{query (and (page-property :document [[Project]]) (page-property :year [[2011]]))}}
-
-