## map,filter and arrow fns

- map and filter are helper functions for arrays
- arrow fns are another way to write functions in js.
- in arrow fns and normal fns there is a difference in how `this` gets binded in the function scope.

- think of them as utilities to transform an iterable into another iterable , by doing some mathematical transformations.

- a function can take another function as input in js, what if the the transformation that we want, we define in a function and `apply` to each element of the array, without explicitly iterating.
