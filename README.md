Download Link: https://assignmentchef.com/product/solved-c-s-372-lab-8-finding-singlesource-shortest-paths-in-loglinear-time
<br>






In this lab, you will implement the Dijkstra’s algorithm. You will use two types of data structure to construct a priority queue to be used in the algorithm: a linked list and a min­heap. You will test your implementation and also compare the performance of the two data structures on large graphs.

You have an opportunity to earn 300% extra credit by writing a map routing program that will find a route from an origin to a destination using a world travel map.

<h1>1        Requirement for the Dijkstra algorithm</h1>

Design the first Dijkstra’s algorithm with the following function prototype that uses an unsorted linked list as priority queue:

void     D i j k s t r a _ l i s t ( Graph &amp; G,   Node &amp; s )

{

<table width="531">

 <tbody>

  <tr>

   <td width="25">/ /</td>

   <td width="346">Input :       graph G,    e i t h e r     undirected       or</td>

   <td width="160">directed ,         and</td>

  </tr>

  <tr>

   <td width="25">/ /</td>

   <td width="346">       a    source    node   s</td>

   <td width="160"></td>

  </tr>

  <tr>

   <td width="25">/ /</td>

   <td width="346">Output :      the   e f f e c t   of    the           algorithm</td>

   <td width="160">i s    that    a l l   nodes</td>

  </tr>

  <tr>

   <td width="25">/ /</td>

   <td width="346">       are    marked    with    a    distance     from       s</td>

   <td width="160"></td>

  </tr>

  <tr>

   <td width="25">/ /</td>

   <td width="346">Perform    D i j k s t r a ’ s    algorithm     on       the</td>

   <td width="160">input      graph       from</td>

  </tr>

  <tr>

   <td width="25">/ /</td>

   <td width="346">       a    given    node   s</td>

   <td width="160"></td>

  </tr>

  <tr>

   <td width="25">/ /</td>

   <td width="346">Use an      unsorted      linked     l i s t   f o r       the</td>

   <td width="160">p r i o r i t y  queue</td>

  </tr>

 </tbody>

</table>

}

Design the second Dijkstra’s algorithm with the following function prototype that uses a min­heap as priority queue:

void         Dijkstra_heap ( Graph &amp; G,        Node &amp; s )

{

/ / Input : graph G, e i t h e r undirected or directed , and / / a source node s

/ / Output : the e f f e c t of the algorithm i s that a l l nodes / / are marked with a distance from s

/ /    Perform   D i j k s t r a ’ s    algorithm     on   the     input     graph    from

/ /        a    given    node   s

/ /     Use a min−heap     f o r   the   p r i o r i t y  queue

}

The effect of the Dijkstra’s algorithm on the graph <em>G </em>is distance labels indicating the distance from source node <em>s </em>to every node in the graph. They will be stored within the Graph data structure. You can enhance the graph class from previous labs in more than one way. You are free to design your strategy and describe it in your lab report. The distance values must not be saved as global variables.

<h1>2        Technical notes</h1>

The priority queue is a dynamically changing data structure and its implementation can be subject to memory problems.

<ol>

 <li>The graph data structure needs to be expanded to handle the edge weight.</li>

 <li>The graph file will contain three numbers in a row, where the last number is the weight of the edge defined by the first two nodes. Your code for reading/writing a graph file will need to be updated to handle the weight as well.</li>

 <li>You will also modify the R file to randomly generate large positively weighted graphs.</li>

 <li>When using an unsorted linked list for the priority queue, the remove­min operation can be achieved by finding the minimum element and then removing it from the list. To traverse a list, you cannot use an index but you can use an iterator. To remove an element from a list, you can use the list::erase()</li>

 <li>The C++ function make_heap() by default makes a max­heap, not minheap. You can make a min­heap by specifying a customized comparison function optional to make_heap().</li>

 <li>Your code must determine the position of a node in the heap in constant time before calling the decrease­key operation on the heap. You can maintain a heap index for each node to resolve this issue.</li>

 <li>As the remove­min and decrease­key operations will modify the heap, the positions of each node in the heap must be updated accordingly. You can manage the positions of each node in the heap via the heap index.</li>

 <li>You can use the following C++ function</li>

</ol>

numeric_limits&lt;double&gt;::infinity()

to define infinity ∞ for the initial distance of each node other than <em>s</em>. The header file limits must be included to use this function. This option is preferable to either ­1 or a very large number from the software engineering point of view.

<h1>3        TestyourimplementationsofDijkstra’salgorithms</h1>

Generate five examples of weighted graphs to test your code. The graphs do not have to be very large but must represent a variety: cyclic/acyclic, directed/undirected, and some having more than one connected component.

