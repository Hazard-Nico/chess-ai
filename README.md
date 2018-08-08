# Grandmaster Level Chess AI (always in progress)

This is a chess AI and chess game built using python. 

I was inspired to try building my own chess ai when I learned about Alpha Go built by Google Deepmind.
See this paper for more information: https://storage.googleapis.com/deepmind-media/alphago/AlphaGoNaturePaper.pdf

This AI using a convolutional neural net as its evaluation function.

The trained convolutional net will be used as an evaluation function to evaluate future states from the tree search.  Then, the optimal move will be determined using the minimax algorithm (with alpha beta pruning).


Please use virtual machine to run this:

```
brew install python3
virtualenv -p /usr/local/bin/python3 venv 
virtualenv venv
source venv/bin/activate
pip install ipython notebook
```

You can find more details in my blog:
luweilikesdata.blogspot.com


### Tree generation:

The tree generator component of the chess AI generates the possible future board positions based on the possible moves that the pieces can make.  At any given position, there are on average 20 possible moves that can be made in chess.

![alt tag](http://www.andreykurenkov.com/writing/images/2016-4-15-a-brief-history-of-game-ai/2-evalfunc.png)

The above illustrates a chess tree.  Possible moves are generated from the current position to create hypothetical future states. 

## Evaluation function

I would say that this is the intuitive component of the chess AI.  Given an 8x8 chess position, the evaluation function with determine between a move is good or not by assigning it a numerical score.   A negative score means that black is winning, a positive score means that white is winning.

I believe this component of the AI is the most important because it is the one that can be greatly optimized.

The evaluation function can take many forms depending on what approach you want to take. You can use hard coded heuristic features. You could take a model based approach (ie. train a neural network).

![alt tag](http://www.neurosciencemarketing.com/wp-content/uploads/2015/06/einstein-valuable-540x338.jpg)

## Minimax algorithm:

The minimax algorithm essentially tries to find the optimal move from a tree of moves.   Starting from the leaves of the tree, you want to backwards calculate back to the optimal move by alternating between min() and max() (hence the name, minimax). 

When it is your turn, you want to optimize for your outcome, therefore you want to calculate the max() position score. 

When it is your opponents turn, he wants to minimize your outcome, therefore it calculates the min() position score.

![alt tag](https://www3.ntu.edu.sg/home/ehchua/programming/java/images/GameTTT_minimax.png)


The guide below explains minimax very well:
http://web.cs.ucla.edu/~rosen/161/notes/minimax.html

## Alpha-beta pruning:

Alpha-beta pruning is a process that can be used to greatly reduce the space of the tree search.  It works by pruning the search tree as you generate it by ruling out paths that neither you nor your opponent will never take.  

This is done by keeping track of two values called alpha and beta as you are searching through the tree.  
Alpha is the maximum lower bound (the lowest score you are willing to accept)  
Beta is the minimum upper bound (the highest score your opponent is willing to accept)  

The guide below explains alphabeta pruning very well:
http://web.cs.ucla.edu/~rosen/161/notes/alphabeta.html
