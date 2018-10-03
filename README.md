# dcswapgame
Dragon City Swap Game Optimizer

A simple program / library to optimize the moves to take in dragon city's puzzle island / fruit island (bejeweled/candy crush/match-3).

Requirements
------------
Python3 - it will probably work with python2 as well, but I haven't tried

colorama [optional] - for a better display on the terminal

ipython [optonal] - it will work without, but it'll be a mess

Usage
-----

There is no user interface, not even a command line interface.

There are some functions that can be called in a python repl to use it interactively. This is an example session:

    import swapgame
    # create a shortcut, this will be used a lot
    f = lambda s: swapgame.fruitisland(s)[0][1]
    
    # this function defines your preferences as to which tiles to remove
    def evaluate(X, removed, moves):
        counts = {}
        for r in removed:
            counts[r.color] = counts.get(r.color, 0)+1
        return (counts.get(2,0) + counts.get(6,0) / 2 - len(moves) / 3,
        len(removed))
    
    ### repeat the following for each step
    # create the board from game data
    B = f(' ... data from game ... ')
    
    # evaluate possible moves, ordering in accordance to your evaluator
    # be careful with max_level > 2, the computation time can grow exponentially
    _ = B.evaluate_multilevel(evaluator=evaluate, do_print=True, max_level=2)
    # recommendations for moves are printed

Getting the Game Data
---------------------

* Set an intercepting mitm proxy on your phone and trust the CA
* look at the REQUESTS from the execute requests. They contain a large URL-encoded json block.
* copy this block, including the signature at the beginning, and paste it into the fruitisland function
* this block contains the complete layout of the board (as well as your last move and the tiles removed)

*If you do not know what this means, you probably should not use this piece of software*

