# Thinking Machines Data Engineering Exam Solution

By: John Clinton Buzon

## Part 1: Algorithmic thinking

### Brute force approach

`brute_force_approach()` : We brute force the formula by passing multiple values of `|a| < 1000` and `|b| <= 1000` using a brute force `is_prime(n)` function. 

### Improvement 1 - using SieveOfEratosthenes

`brute_force_approach_with_improvement_1()` : We improve the brute force approach with improvement on prime number checking. Instead of calculating if each provided number is prime or not, it checks from a list of one time pre-generated prime numbers (generated by `SieveOfEratosthenes(n)`). This significantly reduces overall computation.

### Improvement 2 - reducing values of potential parameters for `a` and `b`

`brute_force_approach_with_improvement_2()` : We improve the brute force approach with SieveOfEratosthenes improvement by reducing values of potential parameters for `a` and `b`. 

- If `a` and `b` are both negative, they generate a nagative number. Since negative numbers cannot be prime numbers, we ignore them.
- If `a` and `b` are both even numbers, they generate a maximum of 2 consecutive prime numbers. Since the objective of this exam is to find the maximum consecutive prime numbers, we can ignore the results of 2.

By applying the following reductions, we reduce the number of iterations we check.

### Improvement 3 - parallelization

`brute_force_approach_with_improvement_3()` : We improve the approach by parallization. Using a modified version of `brute_force_approach_with_improvement_2()` as `worker(a_range)`, we can now process the same problem in parallel by passing different range values for `a` on multiple workers. In this case we create 4 workers processing the following combinations

- Worker 1: where `a` range(-1000,-500)
- Worker 2: where `a` range(-500,0)
- Worker 3: where `a` range(0,500)
- Worker 4: where `a` range(500,1000)

Once all the workers are complete, we then scan for the output of the 4 workers and get the one which got the highest answer.

### Improvement 4 - using a faster `is_prime` function

`brute_force_approach_with_improvement_4()` : Using `brute_force_approach_with_improvement_3()` we modify the code to use `is_prime_v2(n)` instead of SieveOfEratosthenes approach. Instead of scanning through range(1,n+1) each time we check if a number is prime, we iterate from 2 to sqrt(N) to find all the factors of n. This approach combines improvement 2 and 3 and is the fastest when tested.

### Notes

- Executed using Python 3.7.3
- Sample output can be found in the repository
