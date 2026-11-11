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

Edit: operator is a function, I wrote none.

## P07
'cons' function attaches a value to the front of a passed list giving us (1,2,3) a 3-element list.

## P08
conditional function here checks (if null '()) if the empty list is null which is the same as nil that is returned so the conditional function returns t and therefore returns the first option which is symbol 'empty.

Edit: it is actually a special-operator.

## P09

`(and 1 nil 3)` has `and` as its head. Chapter 7 teaches `and` as a macro, so I
expect the head to be a macro. It stops at `nil` and returns `nil`. That is
`null` with length 0.

I predicted the operator was `macro` and CLISP printed `special-operator`. I
read Chapter 7's description of `and` as a macro and did not account for the
course rule that asks about special operators first. The value, kind, and
length I got right.

## P10

`(progn ...)` has `progn` as its head, a special operator. `defvar` makes
`*ps3-rate*` special, bound to 2. The `let` rebinds it to 10, and because it is
special, `ps3-scale` sees 10 and returns `3 * 10 = 30`. That is an integer,
length `none`, and the head is a special operator.

## P11

`(defun ps3-twice (n) (* n 2))` has `defun` as its head. `defun` is a macro in
the standard, and unlike `and`, `labels`, and `progn`, CLISP keeps that
classification. Its value is the symbol being defined, `ps3-twice`, so kind is
`symbol` and length is `none`. The head is a macro.

I predicted the operator was `special-operator` and CLISP printed `macro`. I
applied the special-operator-first rule to `defun` without checking CLISP's
actual classification. The rule I misread: `defun` is a macro in CLISP, not a
special operator.

## P12

`(labels ((down (n) ...)) (down 3))` has `labels` as its head. I read `labels`
as an ordinary function taking local definitions, so the head would be a
function. It returns `(3 2 1)`, a cons of length 3.

I predicted the operator was `function` and CLISP printed `special-operator`. I
read `labels` as an ordinary function taking local definitions; it is a special
operator. The value, kind, and length I got right.

## P13

`(mapcar #'length '((1 2) () (3)))` has `mapcar` as its head, a function. It
takes the length of each element: 2, 0, 1. The result is `(2 0 1)`, a cons of
length 3, and the head is a function.

## P14

`(mapcar (lambda (n) (* n n)) '(1 2 3))` has `mapcar` as its head, a function.
It squares each element: 1, 4, 9. The result is `(1 4 9)`, a cons of length 3,
and the head is a function.

## P15

`(lambda (n) (* n 2))` has `lambda` as its head, a macro. Evaluating it returns
a function object, written `#<function>`. That is a function, so length is
`none`, and the head is a macro.

## P16
`(let ((factor 2)) ...)` has `let` as its head, a special operator. The lambda
captures `factor = 2` when it is created. The later `let` binds a different
`factor` to 10, but the lambda never sees it, so `(funcall f 3)` returns
`3 * 2 = 6`. That is an integer, length `none`, and the head is a special
operator.