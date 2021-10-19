# Flow-Pathing

**Using topography data to predict the flow of water.**

<p float="center">
  <img src="elvpic.PNG" width="50%" />
  <img src="flacc.gif" width="50%" />
  <br>
    <em> Delaware County PA elevation data and the resulting flow accumulation map derived from it. </em>
 </p>
 
 This project is actually from my software engineering course. However, I was entirely responsible for design and implementation of the flow algorithm, as well as 100% of the code in this repository. 
 
 I had wanted to work on topography data analysis, as it's similar to the data processing one would do for asteroid analysis, and proposed a flood prediction tool for a group project in a course to justify this project. The flow algorithm takes an input 2D array of elevation data and iteratively constructs the flow accumulation at every coordinate in the array. 
 
 The actual algorithm first determines which cardinal direction water will flow in, or if it will pool, using numpy's gradient calculator. Then at each iteration, we add the flow accumulation at one cell to the adjacent cell that it would flow into. However, this accumulation is conservatively added such that each unit of flow accumulation corresponds to an origin cell. Thus, over many iterations, we can even predict the accumulation at a cell with input flows from many thousands of other cells. 
 
 Due to the requirement of having to handle large array sizes and many iterations, a serial program is simply too slow. Even 100 iterations of the flow algorithm took nearly an hour (albeit on a power saving laptop on an amtrak). Thankfully CuPy enables us to write full CUDA kernels within the python script, and as this problem is quite scalable, we gain an immense speedup by using gpu parallelization, to the point where 1000 iterations takes less time than calculating the flow direction map with gradients and loading data into memory. 
