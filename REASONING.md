# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
'(+ 1 (* 2 3))' evaluates * inner function first and then we get (+1 6) so we get 7, head is a function, 7 is an integer with no length.

## P02
'(+ 1 2)' becomes converted into a quote and we get a 3 element list, quote is a special-operator.

## P03
nil becomes just nil with value null and has legnth 0 with no operator.

## P04
t just becomes itself and is a symbol with no operator and no length.

## P05
'symbolp' function is called and evaluates if what is inside is a symbol. nil is a symbol and symbolp returns t with no length as well.

## P06
'car' function retrieves the first element of a list, and since it is handed an empty list, we get nil.

## P07
'cons' function attaches a value to the front of a passed list giving us (1,2,3) a 3-element list.

## P08
conditional function here checks (if null '()) if the empty list is null which is the same as nil that is returned so the conditional function returns t and therefore returns the first option which is symbol 'empty.

## P09
'and' evaluates from left to right, and if it isnt nil it will be true when evaluated by 'and'. It passes 1 and sees nil and immediately stops once it finds nil and returns nil. 'and' is a macro.

## P10
'progn' head is a special-operator that evaluates everything and returns the result of the last thing, '(defvar *ps3-rate* 2)' defines '*ps3-rate*' as 2, '(defun ps3-scale (n) (* n *ps3-rate*))' defines 'ps3-scale (n)' as multiplying n by '*ps3-rate*',  '(let ((*ps3-rate* 10)) (ps3-scale 3))' rebinds '*ps3-rate*' with 10 and evaluates ps3-scale(3) which gives us 3*10 and returns 30 which is an integer.

## P11
'defun' at the head is a macro that doesnt immediately evaluate and just defines what the function is, it also has a return value which is the name of the function itself, so it returns symbol 'ps3-twice'.

## P12
'labels' is a special-operator that defines a function locally instead of globally and runs the code after defining, it also allows the function to be called recursively so here in '(if (= n 0) '() (cons n (down (- n 1))))' we have an if that will return an empty list when n = 0 and since we have '(down 3)' we get a cons 3(cons 2(cons 1 '())) which should give us a (3,2,1) list with 3 elements. 

## P13
'mapcar' function evaluates both of its arguments first before running itself, so the first argument here is '#'length' which is a function that takes the length of each element, and the second argument ''((1 2) () (3))' are just lists so we get the length for each of those which is 2, 0, and 1 and then mapcar now gets those lengths and puts them into a 3 element list (2,0,1).

## P14
'mapcar' here again but this time we have the first argument which is a lambda function that multiplies n by itself, with the second argument is just a list of numbers so we square them all and get a list of (1,4,9).

## P15
'lambda' is actually a macro and just like defun it defines a function but it doesnt give it a name, and since it doesnt have a name it returns the function object which according to the grader notation should be '#<function>' which has the function type and has no length. 

## P16
The first '(let ((factor 2))' assigns 2 to factor, the second line '(let ((f (lambda (n) (* n factor))))' assigns a lambda function to f and since we see factor there, the lambda function stores that 2 assigned to factor. '(let ((factor 10))' assigns 10 to factor but this does not actually change the value of factor that is stored in the f lambda function so when (funcall f 3) is actually called we get (* 3 2) which evaluates to 6.
