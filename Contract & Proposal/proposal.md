**EV Charging Station Implementation- CS 225 Project**

Hansen Punnoose, Anton Sebatian, Sijo Joseph, Tommy Park, Vinay Panayanchery

**Abstract**

**How can we optimize the placement of electric vehicle (EV) charging stations in Los Altos Hills, California to maximize accessibility and meet the growing demand of EV users?**

With the rapid growth of electric vehicle(EV) adoption, it is necessary to develop comprehensive and accessible charging infrastructure. In this project, we aim to optimize the placement of EV charging stations in Los Altos Hills, CA by analyzing the current distribution of charging stations and identifying areas with limited accessibility. Using a combination of open-source data and advanced algorithms, this project offers a practical and efficient approach to optimize the placement of electric vehicle (EV) charging stations in Los Altos Hills, California. By employing the A* search algorithm and carefully selected heuristics, this study identifies the shortest paths between high EV adoption areas and charging stations. The analysis will provide specific recommendations for improving charging station placement in Los Altos Hills, considering real-world constraints and trade-offs. Additionally, the study will suggest potential policy changes or incentives to encourage the expansion of charging infrastructure in areas with limited coverage or high demand. The findings and recommendations will be presented through visualizations, such as maps or charts, to illustrate the current distribution of charging stations, areas with limited coverage, and proposed optimal locations for new stations.

**Major Deliverables**

**Deliverable 1: Road Network Graph:**

Data Structure: Adjacency List 

The road network graph will represent the road network of Los Altos Hills, with intersections as nodes and roads as edges. An adjacency list will be used to store the graph efficiently, allowing easy access to neighboring nodes and their respective edge weights. This will be the primary data structure for implementing the A* search algorithm.

**Deliverable 2: Heuristic Function**

Data Structure: Heuristic Function \


A heuristic function is needed to estimate the cost of the least expensive path from a given node to the destination node in the A* search algorithm. This function will take into account factors such as road distance, estimated travel time, or other suitable metrics. The heuristic function will be an important part of the A* algorithm implementation.

**Deliverable 3: Open and Closed Sets**

Data Structure: Priority Queue (Min-Heap and Set) \
 \
Two data structures will be used to maintain the open and closed sets for the A* algorithm. The open set contains nodes that have been evaluated but not yet expanded, while the closed set contains nodes that have already been expanded. A priority queue (min-heap) will be used for the open set to quickly extract the node with the lowest total cost. A set data structure will be used for the closed set to efficiently check for node membership.

**Deliverable 4: Path Reconstruction **

Data Structure: Map (Associative Array)

A map (associative array) will be used to store the parent of each node visited during the A* search. This data structure will allow efficient backtracking from the destination node to the starting node to reconstruct the shortest path once the destination is reached. \
 \
**Deliverable 5: Charging Station Accessibility Metrics **

Data Structure: Multi-dimensional Array (Matrix) \
 \
 A matrix will be used to store the accessibility metrics for each area with high EV adoption rates. Each row of the matrix will represent an area, and the columns will store metrics such as average travel time or distance to the nearest charging station, the number of charging stations within a certain radius, and other relevant indicators. This will allow for efficient analysis and comparison of charging station accessibility across different areas using the A* results. 

**Dataset Acquisition and Processing**


    **Data Access: **The data for this project will be acquired from three sources: OpenstreetMap(OSM), the national renewable energy laboratory (NREL) Alternative fueling station locator for existing charging stations, and the California DMV for adoption rates. 



