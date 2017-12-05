---
layout: post
title:  "Bitcoin Transaction Fee Estimation"
date:   2017-12-04 22:09:54 -0600
categories: bitcoin fees haskell finance
---

The objective is to develop an web-based, interactive bitcoin transaction fee estimator based on bitcoin core 0.14 implementation. Thanks to the excellent blog post by newburry and the orignal document, I'm saved from needing to read the original implementation.  

In this post, I will cover the overall system architecture as well as the implementation details of the system's components which basically code written in Haskell.

### Objective

We want to find the fee rate that you should use to in order for your 
tx to be included in the blockchain within a given target number of blocks.

### Development Plan

To achieve the above objective, we return the lowest fee rate that will 
with high probability (%95) achieves the objective.

- build a priodic process for updating the fee buckets:
  
  forever:
   fetch the height of the last checked block from the db table
 - fetch the most recent block from RPC
 - fetch the mempool from RPC
 - fetch the unconfirmed tx from db table
 - is the most recent block is heigher than the last checked block?
   - if yes:
    - any transaction in the unconf tx was confirmed in the most recent block?
    -  if yes: update bucket with the new confirmed transactions
    - if no: pass
  - if no: pass
  - delete mempool tx db table enteries
  - insert new mempool tx to db table
  
- build the ui

- deploy the website

### Testing Plan

- Make sure the inserting confirmed tx do not duplicate
- Make sure the inserting unconfirmed tx do not duplicate
