# Final Project Assignment 2: Explore One More! (FP2) 
DUE March 30, 2015 Monday (2015-03-30)

This is just like FP1, but where you do a different library. (Full description of FP1 is [on Piazza.][piazza])

During this assignment, you should start looking for teammates. See the project schedule [on Piazza.][schedule]

Write your report right in this file. Instructions are below. You can delete them if you like, or just leave them at the bottom.
You are allowed to change/delete anything in this file to make it into your report. It will be public.

This file is formatted with the [**markdown** language][markdown], so take a glance at how that works.

This file IS your report for the assignment, including code and your story.

Code is super easy in markdown, which you can easily do inline `(require net/url)` or do in whole blocks:
```
#lang racket

(require net/url)
```

### My Library: plot library
Write what you did!
Remember that this report must include:
 
 I started off looking at a few different libraries like games, game/board, cards, and web-server but I really liked plot so I decided to stick with that. In the program I tested the code provided and looked at how plot works and what a function, in plot, is. Plot is a very nice racket function that I learned can take a list of mathematical functions or a list of lists including axis and functions. For each plot you can control what the axis say, what the title says, the style of the plot, and the color of each function. In my code there are plots of 2D and 3D functions that show how plot behaves. Racket has a large color database and you can either reference a color with one number, a combination of RGB numbers, or by its direct symbolic name. Also when plotting multiple functions you can use function-interval to shade in the space inbetween two functions to see what that looks like on a graph. Overall, I really like plot library's ease of use and well documented code 
 
* a narrative of what you did
* the code that you wrote
* output from your code demonstrating what it produced
* any diagrams or figures explaining your work 

```
#lang racket
;;Started looking at the game library and the card libraries.
;(require games)
;(require games/cards)

;(require games/gl-board-game)

;(define x  (make-table "The board" 5 5))

;(define y (make-deck))
;(send x show #t)

;;Decided that I would try another library and see if there was something I didn't know that looked interesting.

;;Looked into the Web server Library.

;#lang web-server/insta
; (require web-server/servlet-env)

;(define (start req)
;  (response/xexpr
;   `(html (head (title "Hello world!"))
;         (body (p "Hey out there!")))))

;(no-web-browser)

;(require web-server/servlet
;         web-server/servlet-env)
 
;(require web-server/servlet/servlet-structs)

;(define (my-app req)
;  (response/xexpr
;   `(html (head (title "Hello world!"))
;          (body (p "Testing! Testing! 1! 2! 3! Can you read me loud and clear?")))))
 
;(serve/servlet my-app  #:port 8080
;               #:listen-ip #f
;               #:servlet-path "/OPLProject.rkt"
;               #:servlet-regexp #rx"" #:extra-files-paths
;               (list
;                (build-path "/Users/family/Desktop"))
              ; #:command-line? #t
;               )

;(send/back
; (response/xexpr
;  `(html
;    (body
;     (h1 "The sum is: "
;         ,(+ 1
;             2))))))

