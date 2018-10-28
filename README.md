# lisp-interpreter
A lisp interpreter (or: the maxwell’s equations of software)

Based on:
- [Recursive Functions of Symbolic Expressions and Their Computation by Machine, Part I](http://www-formal.stanford.edu/jmc/recursive.pdf) by John McCarthy
- [The Roots of Lisp](http://languagelog.ldc.upenn.edu/myl/llog/jmc.pdf) by Paul Graham
- [The Dawn of Lisp, or: How to Write Eval and Apply in Clojure](https://github.com/ariel-ortiz/the-dawn-of-lisp) by 
Ariel Ortiz.

## Operators

1. `(􏰏quote x􏰐)`: returns x.
```
> (quote a)
a
```

2. `(atom x)`: returns the atom `t` if the value of `x` is an atom or the empty list􏰅
```
> (atom 'a)
t
```
􏰋􏰏􏰐􏰐
3. `(eq x y)`: returns `t` if `x` and `y` are the same atom or both the empty list
```
> (eq 'x 'x)
t
```

4. `(car x)`: returns first element (head)
```
> (car '(a b c))
a
```

5. `(cdr x)`: returns all elements except the first one (tail)
```
> (cdr '(a b c))
(b c)
```

6. `(cons x y)`: returns a list containing the value of `x` followed by the elements of the value of `y`􏰅
```
> (cons 'a '(b c))
(a b c)
```

7. `(cond (p_1 e_1) (p_2 e_2) ... (p_n e_n))`: `p` expressions are evaluated in order until one returns `t`􏰅.
When one `t` is found􏰀 the value of the corresponding `e` expression is returned as the expression.
```
> (cond ((eq 'a 'b) 'first)
      ((atom 'a) 'second))
'second
```

8. Function `(lambda (p_1 ... p_n) e)`, where `p_1 ... p_n` are atoms (parameters), and `e` is an expression.
A function call is an expression with the first element as:
```
((lambda (p1 ... pn) e) a_1 ... a_n)
```

Each expression `a_i` is evaluated, then `e` is evaluated, and while `e` is
evaluated, the value of any occurrence of one of the `p_i` is the value of the
corresponding `a_i` in the most recent function call.

Example:

```
> ((lambda (x) (cons x '(b))) 'a)
(a b)

> ((lambda (x y) (cons x (cdr y)))
   'z
   '(a b c))
(z b c)
```

Parameters can be used as operators in expressions as well as arguments:
```
> ((lambda (f) (f '(b c)))
   '(lambda (x) (cons 'a x)))
(a b c)
```

In ruby:
```
a = lambda {|func| func.call([2, 3]) }
b = lambda {|arg| [1] + arg }

a.call(b)
=> [1, 2, 3]
```

(...)
