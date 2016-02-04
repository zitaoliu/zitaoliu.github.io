---
layout:     post
title:      Jane Street Interview
date:       2016-02-03 11:00:00
summary:    Jane Street Interview - Quantitative Research Position.
categories: interview 
---


## Phone Interview

A coding problem with real settings. 

We have a trading system that wants to trade "n_stocks" stocks (1,...,n_stocks). We have "n_comps" computers (1,...,n_comps). We want to assign each stock to a computer. There exist "n_datas" data streams (1,...,n_datas). We know, for each stock, the set of data streams you need to trade that stock. You can call a function
data_streams[] data_for_stock(stock s). Each data stream has a cost and we can get it by calling int cost_of_data(data_stream d). Our goal is we want to minimize max cost across comps. A cost of a computer is defined as the total costs of the data streams needed on that computer. The data streams on one computer is the union of all the needed data streams from all the stocks on that computer.

