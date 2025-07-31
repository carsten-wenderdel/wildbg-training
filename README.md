# wildbg training process

This repository documents the training process of the neural nets for the backgammon engine [wildbg](https://github.com/carsten-wenderdel/wildbg).

Each folder contains rollout data and the neural net that was trained on that data.
The first rollout happened with random moves. Later rollouts used previous nets.

There are some issues with the rollout data:
- Some position IDs in the folders [0009](data/0009/), [0010](data/0010/), [0012](data/0012/) and [0015](data/0015/)
  have been encoded wrongly. See https://github.com/carsten-wenderdel/wildbg/issues/27

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
| [0012](data/0012/) | Increased number of epochs from 20 to 50. The race data was rolled out with race #9 and contact #11 (each most recent). The contact data was rolled out with race #12 and contact #12. For the contact net we switched from Adam to AdamW, seems to be a small improvement. Overall dramatic improvement over the previous nets, they now only lose 0.7% backgammon. |
| [0013](data/0013/) | No new rollouts. The contact net is using `Hardsigmoid` instead of `ReLU` as activation function. It seems to give slightly better results (equity win 0.01), but inference also takes a bit longer. |
| [0014](data/0014/) | No new rollouts. The contact net is trained on the same data as the two previous ones, just a few more epochs, a slightly smaller learning rate and more careful comparisons between different onnx files. Equity win of 0.01. |
| [0015](data/0015/) | Contains rollout data for race positions, but no net. Due to poor choice of positions training on that data will lead to worse nets than previous ones. |
| [0016](data/0016/) | Race data: Finding the positions was done with contact [11](data/0011/contact.onnx) and race [9](data/0009/race.onnx). Rollouts were done with race [12](data/0012/race.onnx). Race net: We now use `CrossEntropyLoss`, `ReLU`, 83 epochs. |
| [0017](data/0017/) | Contact data: Finding the positions was done with contact [11](data/0011/contact.onnx) and race [9](data/0009/race.onnx). Rollouts were done with contact [14](data/0014/contact.onx) and race [16](data/0016/race.onnx). Contact net: We now use `CrossEntropyLoss`, `HardSigmoid`, 80 epochs. The latest nets (16/17) bring an equity win of 0.021 compared to contact [14](data/0014/contact.onx) and race [12](data/0012/race.onnx).|
