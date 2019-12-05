# TENSORFLOW.JS: CONVERT A MODEL!
<hr>

## Layers Model


I decided to train a custom model using Keras with the Fashion MNIST Dataset. After building the model, I saved it to a 
```.h5``` file using the following code:
```python
model.save('final.h5')
```
The above command saves the weights + model structure.
Once the model was saved, I installed tensorflow.js using the follwoing command:

```python 
!pip install tensorflowjs
```
Next, I ran the following bash command to convert the keras model into a tensorflow.js Layers model:
```python
!tensorflowjs_converter --input_format keras \
                       final.h5 \
                       ../root
```
Here, the ```final.h5``` is the path to the file we saved earlier. While, the ```../root``` is the destination folder i.e. the 
folder we want to save in. Once the command was run, the follwoing files were created:

```
model.json
group1-shard1of1.bin
```
After digging around a bit, I realised that the ```model.json``` file containts the dataflow graph and the weights while the 
```shrad``` file contains the binary weights, which I think is used to cache for faster inference. 

## Graph Model

After using a custom model for the Layers model, I decided to use a pre-trained model for this one. After some exploring, I chose the mobilenet model. As I had already installed tensorflow.js, I did not have to do it again. Here is the code I used:

```python
!tensorflowjs_converter \
    --input_format=tf_hub \
    'https://tfhub.dev/google/imagenet/mobilenet_v1_100_224/classification/1' \
    /../root
  ```
  Here, we define the input format as ```Tensorflow Hub``` and the url to the model. Lastly, we define our destination folder 
  as ```../root```
  
  This outputted the following files:
  ```python
  model.json
  group1-shard1of5.bin
  group1-shard2of5.bin
  group1-shard3of5.bin
  group1-shard4of5.bin
  group1-shard5of5.bin
  ```
  
  
  I also tried to use the Big-GAN model that is used for image generation. Here is the code I used:
  ```python
  !tensorflowjs_converter \
    --input_format=tf_hub \
    'https://tfhub.dev/deepmind/biggan-deep-128/1' \
    /../home
  ```
  
One doubt that I could not solve is why there are a different number of ```shrad``` files for different models? I would love if a mentor could answer it. 

## Difference
The Principal difference is that the Layers model is used to convert models produced using Keras while the Graph model is used
to models produced with TensorFlow Saved Model. 

## Browser 
I tried following the instructions on collab but that did not work out. I personally feel that the documentation is a bit confusing as it mentions to use web servers and CORS but does not give any further documentation. I think this can be a possible imporvement to the other wise fantastic documenttion. 
I hope to continue to try to implement it to a browser, even after the deadline 
