# Type-Batched-Joint-Reducer
Type batched probabilistic joint reducer is a language agnostic tool for efficient program reduction. Given a program with a property of interest such as a C program that causes the GCC compiler to crash, type batched probabilistic joint reducer generates a smaller version of the program that is easier to comprehend and still preserves the property.

Our reducer works by selecting the most advantageous set of nodes from the parse tree of the program being reduced using machine learning temporal models at different points in time during reduction. These advantageous nodes are selected based on the probability of removal success for their grammar rule type at a given point in time. For example, declarations of variables in a C program have low probability of removal success at the beginning of reduction when their uses are still present. This is because removing declarations before their uses generates compile time issues. As reduction proceeds further and more uses get removed, the probability of removal success for declarations may increase. Our mechanism of selecting nodes with the highest probability of removal success, called type scheduling, is dynamic and takes into account these time-varying changes. 

Moreover, by selecting nodes with high probability of removal success, we increase the chance of removing nodes overall. This brings in the potential of removing multiple nodes at the same time using a probabilistic joint reducer. This joint reducer tries to build chunks of nodes from the set of advantageous nodes to remove. Each failing removal helps our joint reducer to learn about the nodes in the chunk and build a better chunk that is more likely to be removable next. 

# How to build
Install the following dependencies:

        cmake version >= 3.2 
        llvm version >= 9
        mlpack version >= 3
        OpenMp version >= 4
        Boost version >= 1.71
        
Make a directory separate from type-batched-joint-reduction directory. You can name this directory build. Then run the following:

        cd build
        cmake -DLLVM_DIR=/path/to/llvmDir/lib/cmake/llvm /path/to/type-batched-joint-reduction
        
# How to run
