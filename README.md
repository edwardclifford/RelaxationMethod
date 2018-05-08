# RelaxationMethod

Problem #2
Our current implementation of the relaxation method is quite crude in that we must specify the number of iterations that it performs, and then simply look at the output to see if we have converged to a fix-point. It would instead be better if we could have our algorithm check its own numbers to see if they are converging to a single value, and then terminate itself if it has converged.
We can measure how close our most recent guess is to a fixed-point by looking at our most-recent three guesses xn−2,xn−1,xnxn−2,xn−1,xn , and seeing if xn−1xn−1 and xnxn are closer to one another than are xn−1xn−1 and xn−2xn−2. Skipping a formal derivation, the following formula gives an upper-bound estimate on how close xnxn is to a true fixed-point:
ϵn=∣(xn−xn−1)22xn−1−xn−2−xn∣
ϵn=∣(xn−xn−1)22xn−1−xn−2−xn∣
That is, if your previous three guesses were 1.01.0, then 1.631.63, and then 1.801.80, plugging these into the preceding formula produces an error bound of ϵ=0.06ϵ=0.06. This means that the guess 1.801.80 is within 0.060.06 of the true fixed-point. To prevent division-by-zero errors, if your denominator is equal to 0.0, replace it with the value 1e-14.
Armed with this formula, we can now write a much better algorithm, which can operate based on a tolerance rather than a strict number of iterations.
Write a second version of the relaxation-method. This function should accept four arguments:
a python function, which accepts a number as an input, and returns a float as an output
an initial guess for the fixed-point, x0x0, a floating-point number
a tolerance value, a positive-valued floating-point number
a max number of iterations that your algorithm is permitted to run
Your algorithm should produce guesses until ϵnϵn is smaller than the specified tolerance value, or until the number of guesses produced (including the initial guess) matches/exceeds the max number of iterations. Like the last function, it should return a list of all the guesses. You will need to have three guesses before you can assess the tolerance.

def relaxation_method2(func, xo, tol, max_it):
    """ Performs the relaxation method to find a fixed-point for `func`,
        given the initial guess `xo`. The relaxation process is carried out for
        `num_it` steps.
        
        Parameters
        ----------
        func : Callable[[float], float]
            The function whose fixed point is being found.
        xo : float
            The initial "guess" value.
        tol : float
            A positive value that sets the maximum permissable error
            in the final fixed-point estimate.
        max_it : int
            The maximum number relaxation-guesses (i.e. the length of the
            list you are creating) allotted before the 
            algorithm will end. The length of the list you return should
            never exceed this number.
            
        Returns
        -------
        List[float]
            A list of the initial guess, and all of the subsequent guesses generated
            by the relaxation method. """
    # student code goes here

