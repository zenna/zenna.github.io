---
layout: post
title:  "Token Black"
date:   2014-03-31 20:30:18
categories: race academia
---

(define (geometric p)
  (if (flip p)
      0
      (+ 1 (geometric p))))

Write a probabilistic program
(define (praneeth-problem)
  (define n-cells 10)
  (define n-green 3)
  (define n-red 6)
  (define green-cells (repeat n-cells (lambda () (flip (/ n-green n-cells)))))
  (define red-cells (repeat n-cells (lambda () (flip (/ n-red n-cells)))))
  (define both (map and green-cells red-cells))
  (define n-overlap (sum (map (lambda (x) (if x 1 0) both))))
  n-overlap)

(defn sum
  [coll]
  (reduce + coll))


(defn praneeth-problem []
  (def n-cells 10)
  (def n-green 3)
  (def n-red 6)
  (def green-cells (repeatedly n-cells (fn [] (flip (/ n-green n-cells)))))
  (def red-cells (repeatedly n-cells (fn [] (flip (/ n-red n-cells)))))
  (def both (map (fn [x y] (and x y)) green-cells red-cells))
  (def n-overlap (sum (map (fn [x] (if x 1 0)) both)))
  n-overlap)
  


OK, let me try to be more clear:
There are D cells, of which n are labeled with red tag and c are labeled with green tag (randomly and independently). 
1) what is the probability of finding p double labeled cells?
2) what is the expected number of double labeled cells?

The way I ended up thinking about this was to find the PDF of number of co-labeled cells using the hypergeometric distribution and then answering both the above questions becomes trivial.

Couple of examples where n*c/D^2 doesn't work:
If there are 2 cells, one of them red and one of them green, then the probability of finding one double labeled cell is 0.5 right?

Another example: if there are 3 cells and 2 are labeled red and 1 is labeled green, then the probability of finding one double labeled cell is 1/3.

Also, max, if the probability of any given cell being double labeled is nc/D^2, and the probability of finding one double labeled cell is nc/D doesn't work because if there are 6 cells and 3 are labeled red and 3 green, then nc/D gives a number greater than 1.

Galen, the hypergeometric distribution is symmetric for swapping n and c. This is a requirement because the probability of finding colabeled cells doesn't change if I swap the red and green tags. Does this happen with the binomial distribution? The example they gave on Wikipedia seemed like the same problem I was trying to address. How would I incorporate n, c and D into the binomial distribution?

Julian, I didn't understand what small d was in your formula. Is it the number of colabeled cells?

Thanks for helping me think about this guys! Let me know your thoughts.






