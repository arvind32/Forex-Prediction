# Forex-Prediction

This is a simple predictor of the GBP-SGD foreign exchange (FX) rate.

### Motivation

- I wanted to use this to build a working intuition of LSTMs
- Personal interest: the GBP-SGD rates affects my savings, so I tested if it was possible to predict this. Even modest accuracy would be useful because I would use it to shift funds, and not for trading strategies

---

### Past Work and Conclusions

- Surprisingly little research published research on FX vs. other asset classes; no prior work looking at this specific currency pair
- Non-linear, stochastic, highly non-stationary
- Results from successful approaches in other classes (e.g. indices, equities) don’t generalize well to FX

---

### Model used: LSTM

- Recommended model for time series data
- State of the art FX trading strategies apparently use LSTM networks, albeit with more advanced features. Outperforms even standard econometric models like GARCH (for equities), according to this paper on [Deep Learning Stock Volatility with Google Domestic Trends](https://arxiv.org/abs/1512.04916).
- My general impression from speaking with practitioners was corroborated by this recent paper on [Deep LSTM with Reinforcement Learning Layer for Financial Trend Prediction in FX High Frequency Trading Systems](https://www.mdpi.com/2076-3417/9/20/4460/htm), specifically the literature review section covering algorithmic approaches to high-frequency trading
- This paper on [Forecasting volatility trend of INR USD currency pair with deep learning LSTM techniques](https://ieeexplore.ieee.org/abstract/document/8768767) demonstrates how LSTM methods outperform SVM, Random Forest and Boosting techniques for FX predictions. 
- [a] and [b] also demonstrate similar findings for other financial asset classes.

---

### Hyperparameter Tuning

- Batch size 256 turned out to be the setting that gave best results
- Adding additional layers or increased epochs didn’t appear to offer significant improvements in prediction accuracy

### What I Learned

- Model seems to have good accuracy
- Consensus seems to be that simplex models don’t yield better results for Forex prediction vs vanilla models. This [recent paper](https://link.springer.com/content/pdf/10.1007/s42521-020-00019-x.pdf) systematically reviews different deep learning approaches to Forex prediction and comes to the same conclusion
- Such accuracy from even a simple model perhaps gives insight into how incredibly liquid the FX market is, where market-efficiency is almost taken for granted
- However, sharp FX fluctuations are not easily captured (this is not unique to FX-datasets). These correspond to macro-economic and geopolitical events such as the Brexit vote and the announcement of UK's lockdown in March
- Other model variants like LSTM with “peephole connection” may help, but my understanding is that this only brings out the time-relationship between different spikes (especially ones separated by 50 time steps). I doubt this will help because the spikes are due to “extrinsic” factors like geopolitical events and not necessarily time-relationship across prices. Including other features might help instead.


![Sample](https://i.postimg.cc/8z9py3fQ/Sample.png "Prediction of GBP-SGD rate")


### Next Steps

1. Figure out a better way to tune hyperparameters: grid search too tedious
2. Try different scaling methods and time-labels from [this paper](https://arxiv.org/pdf/1907.03010.pdf)
3. Try exotic activation functions: Swish etc.
4. Recast as classification instead (price movements up/down) and add more complex layers

---

### Other References

[a] Fischer, T., & Krauss, C. (2018). Deep learning with long short-term memory networks for financial market predictions. European Journal of Operational Research, 270(2), 654–669

[b] Shen, G., Tan, Q., Zhang, H., Zeng, P., & Xu, J. (2018). Deep learning with gated recurrent unit networks for financial sequence predictions. Procedia Computer Science, 131, 895–903.
