# "MiniKanren", Byrd and Friedman #

## The Language ##
* `(symbolo x)`: if I ever get a value, it'll be a symbol
* `(numbero x)`: it'll be a number
* `(noo x)`: it'll be a number
* `(run n (x) (...)))`: evaluates and returns `n` solutions for `x`
* `(fresh (...))`: fresh variables
* `_`: I don't know what I'll ever be
* `(conde [...] [...])`
* `(run* ...)`: evaluates and returns all solutions
* `(define rember
    (fn (x l)
        (cond
            [(null? l) `()]
            [(eq? (car l) x) (cdr l)]
            [else (cons (car l) (rember x (cdr l)))])))`
  * `(rember 'b '(a b c))` -> `(a c)`
* But we want more answers...
* `(define rembero
    (fn (x l out)
        (conde
            [(== '() l) (== `() out)]
            [(fresh (d)
                (== `(,x . ,d) l)
                (== d out))]
            [(fresh (a d res)
                (== `(,a . ,d) l)
                (=/= a x)
                (rembero x d res)
                (== `(,a . ,res) out)]`
* `(run 2 (q) (rembero 'b '(a b c) q))` -> `((a c))`
* Now lets run in backwards...
* `(run* (q) (rembero 'b q '(a b c)))` -> `((b a b c) (a b b c)`
* ...now I'm lost...
















