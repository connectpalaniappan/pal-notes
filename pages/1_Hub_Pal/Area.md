- Pick only 4 areas to focus on
-
- {{embed ((67746629-c145-4049-b02d-be66b4775f9b))}}
  query-properties:: [:page :created :assignedto :targetcompletiondate :completed :type :year :tags :nexttaskdate :created-at :updated-at]
- Todo
	- {{query (and (page-property :document [[Area]]) (page-property :status "#todo") (not (page-property :template)))}}
- Future
	- {{query (and (page-property :document [[Area]]) (page-property :year [[future]]) (not (page-property :template)))}}
	  query-properties:: [:page :identity :archetype :ideas]
	  query-sort-by:: identity
	  query-sort-desc:: false
- 2025
	- {{query (and (page-property :document [[Area]]) (page-property :status "#inprogress"))}}
	  id:: 67746629-c145-4049-b02d-be66b4775f9b
	  query-properties:: [:page :identity :archetype :metric :ideas]
- 2024
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2024]]))}}
	  query-properties:: [:page :identity :year :status]
- 2023
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2023]]))}}
	  query-properties:: [:page :identity :year :status]
- 2022
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2022]]))}}
	  query-properties:: [:page :status :year :identity]
- 2021
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2021]]))}}
- 2020
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2020]]))}}
- 2019
	- {{query (and (page-property :document [[Area]])(page-property :year [[2019]]))}}
- 2018
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2018]]))}}
- 2017
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2017]]))}}
	  query-properties:: [:page :status :year :identity]
- 2016
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2016]]))}}
	  query-properties:: [:page :status :year :identity]
- 2015
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2015]]))}}
	  query-properties:: [:page :status :year :identity]
- 2014
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2014]]))}}
- 2013
	- {{query (and (page-property :document [[Area]]) (page-property :year [[2013]]))}}
- 2012
	- {{query (and (page-property :document [[Area]])(page-property :year [[2012]]))}}
- 2011
	- {{query (and (page-property :document [[area]]) (page-property :year [[2011]]))}}
-