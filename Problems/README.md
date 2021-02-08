My pytorch implementation of the Gatys style transfer code.
Losses are computed for mid-layer results, so I decided to create copies of the model, until the mid-layers.
The code takes truncated copies of vgg19 and computes loss and gradient per copy.

For instance, if we take layers pool2 and pool4 for computing Gram MSE, we would create 2 truncated copies of vgg19. One ending at pool4, and another ending at pool2.
In the figure below, only the pooling layers are shown, but convolution layers and relu layers are still there (except for at the end of pool4 in the first case and pool 2 in the second case)


![Alt text](https://github.com/mesahwi/Constraind-Reconstrution/blob/main/Problems/overview1.jpg?raw=true "Taking layers pool2 and pool4 as interested")


At the end, the losses would be summed up and passed to an optimizer (scipy's version of L-BFGS in my case), along with the sum of the gradients.

I believe my code to be a correct implementation, but I get different results from the caffe code developed by the Bethge group.
When transfering the pebble style(below) 

![Alt text](https://github.com/mesahwi/Constraind-Reconstrution/blob/main/Problems/pebbles.jpg?raw=true)

to white noise, I get 

![Alt text](https://github.com/mesahwi/Constraind-Reconstrution/blob/main/Problems/my_result.png?raw=true)

,when I should be getting

![Alt text](https://github.com/mesahwi/Constraind-Reconstrution/blob/main/Problems/what_i_should_get.png?raw=true)

Any help would be greatly appreciated.
