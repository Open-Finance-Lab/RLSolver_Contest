Testing
=======

Now that training is complete and the best model has been selected and moved, we proceed to the testing phase.  
The following steps configure and run inference using the trained model on graphs of various sizes.

1. **Switch to inference mode**:

   Edit  `rlsolver/methods/eco_s2v/config.py <https://github.com/Open-Finance-Lab/RLSolver/blob/master/rlsolver/methods/eco_s2v/config.py>`_.  


   .. code-block:: python

      TRAIN_INFERENCE = 1                                              # 1 = inference mode
      NUM_TRAINED_NODES_IN_INFERENCE = 20              # model was trained on 20-node graphs
      NUM_INFERENCE_NODES = [20, 100, 200, 400, 800]   # test on graphs of various sizes
      NUM_INFERENCE_SIMS = 50                          # number of parallel environments in inference

   Although the model was trained only on 20-node graphs, it can be applied to larger graphs.
   Ensure that all test graphs have node counts ≥ 20.

2. **Run inference**:

   Run `rlsolver/methods/eco_s2v/main.py <https://github.com/Open-Finance-Lab/RLSolver/blob/master/rlsolver/methods/eco_s2v/main.py>`_.

   .. code-block:: text

      python rlsolver/methods/eco_s2v/main.py 


   This step uses the selected best model to run inference over all test instances.

   The result files will be saved in:  rlsolver/result/syn_BA/

   Each result file includes:

   - ``obj``: best objective value (maximum cut size)
   - ``running_duration``: solving time in seconds
   - ``num_nodes``: number of nodes in the graph
   - ``alg_name``: algorithm used (e.g., ``eeco``)
   - node assignments: each node's group (1 or 2)

   Example output:

   .. image:: /_static/result.png
      :align: center
      :width: 600px

This completes the full pipeline: **Training → Model Selection → Inference** for the `eeco` (or s2v, or eco) method on synthetic BA graphs.
