---
date: '2011-03-14 04:28:39'
layout: post
slug: prime-numbers-and-the-riemann-zeta-function
status: publish
title: Prime Numbers and the Riemann Zeta Function
wordpress_id: '59'
categories:
- expository
tags:
- fourier analysis
- mathematics
- number theory
- prime numbers
- riemann zeta function
---

Lots of people know that the [Riemann Hypothesis](http://en.wikipedia.org/wiki/Riemann_hypothesis) has _something_ to do with prime numbers, but most introductions fail to say what or why. I'll try to give one angle of explanation.





# Layman's Terms





Suppose you have a bunch of friends, each with an instrument that plays at a frequency equal to the imaginary part of a zero of the Riemann zeta function. If the Riemann Hypothesis holds, you can create a song that sounds exactly at the prime-powered beats, by simply telling all your friends to play at the same volume.





# Mathematical Terms





Let $latex \pi(x) $ denote the number of primes less than or equal to x. Recall [Gauss's approximation](http://en.wikipedia.org/wiki/Prime_number_theorem#The_prime-counting_function_in_terms_of_the_logarithmic_integral): $latex \pi(x) \approx \int _ 2 ^ x \frac{1}{\log t} \,dt $ (aka, the "probability that a number n is prime" is approximately $latex \frac{1}{\log n} $).





Riemann improved on Gauss's approximation by discovering an _exact_ formula $latex P(x) = A(x) - E(x) $ for counting the primes, where







  * $latex P(x) = \sum _ {p ^ k < x} \frac{1}{k} $ performs a weighted count of the prime powers less than or equal to x. [Think of this as a generalization of the prime counting function.]


  * $latex A(x) = \int _ 0 ^ x \frac{1}{\log t} \,dt+ \int _ x ^ {\infty} \frac{1}{t(t ^ 2  -1) \log t} \,dt $ $latex - \log 2 $ is a kind of generalization of Gauss's approximation.


  * $latex E(x) = \sum _ {z : \zeta(z) = 0} \int _ 0 ^ {x ^ z} \frac{1}{\log t} \,dt $ is an error-correcting factor that depends on the zeroes of the Riemann zeta function.






In other words, if we use a simple Gauss-like approximation to the distribution of the primes, the zeroes of the Riemann zeta function sweep up after our errors.





Let's dig a little deeper. Instead of using Riemann's formula, I'm going to use an equivalent version





$latex \psi(x) = (x + \sum _ {n = 1} ^ {\infty} \frac{x ^ {-2n}}{2n} - \log 2\pi) - \sum _ {z : \zeta(z) = 0} \frac{x ^ z}{z} $





where  $latex \psi(x) = \sum _ {p ^ k \le x} \log p $. Envisioning this formula to be in the same $latex P(x) = A(x) - E(x)$ form as above, this time where







  * $latex P(x) = \psi(x) = \sum _ {p ^ k \le x} \log p $ is another kind of count of the primes.


  * $latex A(x) = x + \sum _ {n = 1} ^ {\infty} \frac{x ^ {-2n}}{2n} - \log 2\pi $ is another kind of approximation to $latex P(x)$.


  * $latex E(x) = \sum _ {z : \zeta(z) = 0} \frac{x ^ z}{z} $ is another error-correction factor that depends on the zeroes of the Riemann zeta function.






we can again interpret it as an error-correcting formula for counting the primes.





Now since $latex \psi(x) $ is a step function that jumps at the prime powers, its derivative $latex \psi'(x) $ has spikes at the prime powers and is zero everywhere else. So consider





$latex \psi'(x) = 1 - \frac{1}{x(x ^ 2 - 1)} - \sum _ z x ^ {z-1} $





It's well-known that the zeroes of the Riemann zeta function are symmetric about the real axis, so the (non-trivial) zeroes come in conjugate pairs $latex z, \bar{z} $. But $latex x ^ {z-1} + x ^ {\bar{z} - 1} $ is just a wave whose amplitude depends on the real part of z and whose frequency depends on the imaginary part (i.e., if $latex z = a + bi $, then $latex x ^ {z-1} + x ^ {\bar{z}-1} = 2x ^ {a-1} cos (b \log x) $), which means $latex \psi'(x) $ can be decomposed into a sum of zeta-zero waves. Note that because of the $latex 2x ^ {a-1}$ term in front, the amplitude of these waves depends only on the real part $latex a$ of the conjugate zeroes.





For example, here are plots of $latex \psi'(x) $ using 10, 50, and 200 pairs of zeroes:





[![10 Pairs](http://dl.dropbox.com/u/10506/blog/riemann-hypothesis/10.png)](http://dl.dropbox.com/u/10506/blog/riemann-hypothesis/10.png)





[![50 Pairs](http://dl.dropbox.com/u/10506/blog/riemann-hypothesis/50.png)](http://dl.dropbox.com/u/10506/blog/riemann-hypothesis/50.png)





[![50 Pairs](http://dl.dropbox.com/u/10506/blog/riemann-hypothesis/200.png)](http://dl.dropbox.com/u/10506/blog/riemann-hypothesis/200.png)





So when the Riemann Hypothesis says that all the non-trivial zeroes have real part 1/2, it's hypothesizing that the non-trivial zeta-zero waves have equal amplitude, i.e., they make equal contributions to counting the primes.





**In Fourier-poetic terms**, when Flying Spaghetti Monster composed the music of the primes, he built the notes out of the zeroes of the Riemann zeta function. If the Riemann Hypothesis holds, he made all the non-trivial notes equally loud.
