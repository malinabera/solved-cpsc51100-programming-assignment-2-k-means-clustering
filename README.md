Download Link: https://assignmentchef.com/product/solved-cpsc51100-programming-assignment-2-k-means-clustering
<br>
Clustering has many applications, including inferring population structures from genetic data, recognizing communities within social networks, or segmenting of customers for market research.




One of the most popular algorithms for performing clustering is the <em>k</em>-means method. The algorithm depends on the notion of <em>distance</em> between two points. For points with only one dimension (just single values), we can define the distance between two points  and  as




The k-means algorithm will work by placing points into clusters and computing their <em>centroids</em>, which is defined as the average of the data points in the cluster. Specifically, the algorithm works as follows:

<ol>

 <li>Pick k, the number of clusters.</li>

 <li>Initialize clusters by picking one point (centroid) per cluster. For this assignment, you can pick the first <em>k</em> points as initial centroids for each corresponding cluster.</li>

 <li>For each point, place it in the cluster whose current centroid it is nearest.</li>

 <li>After all points are assigned, update the locations of centroids of the k clusters</li>

 <li>Reassign all points to their closest centroid. This sometimes moves points between clusters.</li>

 <li>Repeat 4,5 until convergence. Convergence occurs when points don’t move between clusters and centroids stabilize.</li>

</ol>










<strong>Requirements</strong>

You are to create a program using Python that does the following:

<ol>

 <li>Asks the user for the number of clusters. This is the parameter <em>k</em> that will be used for <em>k</em>-means.</li>

 <li>Reads the input file (prog2-input-data.txt) and stores the points into a list</li>

 <li>Applies the k-means algorithm to find the cluster for each point.</li>

 <li>Displays the points that each cluster contains after each iteration of the algorithm</li>

 <li>Writes the final cluster assignments to the screen and the output file (prog2-output-data.txt).</li>

</ol>




YOU CANNOT USE ANY PYTHON PACKAGES FOR THIS PROGRAM (NUMPY, PANDAS, …) – NO IMPORT STATEMENTS.




<strong>Additional Requirements</strong>

<ol>

 <li>The name of your source code file should be py. All your code should be within a single file.</li>

 <li>Your code should follow good coding practices, including good use of whitespace and use of both inline and block comments.</li>

 <li>You need to use meaningful identifier names that conform to standard naming conventions.</li>

 <li>At the top of each file, you need to put in a block comment with the following information: your name, date, course name, semester, and assignment name.</li>

 <li>The output of your program should <strong>exactly</strong> match the sample program output given at the end. That is, for same input, it should generate the same output. Note that I may use other test cases for grading your program and your code needs to work correctly in all cases.</li>

</ol>







<strong> </strong>

<strong>Data File Format</strong>

Let N be the number of points and Pi to be the value of point i. The input file should be of the following format:

P1

P2

…

PN




Example:

1.2

2.1

4.56

2.113

2.2




The name of the input file is always:

prog2-input-data.txt




<strong>What to Turn In</strong>

You will turn in the single kMeans.py file using BlackBoard.




<strong>HINTS</strong>

<ul>

 <li>Make use of list comprehensions for reading lines from a file and then converting the strings into a list of floats.</li>

 <li>Use pwd() to check the directory where you should place your input file.</li>

 <li>Use a dict data structures for storing centroids and clusters. The centroids dict will be a mapping from cluster number to centroids. The clusters dict will be a mapping from cluster number to a list of points in the cluster.</li>

</ul>




<strong># Initialization</strong>

<ol>

 <li>Print header info to screen</li>

 <li>Get input/output file names and number of clusters</li>

 <li>Read file:</li>

</ol>

-use open() and a list comprehension to strip all lines of ending char (using rstrip method) and convert to floats

<ol start="4">

 <li>Create variables to store centroids, clusters, and point assignments. Initially, pick one point (centroid) per cluster:</li>

</ol>

-create and initialize a variable to store centroids for each cluster: a mapping (dict) from range(k) to data[0:k]

-create and initialize another variable to store all points for each cluster: a mapping (dict) of range(k) to k empty lists

-use zip when creating the dict

-create and initialize a dict mapping points to clusters

-create a variable to store old point assignments (from previous iteration)

# Algorithm

<ol start="5">

 <li>Repeat the following:</li>

 <li>a) Save current point assignment into old point assignment variable (create a new dict from current assignment</li>

</ol>

variable)

