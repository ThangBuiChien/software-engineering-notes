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
