# Breakthrough

## Former

This was second game when I practiced NN and was succesful in it. At the time my learning framework was quite different, and I used to use minimax (alpha-beta) for training. Many changes occurred since then.

For breakthrough I used to have more complicated inputs. Each square, aside from being empty, black pawn or white pawn, each square could be also attacked, protected or both. So the indexes for each square goes like this: 0 - empty, 1 - white, 2 - black, +3 if square attacked by white pawn, +6 if square attacked by black pawn. And +12 if side to move was black. Yes, in the old times I had different inputs for the side to move, effectively doubling parameters and wasting precious space. It was at the times when I just learned how to utilize NNs and backpropagation values seemed simple then, less wrong sign errors to occur.

So there were 24x64=1536 inputs (a little less because for example white's home row can't be attacked by white pawns). The network distinguished protected and attacked pawn from unprotected one. This came from my standard eval, where I would penalty attacked unprotected pawn and it was winning more. Up to 6 squares could be changed per move. I used 48 hidden units in 1 hidden layer. It was winning 100% against any non-NN bots at the time. Not much changed until others started using NNs as well and crushed me. Later I added second hidden layer, it was slower but slightly better. In the meantime I used neural networks in other games, evolving my learning framework and search algorithms.

![breakthrough](breakthrough.png "Breakthrough")

Indexes per squares in the image above are: { 1, 1, 1, 16, 2, 4, 1, 1, 5, 0, 2, 3, 5, 6 }

As index inputs for the net (assuming top left is square is 0): { 1, 27, 53, 94, 106, 134, 157, 183, 213, 234, 262, 289, 317, 344 }


## Present

Then after some hiatus I decided to rewrite breakthrough learning framework. I decided to test simple inputs. White and black pawns only. So 128 inputs, but because due to extended solver, no my pawns on enemy house and no enemy pawn in my home row and no my pawns in enemy home row will ever be used in the network, so there are effectively 112 inputs. Because using rotation, if there is my pawn below enemy home row (and this is my move) then I win, so no need for my pawns below enemy home row as well. So 104 inputs in total. Because they wasted much less space, I could use bigger hidden layer. And lo and behold, those inputs are better than my old complicated one. It required at least 320 hidden nodes, but because 2, at most 3 inputs change per move, the speed decrease didn't occur. Moreover, less time is spent to extract features from position. And the more hidden units in the layer, the better it played. As of writing this article, I have 720 hidden units, 1 hidden layer in breakthrough.

For the image above, the index inputs for the net are: { 1 2, 3, }

As you can see, sometimes simpler is better. I learned a lot and changed my learning methodology several times. Some things have to be revised, perhaps they are no more needed. For example TD-Gammon utilized additional features in its inputs, but [more recent experiments show](http://www.scholarpedia.org/article/User:Gerald_Tesauro/Proposed/Td-gammon#Performance_Results) they may have been not needed after all.
