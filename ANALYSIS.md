# Environments and the Toy Evaluator

Which line captures the defining environment, and what is in that environment at the moment it's captured?

    (make-closure (second expr) (third expr) env) is the line that captures the environment when (eql (car expr) 'lambda) is true. What is in env at the moment it is captured is the bindings that were active at the time that is passed into eval-expr.

What would the scope-discrimination case return if apply-closure extended the caller's environment instead, and what would that make the language?

    Assuming this is talking about the case that separates a correct E4 from a plausible one, if apply-closure extended the caller's environment, we would setting the value of x to 100 in line (let ((x 100)) after the x value of 2 was already taken from when the function was defined, thus giving us a result of 101 instead of 3. The lambda would then be reading x from wherever it is called, not from where it was written, so the value 2 captured at definition time would be ignored. This would make the language dynamically scoped instead of lexically scoped, because free variables in a function body would be looked up at call time, and a closure would no longer hold on to the environment it was created in.

Why does the host CLISP need funcall where the toy language doesn't?

    CLISP needs funcall because it keeps variables and functions in two separate places. When CLISP sees (f 1), it looks for f among the variables and finds no function there, so nothing gets called. Writing (funcall f 1) tells it to look among the functions instead, which is why the host also uses #' when handing a named function to mapcar. Our toy language has only one place, so a variable can hold a function and (f 1) just works without funcall, and apply-closure can simply evaluate the head to get the function.