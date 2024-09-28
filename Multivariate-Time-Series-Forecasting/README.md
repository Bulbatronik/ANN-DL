<h1 align="center"> Multivariate Time-Series Forecasting</h1>

## Overview
The goal of the project is to develop a Neural Network based forecasting model for a multivariate time series by exploiting past observations in the input sequence to correctly predict the future. This project explores the impact of various network hyperparameters, such as the type of recurrent layers, number of units, dropout, attention, as well as the window size, future telescope, prediction type (one-shot vs autoregressive) and etc. Based on the work done and the ranking on `CodaLab` competition organized by the TA of the course, our team achieved 5 out of 5 points for the assignment. 

## Dataset
The dataset used in this project is can be found in the [`input` folder](input/). Our dataset contains `68529` samples of `7` time-series stored in a **csv** file.

We split the dataset into a training (80%) and validation (20%) sets. The dataset is than rescaled using `MinMax` scaler fitted on the training set and applied to both datasets. We extract the windows from the data if size `200` with stride set to `5`. We did not create a test set, as it was already provided on the `CodaLab` platform.

## Approach
Folder [`notebooks/past_versions`](notebooks/past_versions/) contains two folders (`one shot` vs `autoregressive`) based on the way we perform the forecasting of the future. We evaluated both oneshot and autoregressive predictions on most of our model, and found that the
latter produced better predictions in almost all the cases. To summarize the content, we provide the following changelog:

### Autoreg
- 00_LSTM: three LSTM layers (50 units each) + dropout (0.2 each), scores 9.5369
- 01_BiLSTM: three Bidirectional LSTM layers (256 units each) + dropout (0.2 each), scores 4.0945
- 02_GRU: three GRU layers (256 units each) + dropout (0.2 each), similar to 00_LSTM, not submitted
- 03_BiGRU: three Bidirectional GRU layers (256 units each) + dropout (0.2 each), scores 8.2179
- 04_BiLSTM: four Bidirectional LSTM layers (256 units each) + dropout (0.2 each), scores 5.0126
- 05_BiLSTM: two Bidirectional LSTM layers (256 units each) + dropout (0.2 each), scores 5.1252
- 06_seq2seq: 3enc+2dec BiLSTM layers (256 units each), waiting for test
- 07_seq2seq-attention: 3enc+2dec BiLSTM layers (256 units each) + attention mechanism, waiting for test

### Oneshot
- 00_LSTM: three LSTM layers (50 units each) + dropout (0.2 each), similar to its autoreg counterpart, not submitted
- 01_BiLSTM: three Bidirectional LSTM layers (256 units each) + dropout (0.2 each), scores 6.5361
- 02_BiGRU: three Bidirectional LSTM layers (256 units each) + dropout (0.2 each), scores 5.1881

Initial tests with unidirectional layers yielded similar results (`RMSE around 9.5`) for both `LSTM` and `GRU` layers; changing the number of units per layer (50, 100, 256) and the number of layers (2, 3, 4) did not bring a significant improvements. During this
phase we observed that, in some cases, there was a jump discontinuity between the last input and the first predicted value: to solve this issue we employed a dropout layer after every recurrent one, and ob-
served that the gap disappeared.

Later we tested `GRU` and `BiLSTM` models, where we obtained the best results for `BiLSTM` with 3 recurrent layers (`RMSE 4.0945`).

After that we used `Seq2Seq` architecture  with `BiLSTM` layers, which we further adapted by using `Luong attention` over it, which achieved the the best final performance of all the tested configurations (`RMSE 3.56`).

The final results, as well as a brief description of the steps done, are presented in the [report file](report/tex/main.pdf).

## References
Thang Luong, Hieu Pham, and Christopher D. Manning. (2015). Effective Approaches to Attention-based Neural Machine Translation.
