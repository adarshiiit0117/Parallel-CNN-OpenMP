

<h1>CNN-OpenMP</h1>

<h2>Overview</h2>
<p>
CNN-OpenMP is an implementation of a <strong>Convolutional Neural Network (CNN) from scratch in C</strong>,
created to understand both the <strong>internal workings of CNNs</strong> and the
<strong>application of shared-memory parallelism using OpenMP</strong>.
</p>

<p>The project includes:</p>
<ul>
    <li>A <strong>serial (single-threaded) implementation</strong> as a correctness baseline</li>
    <li>A <strong>parallel OpenMP implementation</strong> to accelerate compute-intensive CNN operations</li>
</ul>

<p>
This implementation avoids high-level machine learning frameworks and focuses on
<strong>low-level programming, parallel computing concepts, and performance analysis</strong>.
</p>

<hr>

<h2>CNN Pipeline Implemented</h2>
<p>The CNN forward pass implemented in this project consists of the following stages:</p>
<ol>
    <li>Reading input matrices from text files</li>
    <li>Zero padding</li>
    <li>2D convolution using multiple kernels</li>
    <li>Sigmoid activation function</li>
    <li>Max pooling (downsampling)</li>
    <li>Output feature map generation</li>
</ol>

<hr>

<h2>Input Format</h2>
<p>Each input file should follow this format:</p>
<pre>
N
a11 a12 a13 ... a1N
a21 a22 a23 ... a2N
...
aN1 aN2 aN3 ... aNN
</pre>

<ul>
    <li><strong>N</strong> is the size of the square matrix</li>
    <li>Values are floating-point numbers</li>
</ul>

<p>Expected input files:</p>
<ul>
    <li><code>input.txt</code> – input image</li>
    <li><code>kernel1.txt</code> – convolution kernel 1</li>
    <li><code>kernel2.txt</code> – convolution kernel 2</li>
    <li><code>kernel3.txt</code> – convolution kernel 3</li>
</ul>

<div class="note">
    <strong>Note:</strong> Input files are not included in the repository because they are runtime-dependent
    and may vary across executions.
</div>

<hr>

<h2>Compilation and Execution</h2>

<h3>Serial Version</h3>
<pre>
gcc serial.c -o serial -lm
./serial
</pre>

<h3>Parallel Version (OpenMP)</h3>
<pre>
gcc parallel.c -o parallel -fopenmp -lm
./parallel
</pre>

<hr>

<h2>Parallelization Strategy</h2>
<p>
OpenMP is used to parallelize the most compute-intensive operations in the CNN pipeline:
</p>
<ul>
    <li>Convolution</li>
    <li>Sigmoid activation</li>
    <li>Max pooling</li>
</ul>

<p>Nested loops are parallelized using:</p>
<pre>
#pragma omp parallel for collapse(2)
</pre>

<p>
Each thread operates on independent data elements, ensuring the implementation is
<strong>race-condition free</strong> without requiring synchronization primitives such as locks or atomic operations.
</p>

<hr>

<h2>Performance Analysis</h2>
<ul>
    <li>The serial implementation serves as a correctness baseline</li>
    <li>The OpenMP implementation leverages multiple CPU cores to reduce execution time</li>
    <li>Profiling using <code>gprof</code> confirms correct execution flow and function calls</li>
    <li>Due to small input sizes, execution time may fall below the profiler’s sampling resolution</li>
    <li>Wall-clock timing (e.g., <code>omp_get_wtime()</code>) is preferred for accurate performance evaluation</li>
</ul>

<hr>

<h2>Key Learning Outcomes</h2>
<ul>
    <li>Implemented CNN operations without using machine learning libraries</li>
    <li>Gained a clear understanding of convolution, padding, activation, and pooling</li>
    <li>Applied OpenMP for shared-memory parallelism</li>
    <li>Analyzed performance bottlenecks and parallelization limits</li>
    <li>Learned practical profiling and performance evaluation techniques</li>
</ul>

<hr>

<h2>Technologies Used</h2>
<ul>
    <li>C</li>
    <li>OpenMP</li>
    <li>GCC</li>
    <li>gprof</li>
</ul>

<footer>
    <strong>Author:</strong> Adarsh Dubey
</footer>

</body>
</html>
<img width="941" height="611" alt="image" src="https://github.com/user-attachments/assets/3039759d-d738-4997-9e5e-b994a7921b08" />

