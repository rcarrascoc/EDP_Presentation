## Exploring the potential of new GPU features for Convex Hull algorithm
----
### By Roberto Carrasco
----



----
## Outline
----
<ul>
    <li>Introduction</li>
    <li>Basic concepts</li>
    <li>Problem statement</li>
    <li>Hypotheses and goal</li>
    <li>Algorithm</li>
    <li>Advances related to each goal</li>
    <li>Summary</li>
    <li>Work plan</li>
</ul>

Note: This will only appear in the speaker notes window.



----
<h2> Introdution </h2>
----

<p>What convex hull is?</p>

<img src="/assets/images/ch_car.gif" alt="drawing" width="600"/>
<!img src="/assets/images/convex_Hull.png" alt="drawing" width="500"/>




----
<h2> Basic concepts</h2>
----
<p>Preprocessing</p>

<p>GPU</p>



<h3> Preprocessing</h3>
----



<h3> GPU</h3>
----
<div class="container">
    <div class="col">
        <img src="/assets/images/cuda.png" alt="drawing" width="600"/>
    </div>
    <div class="col">
        <img src="/assets/images/cub.png" alt="drawing" width="600"/>
    </div>
    <div class="col">
        <img src="/assets/images/thrust.png" alt="drawing" width="600"/>
    </div>
</div>



<h3> Why I wanna accelerate that</h3>
----
<div class="container">
    <div class="col">
        <ul>
            <li>Video Games</li>
            <li>Selfdriver</li>
            <li>Face recognition</li>
            <li>Robotic</li>
            <li>Data mining</li>
        </ul>
    </div>
    <div class="col">
        <img src="/assets/images/collision.jpeg" alt="drawing" width="500"/>
    </div>
</div>



-----
<h2> Problem statement</h2>
-----



-----
<h2> Hypotheses and goal</h2>
-----



<h3> Hypotheses </h3>
-----
<ol>
    <li>A parallel pre-processing technique can improve the state-of-the-art on GPU-based convex hull algorithms.</li>
    <li>The use of the new features of modern GPUs, such as tensor cores and ray tracing cores, can speed up the state-of-the-art GPU convex hull calculation.</li>
</ol>



### Main objective
-----
Design new parallel algorithms for solving convex hull problems over arbitrary point sets, efficient, robust, scalable, and satisfying correctness criteria



### Specific objectives
-----
<ol>
    <li>Review and identify the state-of-the-art convex hull algorithms and filtering techniques.</li>
    <li>Develop GPU pre-processing filtering techniques in two dimensions for convex hull and compare their efficiency with the state-of-the-art.</li>
    <li>Improve the state-of-the-art 3D filtering for convex hull algorithms both sequential and parallel and compare the performance of the new approaches with the state-of-the-art.</li>
    <li>Evaluate the contributions of the proposed algorithms in generating Delaunay triangulations and handling dynamic scenarios.</li>
</ol>



-----
## Algorithm
-----
```
Require: Set of points
Ensure: Set of points candidae to the hull
    1. Finding the polygon/polyedron
    2. Extracting candidite points
    3. Computing the convex hull from the candidate points
```



## 1. Finding the polygon/polyhedron
<div class="container">
    <div class="col">
        <img src="/assets/images/porygon.png" alt="drawing"/>
    </div>
    <div class="col">
        <img src="/assets/images/porygon2.png" alt="drawing"/>
    </div>
</div>



## 1.1 Two Dimension: Eight-side Polygon
<img src="/assets/images/fig_filter.png" alt="drawing" width="600"/>



## 1.1 Two Dimension: Eight-side Polygon
<img src="/assets/images/d_distance.png" alt="drawing" width="600"/>



## 1.2 Three Dimension: Twenty-four-face Polyhedron
<img src="/assets/images/3d_filter.PNG" alt="drawing" width="900"/>



## 2. Extracting Candidate Points
<img src="/assets/images/polygon.png" alt="drawing" width="400"/>



## 3. Computing The Convex Hull From The Candidate Points
<img src="/assets/images/hull.png" alt="drawing" width="400"/>



