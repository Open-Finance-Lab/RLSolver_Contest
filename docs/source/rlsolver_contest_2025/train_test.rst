Training
========

RLSolver makes it easy to get started — no separate training scripts are needed for conventional methods. You can run the provided solvers directly on well-prepared datasets.

For more details about available datasets, see the `README.md`.

In this guide, we walk through the full pipeline using the `s2v` method on 20-node Barabási–Albert (BA) graphs.

In the following, take the RL method s2v-DQN as an example: Dai et al. (2017) `Learning Combinatorial Optimization Algorithms over Graphs <https://arxiv.org/abs/1704.01665>`_.

During training, the reinforcement learning agent explores how graph structures relate to optimal (or near-optimal) solutions such as maximum cuts.  
Through repeated trial and reward, it gradually learns a general strategy that can be applied to new, unseen graphs with similar characteristics.

1. **Set basic config**:

   Edit `rlsolver/methods/eco_s2v/config.py <https://github.com/Open-Finance-Lab/RLSolver/blob/master/rlsolver/methods/eco_s2v/config.py>`_.  
  .. code-block:: python

      ALG = Alg.s2v                                   # select s2v as the RL method
      GRAPH_TYPE = GraphType.BA                       # use BA (Barabási–Albert) graph distribution
      NUM_TRAIN_NODES = 20                            # each training graph has 20 nodes
      TRAIN_INFERENCE = 0                             # 0 = train mode; 1 = inference mode

2. **Run training**:

  Run `rlsolver/methods/eco_s2v/main.py <https://github.com/Open-Finance-Lab/RLSolver/blob/master/rlsolver/methods/eco_s2v/main.py>`_.

   .. code-block:: text

      python rlsolver/methods/eco_s2v/main.py 

   This will generate a folder:  rlsolver/methods/eco_s2v/pretrained_agent/tmp/s2v_BA_20spin_b/

   Inside this folder, multiple `.pth` model snapshots will be saved over time.

   .. image:: /_static/example_s2v_training.png

3. **Select the best model from this folder**:

   Edit `rlsolver/methods/eco_s2v/config.py <https://github.com/Open-Finance-Lab/RLSolver/blob/master/rlsolver/methods/eco_s2v/config.py>`_.  

   Find the line:

   .. code-block:: python

      NEURAL_NETWORK_SUBFOLDER = "s2v_BA_20spin_s"

   To select a different model folder, set the param ``NEURAL_NETWORK_SUBFOLDER`` using the name of the desired folder.  
   For example:

   .. code-block:: python

      NEURAL_NETWORK_SUBFOLDER = "s2v_BA_20spin_b"

   Then run:  
   `rlsolver/methods/eco_s2v/train_and_inference/select_best_neural_network.py <https://github.com/Open-Finance-Lab/RLSolver/blob/master/rlsolver/methods/eco_s2v/select_best_neural_network.py>`_.

   .. code-block:: bash

      python rlsolver/methods/eco_s2v/train_and_inference/select_best_neural_network.py

   It will generate a file like: s2v_BA_20spin_1033_best.pth

   .. image:: /_static/best.png

4. **Rename and move the best model**:

      s2v_BA_20spin_best.pth  →  rlsolver/methods/eco_s2v/pretrained_agent/

   .. image:: /_static/move.png
