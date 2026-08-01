**

Task 1: Behaviour Cloning Baseline

  

Modifications:

- Added LayerNorm: BC is prone to overfitting and normalisation is beneficial for imitation learning tasks
    
- Changed from ReLU to SiLU: ReLU may lead to representational rigidity (dead neurons) compared to SiLU.
    
- Changed Loss from MSE to Huber Loss: Huber Loss acts like MSE for small errors but switches to a linear penalty (like MAE) for larger errors.
    
- Added Validation split for overfitting detection
    
- Added Early stopping based on val loss
    
- Added Learning rate scheduler
    

**