<h2>Publications</h2>
<h3 style="text-align: left">Published in</h3>
<p style="text-align: justify; font-size:60%">[1] Roberto Carrasco, Hector Ferrada, Cristobal A. Navarro, Nancy Hitschfeld, <b>An evaluation of GPU filters for accelerating the 2D convex hull</b>, Journal of Parallel and Distributed Computing, Volume 184, 2024, 104793, ISSN 0743-7315, https://doi.org/10.1016/j.jpdc.2023.104793.</p>
<h3 style="text-align: left">Submitted to</h3>
<p style="text-align: justify; font-size:60%">[2] Roberto Carrasco, Hector Ferrada, Cristobal A. Navarro, Nancy Hitschfeld, <b>GPU Preprocessing for Accelerating 3D Convex Hull Computation</b>, LATIN24.</p>
<h3 style="text-align: left">Writting</h3>
<p style="text-align: justify; font-size:60%">[2] Sergio Salinas-Fernandez, Roberto Carrasco-Cavieres, Nancy Hitschfeld-Kahler, <b>GPolylla: GPU-accelerated polygonal mesh generator</b></p>



-----
## Advances and results related to each objective
-----



### Objective 1: Review and identify the state-of-the-art on convex hull algorithms and filtering techniques.
----



### Objective 2: Develop GPU preprocessing filtering techniques in two dimensions for convex hull and compare their efficiency with the state-of-the-art.
----
<img src="/assets/images/paper1.PNG" alt="drawing" width="700"/>



#### Our Variants
<ol>
    <li>thrust\_copy</li>
    <li>thrust\_scan</li>
    <li>cub\_flagged</li>
    <li>gpu\_scan</li>
    <li>omp\_manhattan</li>
    <li>omp\_euclidean</li>
    <li>cpu\_manhattan</li>
    <li>cpu\_euclidean</li>
</ol>



<h4 style="text-align: left;">Objective 2 - Experiment 1:</h4>
<img src="/assets/images/study_cases_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Graphic representation of the distributions. The figure on the left side corresponds to a normal distribution with a mean of 1 and a standard deviation of 0.1. Next to it is a uniform distribution with a mean of 1 and a standard deviation of 0.1. Finally, the figure on the right is a circumference centered at the origin with a
radius of 1. </p>



<h4 style="text-align: left;">Objective 2 - Experiment 1:</h4>
<img src="/assets/images/experiment1_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup over the \texttt{cpu\_euclidean} filter, considering only the preprocessing filtering phase, for all our proposed variants implemented in GPU, CPU-sequential, and CPU-parallel (using OpenMP with 32 threads), respectively; for normal, uniform, and circumference distributions. The point range is between $2^{25}$ and $2^{30}$, with equidistant sampling. </p>



<h4 style="text-align: left;">Objective 2 - Experiment 1:</h4>
<img src="/assets/images/experiment1_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup of filter + CGAL:convex_hull_2 over the convex hull filtered with cpu_euclidean, for all our proposed variants implemented in GPU, CPU-sequential, and CPU-parallel (using OpenMP with 32 threads), respectively; for normal, uniform, and circumference distributions. The point range is between 225 and 230, with equidistant sampling. </p>



<h4 style="text-align: left;">Objective 2 - Experiment 1:</h4>
<img src="/assets/images/experiment1_2_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup of filter + \texttt{CGAL:convex\_hull\_2} over the convex hull filtered with \texttt{cpu\_euclidean}, for all our proposed variants implemented in GPU, CPU-sequential, and CPU-parallel (using OpenMP with 32 threads), respectively; for normal, uniform, and circumference distributions. The point range is between $2^{25}$ and $2^{30}$, with equidistant sampling. </p>



#### Competitors
<ol>
    <li>CGAL:convex\_hull\_2</li>
    <li>CGAL:graham\_andrew</li>
    <li>Qhull</li>
    <li>cudachain</li>
</ol>



