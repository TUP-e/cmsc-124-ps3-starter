# REASONING

## P01

`(+ 1 (* 2 3))` has `+` as its head, a function, so both operands run first.
The inner `(* 2 3)` returns 6, then `(+ 1 6)` returns 7. That is an integer,
so length is `none` and the head is a function.

## P02

`''(+ 1 2)` — the corpus's outer quote stores the form, so what `./run`
evaluates is `(quote (+ 1 2))`. Its head is `quote`, a special operator, which
returns its argument `(+ 1 2)`. That is a three-element list, so kind is `cons`,
length is 3, and the head is a special operator.

I predicted the value `(quote,(+,1,2))` with length 2 and CLISP printed
`(+,1,2)` with length 3. I read the inner quote as if it survived evaluation.
The rule I misread: the corpus's outer quote is consumed at load time, so
`./run` evaluates `(quote (+ 1 2))`, whose value is the three-element list
`(+ 1 2)`.

## P03

`'nil` — the corpus's quote stores the atom `nil`, so `./run` evaluates `nil`
itself. It returns `nil`, the empty list: kind `null`, length 0. The form is an
atom, so it has no head and operator is `none`.

I predicted the operator was `special-operator` and CLISP printed `none`. I
treated the corpus's storage quote as the head of the form being evaluated. The
rule I misread: the corpus quote is consumed at load time, so `./run` sees the
atom `nil`, which has no head.

## P04

`'t` — the corpus's quote stores the atom `t`, so `./run` evaluates `t` itself.
It returns the symbol `t`, not a sequence, so kind is `symbol` and length is
`none`. The form is an atom, so operator is `none`.

I predicted the operator was `special-operator` and CLISP printed `none`. I
treated the corpus's storage quote as the head of the form being evaluated. The
rule I misread: the corpus quote is consumed at load time, so `./run` sees the
atom `t`, which has no head.

## P05

`(symbolp nil)` has `symbolp` as its head, a function, so `nil` runs first.
`symbolp` returns `t` because `nil` is a symbol. That result is a symbol, so
length is `none` and the head is a function.

## P06

`(car '())` has `car` as its head, a function. The quote hands it the empty
list, and `car` of `nil` returns `nil`. That is `null` with length 0, and the
head is a function.

## P07

`(cons 1 '(2 3))` has `cons` as its head, a function. It puts 1 on the front of
`(2 3)` and returns `(1 2 3)`. That is a cons of length 3, and the head is a
function.

## P08

`(if (null '()) 'empty 'full)` has `if` as its head, a special operator. The
condition `(null '())` is true, so `if` returns `'empty` and skips `'full`. That
is the symbol `empty`, length `none`, and the head is a special operator.

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