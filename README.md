# ML_setup
# Description
A step by step guide of how to setup an AMD RX7900 GPU on an Arch System.
Tensorflow is also being set up in a Docker container

# HOW To
1. ## Install rocm driver
- check GPU
```bash
    lspci -k | grep -EA3 'VGA|3D'
```
- install rocm driver. Make sure, that the system is clean and does not have any remnants of older drivers installed
```bash
    sudo apt update
    yay -S rocm-opencl-runtime
```
2. ## Install Docker
- Not entirely sure, what the package name is. 
- The usermod is for not having to write sudo for every docker command
```bash
    sudo pacman -S docker
    sudo usermod -aG docker $USER
```
- Test run
```bash
    docker run -it --rm hello-world
```

3. ## Run test container

```bash
sh container.start
```

4. ## Run Tensorflow check
- In Container:

```bash
python
```

```python
import tensorflow as tf
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))

gpus = tf.config.list_physical_devices('GPU')
print("GPUs:", gpus)

```

5. ## Run Tensorflow test 

```python
    import tensorflow as tf
    vec_1 = tf.constant([1.0,2.0,3.0],dtype = tf.float32)
    vec_2 = tf.constant([2.0,0.4,30.0],dtype = tf.float32)
    res = tf.multiply(vec_1,vec_2)
    print("result: ",res.numpy())
```



## Project status
This is just a quickstart for my current system. The package versions and names change every now and then, so be warned and be prepared to clean up old packages. 

I intend to revisit this repo to update the commands, but not very frequently. If you have any other GPU's or Operating systems, feel free to contribute.