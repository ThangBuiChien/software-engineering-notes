# Optimize using all VRAM and CPU

cudnn.benchmark = True -> Finds optimal convolution algorithms

VRAM using low =>
Increase batch size
Use larger model
Cache more data on GPU

RAM Usage low =>
Could improve data loading pipeline
Opportunity for larger data prefetching

```python
train_loader = DataLoader(
    dataset,
    batch_size=batch_size,
    num_workers=4,  # Increase from default
    pin_memory=True,  # Important for GPU training
    prefetch_factor=2
)

```

# Speed up training in pytorch

1. Consider using a different learning rate schedule.

2. Use multiple workers and pinned memory in DataLoader.

   - Turn on prefetching.
   - Increase the number of workers: num_worker = 4 \* num_GPU. Remember Inc Num ~ Inc RAM of CPU
   - Use pin_memory=True.

3. Max out the batch size.

4. Use Automatic Mixed Precision (AMP).

5. Consider using a different optimizer.

6. Turn on cudNN benchmarking.

7. Beware of frequently transferring data between CPUs and GPUs.

8. Use gradient/activation checkpointing.

Use gradient accumulation.

Use DistributedDataParallel for multi-GPU training.

Set gradients to None rather than 0.

Use .as_tensor rather than .tensor()

Turn off debugging APIs if not needed.

Use gradient clipping.

Turn off bias before BatchNorm.

Turn off gradient computation during validation.

Use input and batch normalization.

# Deep learning method

```
# These are equivalent:
nn.MaxPool2d(kernel_size=2, stride=2)
nn.MaxPool2d(2)  # stride defaults to kernel_size if not specified
```

kernel_size: The size of the window to take a max over.
stride: How much to move the window by in each step.

# Loss function, optimizer and scheduler

## 1.Loss Functions:

- CrossEntropyLoss: Standard for multi-class classification
- BCELoss/BCEWithLogitsLoss: For binary classification
- MSELoss: For regression tasks
- L1Loss: For regression when outliers should have less influence
- SmoothL1Loss: Combines benefits of L1 and L2, good for object detection

## 2.Optimizers:

- SGD with momentum: Often gives best final accuracy but slower convergence
- Adam: Great default choice, especially for deep networks
- AdamW: Better weight decay implementation than Adam
- RMSprop: Good for RNNs and non-stationary problems

## Learning Rate Schedulers:

- CosineAnnealingLR: Smooth decay, good for many tasks
- ReduceLROnPlateau: Reduces LR when metrics plateau
- OneCycleLR: Popular for faster convergence
- StepLR: Simple step decay at fixed intervals
- CosineAnnealingWarmRestarts: Periodic restarts can help escape local minima

## Tips

Some tips for choosing:

- Start with Adam optimizer and CrossEntropyLoss for classification tasks
- If overfitting, increase weight decay or try AdamW

```python
import torch
import torch.nn as nn
import torch.optim as optim

# 1. Common Loss Functions
def get_loss_function(loss_type, **kwargs):
    loss_functions = {
        # Classification
        'cross_entropy': nn.CrossEntropyLoss(),  # Multi-class classification
        'bce': nn.BCELoss(),  # Binary classification
        'bce_with_logits': nn.BCEWithLogitsLoss(),  # Binary classification with sigmoid

        # Regression
        'mse': nn.MSELoss(),  # Mean squared error
        'mae': nn.L1Loss(),  # Mean absolute error
        'smooth_l1': nn.SmoothL1Loss(),  # Huber loss

        # Special Cases
        'kl_div': nn.KLDivLoss(),  # KL divergence
        'nll': nn.NLLLoss(),  # Negative log likelihood
    }
    return loss_functions[loss_type]

# 2. Common Optimizers
def get_optimizer(optimizer_type, model_params, lr=0.01, **kwargs):
    optimizers = {
        'sgd': optim.SGD(
            model_params,
            lr=lr,
            momentum=kwargs.get('momentum', 0.9),
            weight_decay=kwargs.get('weight_decay', 5e-4)
        ),
        'adam': optim.Adam(
            model_params,
            lr=lr,
            betas=kwargs.get('betas', (0.9, 0.999)),
            weight_decay=kwargs.get('weight_decay', 5e-4)
        ),
        'adamw': optim.AdamW(
            model_params,
            lr=lr,
            betas=kwargs.get('betas', (0.9, 0.999)),
            weight_decay=kwargs.get('weight_decay', 0.01)
        ),
        'rmsprop': optim.RMSprop(
            model_params,
            lr=lr,
            momentum=kwargs.get('momentum', 0),
            weight_decay=kwargs.get('weight_decay', 0)
        )
    }
    return optimizers[optimizer_type]

# 3. Common Learning Rate Schedulers
def get_scheduler(scheduler_type, optimizer, **kwargs):
    schedulers = {
        'cosine': optim.lr_scheduler.CosineAnnealingLR(
            optimizer,
            T_max=kwargs.get('T_max', 200)
        ),
        'cosine_warm': optim.lr_scheduler.CosineAnnealingWarmRestarts(
            optimizer,
            T_0=kwargs.get('T_0', 10)
        ),
        'step': optim.lr_scheduler.StepLR(
            optimizer,
            step_size=kwargs.get('step_size', 30),
            gamma=kwargs.get('gamma', 0.1)
        ),
        'reduce_on_plateau': optim.lr_scheduler.ReduceLROnPlateau(
            optimizer,
            mode=kwargs.get('mode', 'min'),
            factor=kwargs.get('factor', 0.1),
            patience=kwargs.get('patience', 10)
        ),
        'one_cycle': optim.lr_scheduler.OneCycleLR(
            optimizer,
            max_lr=kwargs.get('max_lr', 0.1),
            epochs=kwargs.get('epochs', 100),
            steps_per_epoch=kwargs.get('steps_per_epoch', 100)
        )
    }
    return schedulers[scheduler_type]

# Example usage:
def setup_optimization(model, loss_type='cross_entropy', optimizer_type='adam',
                      scheduler_type='cosine', **kwargs):
    criterion = get_loss_function(loss_type)
    optimizer = get_optimizer(optimizer_type, model.parameters(), **kwargs)
    scheduler = get_scheduler(scheduler_type, optimizer, **kwargs)
    return criterion, optimizer, scheduler
```
