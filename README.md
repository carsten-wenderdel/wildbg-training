# wildbg training process

This repository documents the training process of the neural nets for the backgammon engine [wildbg](https://github.com/carsten-wenderdel/wildbg).

Each folder contains rollout data and the neural net that was trained on that data.
The first rollout happened with random moves. The second rollout used the first net for evaluating moves etc.

## 

| Data | Remarks |
| -------- | ------- |
| [0001](data/0001/) | Trained on rollouts with random moves |
| [0002](data/0002/) | |
| [0003](data/0003/) | Use `tanh` instead of `sigmoid` for inner layer |
| [0004](data/0004/) | |
| [0005](data/0005/) | Increased number of epochs from 10 to 20. Increased learning rate from 0.1 to 4.0 |
| [0006](data/0006/) | |
| [0007](data/0007/) | The 7th net is actually a bit worse than the 6th net. Less wins, less backgammon wins, but more gammon wins. |
| [0008](data/0008/) | No new rollouts were done. Instead this net was trained on the combined rollout data of iteration [6](data/0006/rollouts.csv) and [7](data/0007/rollouts.csv). The network topology has been changed from one hidden layer with `tanh` activation to three hidden layers with `ReLu` activation. |
| [0009](data/0009/) | Rollouts were done with the net from iteration [8](data/0008/wildbg.onnx). We now have different sets of data for contact and race positions, two different networks and also two different number of inputs. Combined they are better than the 8th iteration, but lose a lot of backgammons because the contact network is too optimistic. It will avoid going into a race and then loses backgammon instead. |
| [0010](data/0010/) | Rollouts were done with the nets from iteration [9](data/0009/). Only a contact network was rolled out and trained. The loss function for training was changed from MSELoss to L1Loss. |
| [0011](data/0011/) | No new rollouts; using the same training data as [0010](data/0010/). Instead of the PyTorch optimizer `SGD` here we used `Adam`. When duelling with the previous net, this results in an equity win of roughly 0.02. |
