# Introduction

For the most board games I use neural network for evaluation. They are somewhat complex and relatively slow but they compensate with their accuracy. The road to what I have achieved now was winding and bumpy, for years I changed and improved my implementations, the learning framework I use, and search algorithms. In this article I'm gonna write about the inputs I use for the board games I have written bots for.

If you used minimax or even mcts with some modifications, you probably struggled with the proper evaluation function. Evaluation function is something that tells how good a position is for the player. For various games it may mean something completely different. For chess the simple evaluation is material advantage + perhaps positional piece-square tables. For othello naive material generally works worse than random despite the fact that the goal of othello is to get as much stones as possible. Positional evaluation and mobility is much more important in othello. One thing is to come up with proper features for the game (material? patterns? corner stones?), the other is to get the right numbers for them (is queen worth 9 pawns? is corner stone worth 10 stones?). There are several automated ways to do this, ["Texel tuning"](https://www.chessprogramming.org/Texel%27s_Tuning_Method) being one of them. If you use gradient descent in Texel tuning, this is very much not unlike training neural network.

Neural networks have this advantage that for many cases you can use pure representation of a position and the net will figure out the features for itself. But sometimes, helping it by putting relevant features into its inputs makes it stronger and learn faster. The one of the latest revolution for chess, [NNUE](https://www.chessprogramming.org/NNUE), puts every pairs (king,piece) as inputs for the net, because king and its relation to other pieces is quite important, much more in shogi where the NNUE originated. It vastly increases number of possible inputs, but because they are rarely active, the time increase is negligible and you can also take the advantage of efficient partial updates.

My neural networks output value only, most of them have only 1 hidden layer. Hidden activation function is either relu or squared clipped relu and the output activation function is tanh. The inputs for the neural networks are 'one-hots', which are either 0 or 1. 'Ones' can be activated for example when there is pawn in particular square. 'Zeroes' are ommited in calculation. One-hots are different to 'scalars'. Scalars take any real value, for example score, usually normalized so the inputs are real values in range (0,1) or (-1,1).

For many games, I add various features to the inputs. Usually treating certain stones, or pawn differently depending on their neighbours and activating different 'ones' in the inputs. Thus the number of inputs is bigger and they are more sparsely activated. The clear disadvantage is the increased code size, which is visible due to code size limit in Codingame. Another disadvantage may be the increased time taken to extract those features from a position, as well that there are more changes between positions so partial updates will take more time as well. Nevertheless, the increased evaluation accuracy outweighs slowness and speeds up the training. Which additional inputs are good or not? This is something that should be tested and done by trial and error. 

The value networks can be used in various search algorithms, as eval for minimax or eval in mcts rollouts. My main search algorithm is best-first minimax with UCT as presented [here](https://www.codingame.com/playgrounds/55004/best-first-minimax-search-with-uct), nowadays known as [UBFM](https://arxiv.org/abs/2012.10700) but with exploration. Wherever applicable, I use partial updates when expanding node: evaluate base position, then for every child reevaluate only the changes. In the next pages I will present the inputs I use now and some I used before.

# Games

- [Oware Abapa](oware.md)
- [Breakthrough](breakthrough.md)
- [Connect 4 & Yavalath](connect4.md)
- [Othello](othello.md)
- [Ultimate Tic Tac Toe](uttt.md)
- [Amazons](amazons.md)
- [Clobber](clobber.md)
- [Nine Men's Morris](nmm.md)
- [Onitama](onitama.md)
- [Hex](hex.md)
