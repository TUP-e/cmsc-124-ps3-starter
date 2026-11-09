# REASONING

## P01

`(+ 1 (* 2 3))` has `+` as its head, a function, so both operands run first.
The inner `(* 2 3)` returns 6, then `(+ 1 6)` returns 7. That is an integer,
so length is `none` and the head is a function.

## P02

`''(+ 1 2)` has `quote` as its head. The outer quote returns the inner form
`(quote (+ 1 2))` untouched. That list has two elements: `quote` and `(+ 1 2)`.
So it is a cons of length 2, and the head is a special operator.

## P03

`'nil` has `quote` as its head, which returns `nil` untouched. `nil` is the
empty list, so kind is `null` and length is 0. The head is a special operator.

## P04

`'t` has `quote` as its head, which returns the symbol `t` untouched. That is a
symbol, not a sequence, so length is `none`. The head is a special operator.

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

`(defun ps3-twice (n) (* n 2))` has `defun` as its head. The standard calls
`defun` a macro, so I expect the head to be a macro. It returns the symbol
`ps3-twice`, so length is `none`.

I predicted the operator was `macro` and CLISP printed `special-operator`. I
knew the standard calls `defun` a macro, but CLISP answers `special-operator`
under the special-operator-first rule. The value, kind, and length I got right.

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