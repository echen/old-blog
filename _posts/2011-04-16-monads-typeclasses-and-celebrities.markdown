---
date: '2011-04-16 03:40:23'
layout: post
slug: monads-typeclasses-and-celebrities
status: trash
title: Introduction to Monads and Typeclasses in Haskell
wordpress_id: '84'
categories:
- expository
tags:
- functional programming
- haskell
- monads
---

My favorite problems are the ones that you can turn into a mini-lesson on something new. I realized the following problem could make a nice introduction to the Maybe monad and typeclasses in Haskell, so I'm going to try lessonizing it here.


# Finding Celebrities


The problem is this: suppose you have a group of people, and you want to find a "celebrity" among them, where a celebrity is defined as a person P such that everybody else knows P, but P knows no one. (Note that, by the definition of celebrity, there can be at most one celebrity in a group.) So you're given a group of people, a black box oracle that tells you whether person X knows person Y, and you want to efficiently find a celebrity in the group (if such a celebrity exists).

The solution I came up with is the following two-step algorithm:



	
  * Step 1 finds a candidate celebrity. We keep a temporary candidate C and walk through the group: if C knows the current person P under our pointer, then C can't be a celebrity, so we change the temporary candidate to be P and move on; otherwise, if C does not know the current person P, then we keep C as our candidate and move to the next person on the list.

	
  * Step 2 checks that our candidate celebrity C is actually a celebrity. We walk through the list of people, and check that for every other person P, P knows C but C does not know P.


Let's code this up now in Haskell. Since the algorithm has two steps, let's code up each step individually.

    
    -- Step 1
    findCandidate :: [Person] -> (Person -> Person -> Bool) -> Maybe Person
    findCandidate [] _ = Nothing
    findCandidate (x:[]) _ = Just x
    findCandidate (x:y:rest) knows =
        if x `knows` y
            then findCandidate (y:rest) knows
            else findCandidate (x:rest) knows
    
    -- Step2
    checkCandidate :: [Person] -> (Person -> Person -> Bool) -> Person -> Maybe Person
    checkCandidate [] _ candidate = Just candidate
    checkCandidate (x:xs) knows candidate
        | x == candidate = checkCandidate xs knows candidate
        | otherwise      =
            if (x `knows` candidate) && (not $ candidate `knows` x)
                then checkCandidate xs knows candidate
                else Nothing


Now how do we combine the first two steps? A first approach might be the following:

    
    badFindCelebrity :: [Person] -> (Person -> Person -> Bool) -> Maybe Person
    badFindCelebrity xs knows = checkCandidate xs knows (findCandidate xs knows)


But this doesn't work! There's a _type mismatch_ in our definition: `checkCandidate` takes a `Person` in its last argument, but `findCandidate xs knows` returns something of type `Maybe Person`.

How do we fix this? One approach would be to do some checking of our candidate celebrity: if it's `Nothing`, then don't even bother passing it to `checkCandidate` and just fail immediately; otherwise, extract the person from its `Just x` wrapper, and pass this extraction to `checkCandidate`. This works as follows:

    
    messyFindCelebrity :: [Person] -> (Person -> Person -> Bool) -> Maybe Person
    messyFindCelebrity xs knows =
        case findCandidate xs knows of
            Nothing -> Nothing
            Just x  -> checkCandidate xs knows x


This isn't too bad, but what if we later want to add some additional checks? For example, instead of finding any old celebrity, we might want to find only celebrities that have recently starred in a movie, in which case we'd have to modify our algorithm to:

    
    recentMovie :: Person -> Maybe Person
    recentMovie x = ...
    
    messyFindCelebrity' :: [Person] -> (Person -> Person -> Bool) -> Maybe Person
    messyFindCelebrity' xs knows =
        case findCandidate xs knows of
            Nothing -> Nothing
            Just x 	-> case checkCandidate xs knows x of
    	    Nothing -> Nothing
    	    Just y  -> recentMovie y




# Maybe Monad


Enter the Maybe monad. Instead of forcing us to make these `Nothing` checks and `Just x` extractions ourselves, the Maybe monad has a "chaining" operator `>>=` that performs checks and extractions automatically. That is, `Nothing >>= f` is always `Nothing`, and `Just x >>= f` returns `f x`, so we can rewrite our `findCelebrity` method as:

    
    findCelebrity :: [Person] -> (Person -> Person -> Bool) -> Maybe Person
    findCelebrity xs knows =
        findCandidate xs knows >>= checkCandidate xs knows


Or, in the sugared `do` syntax:

    
    findCelebrity :: [Person] -> (Person -> Person -> Bool) -> Maybe Person
    findCelebrity xs knows = do
        candidate <- findCandidate xs knows
        celebrity <- checkCandidate xs knows candidate
        return celebrity


So that's the Maybe monad.


# Typeclasses


Now let's see if we can generalize our solution a bit. In our algorithm above, we didn't really make use of the fact that we were dealing with `Person` data types. The only assumption we made was that we could test whether two Persons were equal, in the `x == candidate` check of `checkCandidate`*. Thus, if we replace the `Person` data type in all our type signatures with a data type that supports equality testing, our function will be a bit more general and work just as well.

To do this, we write

    
    findCandidate :: (Eq a) => [a] -> (a -> a -> Bool) -> Maybe a
    checkCandidate :: (Eq a) => [a] -> (a -> a -> Bool) -> a -> Maybe a
    findCelebrity :: (Eq a) => [a] -> (a -> a -> Bool) -> Maybe a


`Eq a` simply means that `a` is a type that supports equality testing, i.e., given any two objects `x` and `y` of type `a`, writing `x == y` works. So now our `findCelebrity` function can not only find celebrities in a group of Persons, but also find things like the majority or minority in a group of integers (if we use `(<)` or `(>)` as our oracle), and sources or sinks in a graph.

*Note that we can actually get rid of this equality testing assumption, by making `findCandidate` return a list of rejected persons (in addition to the candidate celebrity) that we check against in `checkCandidate`.


# An evasive segue


So there's an introduction to the Maybe monad and typeclasses (that maybe you could have discovered yourself!). For just one more quick intro, note that the celebrity question provides a counterexample to the [Evasiveness Conjecture](http://blog.echen.me/2011/03/14/topological-combinatorics-and-the-evasiveness-conjecture) on _non-monotone_ graphs, showing why the monotonicity assumption in the conjecture is indeed necessary.
