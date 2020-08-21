# Notes
[lecture](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/video-lectures/1a-overview-and-introduction-to-lisp/)


- Implications of rules of procedures/processes help to formalize imperative knowledge.
- It helps to build very large systems, systems large enough that you can't hold the entire program in your head.
- There are techniques for controlling complexity, which is what this course (and CS) is really about.
- When building a large system, very little difference between what I want and what I can imagine.
- some of these tools are:
    - black box abstraction (hide all implementation/internal details)
        - Primitive objects (data, procedures)
        - Means of combination (proc composition, compound data)
        - Means of abstraction (proc definition, simple data abstraction)
        - Capturing common patterns (high-order procs, data as procs)
    - conventional interfaces
        - agreed-upon ways of plugging things together
        - generic operations (allowing ability to work with all kinds of data, functions)
        - large scale structure and modularity
        - object-oriented programming (TRUE oop, with discrete components communicated by immutable messages)
        - operations on aggregates (thinking in terms of streams)
    - Metalinguistic Abstraction (making new languages)
        - controlling complexity of a system is sometimes easier to express as a new language
- How to think about languages:
    - primitive elements
        - Examples: 3, +, 17.4, etc
    - means of combination (putting primitives together)
        - Examples: `(+ 3 17.4)`
        - Interesting side note, lisp's basically manage all data as ASTs, and the parenthesis are there to convert "standard" trees into _linear_ trees
    - means of abstraction
- You do not make arbitrary distinctions in Lisp between things that happen to be primitive in the language and things that happen to be built-in.
    - things you construct get all the power and functionality as if they were primitive (basics of abstraction wrapper)

#### Example of computing square root from lecture
```scheme
(define (sqrt x)
    (try 1 x))

(define (try guess x)
    (if (good-enough? guess x)
        guess
        (try (improve guess x) x)))

(define (good-enough? guess x)
    (< (abs (- (square guess) x))
        .001))

(define (improve guess x)
    (average guess (/ x guess)))

(define (average x y)
    (/ (+ x y) 2))
```

Alternatively, we can encapsulate the entire thing under the `sqrt` proc for "block structure"
(Note that all the functions under `sqrt` have been reduced to arity 1, and are functioning via closures):
```scheme
(define (sqrt x)
    (define (average x y)
        (/ (+ x y) 2))

    (define (improve guess)
        (average guess (/ x guess)))
    
    (define (good-enough? guess)
        (< (abs (- (square guess) x))
            .001))

    (define (try guess)
        (if (good-enough? guess)
            guess
            (try (improve guess))))

    (try 1))
```