* OSM Road map data in XML format: [https://overpass-api.de/api/map?bbox=-122.1542,37.3451,-122.0932,37.3947](https://overpass-api.de/api/map?bbox=-122.1542,37.3451,-122.0932,37.3947)
* NREL in JSON: 
    * Sign up for API key at [https://developer.nrel.gov/signup/](https://developer.nrel.gov/signup/)
    * Fuel type: “ELEC”
    * Location: Los Altos Hills, CA
* California DMV in CSV format:
    *  [https://data.ca.gov/dataset/vehicle-fuel-type-count-by-zip-code](https://data.ca.gov/dataset/vehicle-fuel-type-count-by-zip-code)
    * [https://data.ca.gov/dataset/vehicle-fuel-type-count-by-zip-code/resource/7d2f11a4-cc88-4b3a-8b20-5fb64a3b901a/download/vehicle-count-as-of-12-31-2020.csv](https://data.ca.gov/dataset/vehicle-fuel-type-count-by-zip-code/resource/7d2f11a4-cc88-4b3a-8b20-5fb64a3b901a/download/vehicle-count-as-of-12-31-2020.csv)

    **Data Format:**


    **		**

1. **OSM**:  The source of this dataset is OpenStreetMap. We will use the Overpass API to download OSM data specifically for Los Altos Hills, California, in XML. The size of the dataset will vary depending on the level of detail and the bounding box we define. We plan to use a subset of this data, filtering out irrelevant road types, such as pedestrian paths or private roads, to construct the graph representing the road network.
2. **NREL Alternative Fueling Station Data**: The source of this dataset is the National Renewable Energy Laboratory Alternative Fueling Station Locator, which provides information about existing charging stations in the United States. The input of this dataset will be in JSON format, which we obtain through the NREL API. Size of the dataset depends on the limit parameter we set, but we will only consider charging stations in Los Altos Hills. We plan to use a subset of this data, extracting relevant information like station location and charging station type. 
3. **DMV registration data**: The source of this dataset is the California Department of Motor Vehicles (DMV), which provides vehicle registration data, including fuel type counts by zip code. The input format of this dataset is CSV, which we can download from the California Open Data Portal. The dataset includes vehicle registration data for the entire state of California, so it can be quite large. However, we plan to use a subset of this data, filtering the records by zip codes corresponding to Los Altos Hills. We will calculate the proportion of electric vehicles among the total registered vehicles to estimate the EV adoption rates in the area.

**	**


    **Data Correction: **To parse and correct the input data, we will utilize C++ libraries, such as pugixml for OSM XML data and jsoncpp for NREL JSON data. For CSV data, standard C++ file I/O and string manipulation libraries can be employed. During the parsing process, we will check for missing entries, such as incomplete road data or charging station information. Missing data will be handled by either interpolating values, discarding incomplete records, or contacting the data provider for corrections. Additionally, we will verify the plausibility of values and check for statistical outliers, making corrections or filtering out erroneous data as needed.


    **Data Storage: **The primary data structure for this project will be a weighted graph, with intersections as nodes and roads as edges. We will use C++ STL containers, such as std::unordered_map and std::vector, to create adjacency lists representing the graph. Weights will be assigned to edges based on factors like road distance or estimated travel time. Existing charging stations will be included as nodes in the graph, connecting them to the nearest intersection nodes. Auxiliary data structures, such as priority queues for the A* algorithm, will also be used to improve the efficiency of the algorithms. The total storage cost for the dataset will be O(N + M), where N is the number of nodes (intersections and charging stations) and M is the number of edges (road segments) in the graph. 

**Algorithms**


    **Academic Reference: **https://jeffe.cs.illinois.edu/teaching/algorithms/notes


    **	**


    **Function Inputs: **Two primary inputs: the road network graph and the source and destination nodes.



1. The road network graph, represented as an adjacency list, is constructed using preprocessed OpenStreetMap data. The adjacency list enables efficient access to neighboring nodes and their respective edge weights, making it suitable for implementing the A* search algorithm.
2. The source and destination nodes are determined based on the analysis objectives. They can be existing charging stations or areas with high electric vehicle adoption rates, as identified using the California DMV dataset. For each pair of source and destination nodes, the A* search algorithm will compute the shortest path.
3. A key component of the A* search algorithm is the heuristic function, which estimates the cost from a given node to the destination node. The choice of heuristic influences the efficiency and optimality of the search process. Possible heuristics include straight-line distance (Euclidean distance) between nodes, which is admissible and consistent, ensuring the optimality of the algorithm. Another heuristic could be travel time estimation based on speed limits and road types, which may provide a more accurate representation of real-world conditions but may also require additional data preprocessing and computation.

    **Function Outputs: **The A* search algorithm's output is the shortest path between the source and destination nodes, along with the associated cost (e.g., distance or travel time). This path will be represented as an ordered list of nodes (intersections and charging stations) from the source to the destination. The output may include aggregated statistics such as average travel times or distances to the nearest charging station for areas with high electric vehicle adoption rates. Visualization of the outcome could include maps displaying the road network, charging stations, and calculated shortest paths.


    **Function Efficiency:** The target goal for the Big O efficiency of the A* search algorithm in time complexity is O(b^d), where b is the branching factor (average number of neighbors per node) and d is the depth of the shortest solution. In practice, the actual time complexity may be much lower, depending on the effectiveness of the heuristic function in guiding the search. The memory complexity for the algorithm is also O(b^d), as it may need to store all generated nodes in the worst case


    **Testing Strategy: **

1. Validation on small Dataset: We will begin by testing the algorithm on a smaller, well-known dataset with known optimal paths. This will help us verify the correctness of the implementation and identify any potential issues in the basic logic of the algorithm
2. Comparison with real-world routes: After validating the implementation on a smaller dataset, we will test the algorithm on the actual road network data from Los Altos Hills. We will compare the generated paths to real-world routes and known optimal paths, considering any real-world constraints, such as traffic conditions, road closures, or construction, that may affect the route selection.
3. Since the A* the search algorithm's efficiency and optimality depend on the choice of heuristic; we will test the algorithm using different heuristic functions, such as straight-line distance (Euclidean distance) and travel time estimation based on speed limits and road types. We will assess the impact of each heuristic on the overall search efficiency, solution quality, and computational complexity.