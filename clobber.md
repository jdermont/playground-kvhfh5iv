# Clobber

Raw inputs that take into account white and black stones were weak, to say the least. In the evaluation function for clobber in standard minimax you should take the adjacent stones into account. So I did. For each stone I take into consideration it's orthogonal neighbours. One could think of them as plus-shaped n-tuples. You have black or white stone at the center, and 4 neighbours with one of three states (white, black or empty). If the center square is empty, I don't add that n-tuple into inputs. That gives 2x3^4=162 inputs for each n-tuple, and 64 squares give 162x64=10k inputs (actually a little less because of edges and corners), thus the net is tiny in terms of hidden layer size. Similarly to connect 4 and yavalath, I took some work to make feature extraction and partial updates efficient.

My bot leads with a little margin. It's surprising, because the scores for the moves he shows are often very misleading. If it wins, it wins. But whenever losing game, the bot often gives over 90% chance to win just to prove loss in the next move. I believe this is probably due to the very small size of the network, in terms on its internal representation. That and big branching factor so it doesn't see deep into the future.

![clobber](clobber.png "Clobber")

Example plus-shaped n-tuples. Index of 1 is 1x(012)3=5, index of 2 is 2x(0020)3=12 and index of 3 is **'null'**, because center is empty and it doesn't go to activated inputs. If in n-tuple 3 white stone would be in its center, then index would be 1x(1002)=29, and if black were in its center, then index would be 2x(1002)=58.
