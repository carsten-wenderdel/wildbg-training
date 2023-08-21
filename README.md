# wildbg training process

This repository documents the training process of the neural nets for the backgammon engine [wildb](https://github.com/carsten-wenderdel/wildbg).

Each folder contains rollout data and the neural net that was trained on that data.
The first rollout happened with random moves. The second rollout used the first net for evaluating moves etc.

## 

| Data | Remarks |
| -------- | ------- |
| [0001](data/0001/) | Trained on rollouts with random moves |
| [0002](data/0002/) | |
| [0003](data/0003/) | Use `tanh` instead of `sigmoid` for inner layer |
