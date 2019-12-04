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