Your C++ program must include a main() function that calls the testall() function. When the program is compiled by a C++ compiler it generates a binary executable file that will run when invoked from the command line.

<h1>4        Plot the runtimes of the two Dijkstra’s implementations</h1>

After testing the correctness of the the program, you will study how the runtime scales with the size of graph for the two methods. Use the random graph function you developed in Lab 4 to generate random graphs of increasing sizes.

You will produce four curves in R:

<ol>

 <li>Dijkstra_list runtime as a function of number of nodes in the graph, given the number of edges.</li>

 <li>Dijkstra_heap runtime as a function of number of nodes in the graph, given the number of edges.</li>

 <li>Dijkstra_list runtime as a function of number of edges in the graph, given the number of nodes.</li>

 <li>Dijkstra_heap runtime as a function of number of edges in the graph, given the number of edges.</li>

</ol>

Ideally, the first two curves should be plotted in the same figure for easy comparison; and the last two in another figure.

Your algorithm must be able to handle graphs with 10,000 or more nodes and 1,000,000 or more edges in the order of tens of seconds.

<h1>5        Extra credit (300%): Shortest routes between any two waypoints on earth</h1>

You will apply the Dijkstra’s algorithm on a world travel map [Teresco, 2012] (<a href="http://courses.teresco.org/metal/">http: </a><a href="http://courses.teresco.org/metal/">//courses.teresco.org/metal/</a>) to find a shortest path from one place to another. The map contains 587,376 highway waypoints (nodes) and 665,270 road segments (edges) connecting them on the Earth.

<h2>5.1       Travel Mapping Graph file format</h2>

The map we will use is in a Travel Mapping Graph (tmg) simple format as described in <a href="http://courses.teresco.org/metal/graph-formats.shtml">http://courses.teresco.org/metal/graph­formats.shtml</a>:

<ul>

 <li>The first line specifies the file format. It consists of three spaceseparated entries, the first of which must be “TMG”. The second is a version number, which much be “1.0”. The third entry is either “simple” or “collapsed” indicating whether the edge data is in simple format or collapsed edge format.</li>

 <li>The second line consists of two numbers: the number of vertices (waypoints) |<em>V </em>|, and the number of edges, |<em>E</em>|, (road segments that connect adjacent waypoints).</li>

 <li>The next |<em>V </em>| lines describe the waypoints. Each line consists of a string describing a waypoint, followed by its latitude and longitude as floating­point numbers.</li>

 <li>The last |<em>E</em>| lines describe the road segments. Each line consists of two numbers specifying the waypoint numbers (0­based and in the order read in from this file) connected by this road segment, followed by a string with the name of the road or roads that form this segment. For “collapsed” format graphs, a line describing an edge can optionally have a list of the space­separated latitudes and longitudes of shaping points that define a more accurate path (for both mapping and for computing distances) of the road segment.</li>

 <li>A “simple” format graph is simply a “collapsed” format graph with no edge shaping points.</li>

</ul>

You will download the file tm-master-simple.tmg from <a href="http://travelmapping.net/graphdata/tm-master-simple.tmg">http://travelmapping.net/graphdata/tm-master-simple.tmg </a>The file size is about 33.3 MB.

Please note that the graph should be treated as undirected.

<h2>5.2       The routing task</h2>

You will use the Dijkstra’s algorithm you have just developed to find the shortest path from a given original waypoint to a destination waypoint. For example, if the input pair of waypoints is

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="612f2c53565021">[email protected]</a>+X478507 35.807616 ­104.446678

and

NY11C_N/US11_N 44.776047 ­74.672871

you should print out a shortest path from the first waypoint (in New Mexico) to the second (in update New York) in the following fashion:

Origin:

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="5e10136c696f1e">[email protected]</a>+X478507 35.807616 -104.446678

[road segment 1]

[intermediate waypoint 1]

[road segment 2]

[intermediate waypoint 2] [road segment 3] …

Destination:

NY11C_N/US11_N 44.776047 -74.672871 Total distance: 2021 miles

If the two waypoints are on road­disconnected continents (e.g., one in Asia one in North America), your program should report that no road is possible to connect the two waypoints.

<h2>5.3       The distance between two waypoints</h2>

In order to compute the total distance, your code will use the latitude and longitude of each pair of waypoints (<em>lat</em><sub>1</sub><em>,lon</em><sub>1</sub>) and (<em>lat</em><sub>2</sub><em>,lon</em><sub>2</sub>) to estimate edge length in miles using the Haversine formula:

(1)

(2)

/2)                    (3)

(4)

(5)

where 3961 is the radius of the Earth in miles.


