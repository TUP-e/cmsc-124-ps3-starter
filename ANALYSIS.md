# Environments and the Toy Evaluator

Which line captures the defining environment, and what is in that environment at the moment it's captured?

    (make-closure (second expr) (third expr) env) is the line that captures the environment when (eql (car expr) 'lambda) is true. What is in env at the moment it is captured is the bindings that were active at the time that is passed into eval-expr.

What would the scope-discrimination case return if apply-closure extended the caller's environment instead, and what would that make the language?

    Assuming this is talking about the case that separates a correct E4 from a plausible one, if apply-closure extended the caller's environment, we would setting the value of x to 100 in line (let ((x 100)) after the x value of 2 was already taken from when the function was defined, thus giving us a result of 101 instead of 3. This would make the language dynamically scoped instead of lexically scoped.