;(send/suspend
; (lambda (k-url)
;   (response/xexpr
;    `(html (head (title "Enter a number"))
;           (body
;            (form ([action ,k-url])
;                  "Enter a number: "
;                  (input ([name "number"]))
;                  (input ([type "submit"]))))))))

;;Tried out some code to see if I understood what was happening and decided that besides seeing the actual url created
;;and displayed in my web browser I didn't know the difference between the different parameters of serve/servlet/

;;Thus I decided to look into the plot library because I know plottting.

(require plot)

;plots a basic sin wave.
(plot (function sin (- pi) pi #:label "y = sin(x)"))

;plots a 3D function
(plot3d (surface3d (λ (x y) (* (cos x) (sin y)))
                     (- pi) pi (- pi) pi)
          #:title "3D Chart"
          #:x-label "x" #:y-label "y" #:z-label "cos(x) sin(y)")

;plots a 3D graph with different colored intervals along the z axis that show what range a value is in.
 (parameterize ([plot-title  "Colored 3D function"]
                 [plot-x-label "x"]
                 [plot-y-label "y"]
                 [plot-z-label "cos(x) sin(y)"])
    (plot3d (contour-intervals3d (λ (x y) (* (cos x) (sin y)))
                                 (- pi) pi (- pi) pi)))

;Shows that you can plot multiple functions if you put them in a list.
(plot (list (axes)
              (function sqr -2 2)
              (function (λ (x) x) #:color 0 #:style 'dot)
              (inverse sqr -2 2 #:color 3)))

;plot accepts a list containing a list of axis and functions.
;Aka plot can handle lists of lists O_O awesome.
(plot (list (axes)
              (function sqr -2 2 #:label "y = x^2")
              (function (λ (x) x) #:label "y = x" #:color 0 #:style 'dot)
              (inverse sqr -2 2 #:label "x = y^2" #:color 3)
              (function (λ (x)(* x x x)) #:label "y = x^3" #:color 100)))

;function-interval colors the interval between two functions. That colors of the two functions and
;the intervel inbetween them can be altered. :)
(plot (list (function-interval (λ (x) (- (sin x) 5))
                                 (λ (x) (+ (sin x) 5)) #:color 10
                                 #:line1-color 1 #:line2-color 1)
            (function-interval (λ (x) (- (cos x) 5))
                                 (λ (x) (+ (cos x) 5)))
              (function-interval (λ (x) (- (sqr x))) sqr #:color 4
                                 #:line1-color 4 #:line2-color 4))
        #:x-min (- pi) #:x-max pi)


;Plots a sphere that is hollow and is green.
(plot3d (polar3d (λ (θ ρ) 1) #:color 2 #:line-style 'transparent)
          #:altitude 25)

;plots three circles that are restricted and only drawn at the radius of 0.8.
(plot3d (list (polar3d (λ (θ ρ) 1)  #:label "This is the oracle!" #:color -5 #:line-style 'transparent)
        (polar3d (λ (θ ρ) .8) #:color 15 #:line-style 'transparent)
        (polar3d (λ (θ ρ) .9) #:color 5 #:line-style 'transparent))
          #:x-min -0.8 #:x-max 0.8
          #:y-min -0.8 #:y-max 0.8
          #:z-min -0.8 #:z-max 0.8
          #:altitude 25)

;functions have a first come first serve with preference when ploting them.
(define ((dist cx cy cz) x y z)
  (sqrt (+ (sqr (- x cx)) (sqr (- y cy)) (sqr (- z cz)))))
(plot3d (list (isosurface3d (dist  1/4 -1/4 -1/4) 0.995
                            #:color 4 #:alpha 0.8 #:samples 21)
              (isosurface3d (dist -1/4  1/4  1/4) 0.995
                            #:color 6 #:alpha 0.8 #:samples 21))
        #:x-min -1 #:x-max 1
        #:y-min -1 #:y-max 1
        #:z-min -1 #:z-max 1
        #:altitude 25)

;can use plot-file to send image of plot to a file
;(plot-file (function...) pathoffile typeoffilelike'png)

;shows the different colors that lines can be.
(parameterize ([interval-line1-width  3]
                 [interval-line2-width  3])
    (plot (for/list ([i  (in-range -7 13)])
            (function-interval
             (λ (x) (* i 1.3)) (λ (x) (+ 1 (* i 1.3)))
             #:color i #:line1-color i #:line2-color i))
          #:x-min -8 #:x-max 8))

;if you want to use colors for a black and white print only.
;also shows cool styles.
(parameterize ([line-color  "black"]
                 [interval-color  "black"]
                 [interval-line1-color  "black"]
                 [interval-line2-color  "black"]
                 [interval-line1-width  3]
                 [interval-line2-width  3])
    (plot (for/list ([i  (in-range 7)])
            (function-interval
             (λ (x) (* i 1.5)) (λ (x) (+ 1 (* i 1.5)))
             #:style i #:line1-style i #:line2-style i))
          #:x-min -8 #:x-max 8))
```
* Output from the code
It displays each of the plots in the code. The 3D plots can be turned in different angles and the 2D plots can be zoomed in on.

I included the diagrams in the comment


### How to Do and Submit this assignment

1. To start, [**fork** this repository][forking].
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning)
  3. (You may need to clone and push if you want to add extra files)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[schedule]: https://piazza.com/class/i55is8xqqwhmr?cid=453
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request