<h4 style="text-align: left;">Objective 2 - Experiment 1:</h4>
<img src="/assets/images/experiment1_3_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup of our fastest filters + \texttt{CGAL:convex\_hull\_2} over \texttt{CGAL:convex\_hull\_2}, for our fastest proposed variants implemented on GPU, CPU-sequential, CPU-parallel (using \texttt{OpenMP} with 32 threads), and some fast implementation on the state-of-the-art (\texttt{CGAL}, \texttt{Qhull} and \texttt{cudachain}); for normal, uniform and circumferential distributions. The range of points is between $2^{25}$ and $2^{30}$, with equidistant sampling. </p>



<h4 style="text-align: left;">Objective 2 - Experiment 2:</h4>
<img src="/assets/images/bad_cases.PNG" alt="drawing" width="900"/>
<p style="text-align: center; font-size:60%"><b>Figure: </b>
The intermediate-case test with randomly selected displacement at different values.</p>



<h4 style="text-align: left;">Objective 2 - Experiment 2:</h4>
<img src="/assets/images/experiment2_1_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Running time of the convex hull algorithm for a displaced circumference (intermediate case) varying $p$ between $[0, 0.3]$, and fixed size. </p>



<h4 style="text-align: left;">Objective 2 - Experiment 2:</h4>
<img src="/assets/images/experiment2_2_2d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup of the convex hull algorithm over \texttt{CGAL:convex-hull-2} for a displaced circumference (intermediate case) varying $p$ between $[0, 0.3]$, and fixed size. </p>



### Objective 3: Improve the state-of-the-art on 3D filtering for convex hull algorithms both sequential and parallel and compare he performance of the new approaches with the state-of-the-art.
----
<img src="/assets/images/paper2.PNG" alt="drawing" width="500"/>



<h4 style="text-align: left;">Objective 3 - Experiment 1:</h4>
<img src="/assets/images/study_cases_3d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Illustration of the normal, uniform, and spherical distributions using randomly generated points in 3 dimensions. </p>



<h4 style="text-align: left;">Objective 3:</h4>
<img src="/assets/images/experiment_1_3d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Execution time in milliseconds of filters using Euclidean and Manhattan
distances as metrics to find extreme points in normal, uniform, and spherical
distributions, varying between 33 million and 270 million points. </p>



<h4 style="text-align: left;">Objective 3:</h4>
<img src="/assets/images/experiment_2_3d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup of filters using Euclidean and Manhattan distances as metrics
to find extreme points in normal, uniform, and spherical distributions, varying
between 33 million and 270 million points. </p>



<h4 style="text-align: left;">Objective 3:</h4>
<img src="/assets/images/experiment_3_3d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Execution time in milliseconds to compute the convex hull using a preprocessing step, using the CGAL library for the hull computation, on normal,
uniform, and spherical distributions, varying between 33 million and 270 million
points. </p>



<h4 style="text-align: left;">Objective 3:</h4>
<img src="/assets/images/experiment_4_3d.PNG" alt="drawing" width="900"/>
<p style="text-align: justify; font-size:60%"><b>Figure: </b>
Speedup to compute the convex hull using a preprocessing step, using
the CGAL library for the hull computation, on normal, uniform, and spherical
distributions, varying between 33 million and 270 million points. </p>



<h4 style="text-align: center;">Objective 3:</h4>
<p> Ray Tracing... soon </p>
<img src="/assets/images/rtx.png" alt="drawing"/>



### Objective 4: Evaluate contributions of the proposed algorithms at generating Delaunay triangulations and handling dynamic scenarios.



-----
## Summary
-----
<div class="container">
    <div class="col">
        uwu
    </div>
    <div class="col">
    </div>
</div>



-----
## Work plan
-----



## supported by
-----
<img src="/assets/images/anid_rojo_azul.png" alt="drawing" width="200"/>



## sponsored by
-----
<img src="/assets/images/logobw.png" alt="drawing" width="200"/>



## hosted by
-----
<div class="container" data-background-color="aquamarine">
    <div class="col">
        <img src="/assets/images/logobw.png" alt="drawing" width="200"/>
    </div>
    <div class="col">
        <img src="/assets/images/logobw.png" alt="drawing" width="200"/>
    </div>
</div>