<ol>

 <li>b) Place each point in the closest cluster (you should make a function that does this)</li>

 <li>c) Update the locations of centroids of the k clusters (make a function for this also)</li>

 <li>d) Reinitialize the clusters variable to empty lists</li>

</ol>

# Output

<ol start="6">

 <li>Print the point assignments</li>

</ol>

DETAILED HINTS

# Initialization

<ol>

 <li>Print header info to screen</li>

</ol>

Use print function.

<ol start="2">

 <li>Get input/output file names and number of clusters</li>

</ol>

Use raw_input. For number of clusters (k), make sure to use int() to convert to an integer.

<ol start="3">

 <li>Read file:</li>

</ol>

-use open() and a list comprehension to strip all lines of ending char (using rstrip method) and

convert to floats

I basically showed this in the video:

data = [float(x.rstrip()) for x in open(input_file)]

<ol start="4">

 <li>Create variables to store centroids, clusters, and point assignments. Initially, pick one point</li>

</ol>

(centroid) per cluster:

-create and initialize a variable to store centroids for each cluster: a mapping (dict) from range(k)

to data[0:k]

centroids = dict(zip(range(k),data[0:k])

-create and initialize another variable to store all points for each cluster: a mapping (dict) of

range(k) to k empty lists -use zip when creating the dict

clusters = dict(zip(range(k),[[] for i in range(k)]))

-create and initialize a dict mapping points to clusters

First, think about how points are represented – as numbers in a list, with each number having an

index value. So you can do a mapping between each of the index values (0..k-1) and the cluster

to which the point having this index value belongs. Initially, the points won’t belong to any

cluster, so you can just map to dummy values. Later, you will update these with appropriate

values (after each iteration).

-create a variable to store old point assignments (from previous iteration)

Since there is no previous assignment on first iteration, just assign an empty dict to an

old_point_assignments variable

# Algorithm

<ol start="5">

 <li>Repeat the following:</li>

 <li>a) Save current point assignment into old point assignment variable (create a new dict from</li>

</ol>

current assignment variable)

This should create a copy of the dict holding the point assignments into the

old_point_assignments variable

<ol>

 <li>b) Place each point in the closest cluster (you should make a function that does this)</li>

</ol>

Make a function called assign_to_clusters that takes as input: data, clusters, centroids, and

point_assignments. The function should go through each point and index of that point in data

(use enumarate()) and find the closest centroid. Then add that point to the list of points for that

clusters in the clusters variable. Also, do:

point_assignments[j] = closest_index

<ol>

 <li>c) Update the locations of centroids of the k clusters (make a function for this also)</li>

</ol>

Make a function that takes as input: data, clusters, and centroids. It should go through each list

contained in clusters variable and recompute the centroid by averaging over all the points in that

list (use sum() and len() functions). After computing, update the corresponding centroids value.

<ol>

 <li>d) Reinitialize the clusters variable to empty lists</li>

</ol>

clusters = dict(zip(range(k),[[] for i in range(k)]))

# Output

<ol start="6">

 <li>Print the point assignments</li>

</ol>

Go through all values in point_assignments and print them.







Sample Program Output

CPSC-51100, [semester] [year]

NAME: [put your name here]

PROGRAMMING ASSIGNMENT #2




Enter the number of clusters: 5




Iteration 1

0 [1.8]

1 [4.5, 6.5]

2 [1.1, 0.5]

3 [2.1, 3.2]

4 [9.8, 7.6, 11.32]




Iteration 2

0 [1.8, 2.1]

1 [4.5, 6.5]

2 [1.1, 0.5]

3 [3.2]

4 [9.8, 7.6, 11.32]




Iteration 3

0 [1.8, 2.1]

1 [4.5, 6.5]

2 [1.1, 0.5]

3 [3.2]

4 [9.8, 7.6, 11.32]




Point 1.8 in cluster 0

Point 4.5 in cluster 1

Point 1.1 in cluster 2

Point 2.1 in cluster 0

Point 9.8 in cluster 4

Point 7.6 in cluster 4

Point 11.32 in cluster 4

Point 3.2 in cluster 3

Point 0.5 in cluster 2

Point 6.5 in cluster 1







Output File Contents

Point 1.8 in cluster 0

Point 4.5 in cluster 1

Point 1.1 in cluster 2

Point 2.1 in cluster 0

Point 9.8 in cluster 4

Point 7.6 in cluster 4

Point 11.32 in cluster 4

Point 3.2 in cluster 3

Point 0.5 in cluster 2

Point 6.5 in cluster 1