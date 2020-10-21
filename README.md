# image_mining_2020

I tried serval network to try to understand how the parameters affects the results.

## First try :

For this one I just add another convolution layer with :

* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 20

So we endup with a 20 * 8 * 8 pictures. Then I tried to modify the parameters.

* batch  : 32
* epochs  : 7
* learning rate : 0.002

witch gaves 64.5% of accuracy on test. As the validation loss shows a min at 5 I tried again with only 5 epochs.
That gaves the same result.

So I tried to reduce the learning to prevent the validation loss from diverging.

* batch  : 32
* epochs  : 10
* learning rate : 0.0015

That gaves 65 % of accuracy on test.

## Second try

This time I used 3 convolunational layers :

1)
* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 8

2) (max pooling)
* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 8

3)
* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 13

4) (max pooling)
* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 13

5)
* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 18

6) (max pooling)
* kernel  : 3*3
* stride  : 1
* padding : 1
* output chanel : 18

The idea was to slowly increase the numbers of chanel to gather higher level informations. I kept the size of the images constant in a first time.

For this one I did a lot of test.

1)| 63.4 %
* batch  : 32
* epochs  : 5
* learning rate : 0.001

As it was a bit slow I tried to increase first the number of epoch and then the learning rate.

2)| 64.9 %
* batch  : 32
* epochs  : 10
* learning rate : 0.001


3)| 64.38 %
* batch  : 32
* epochs  : 5
* learning rate : 0.0015

As it seems to be a good idea I contiuned.

4)| 63.8 %
* batch  : 32
* epochs  : 10
* learning rate : 0.0015

This lower the accuracy. The validation loss has began to divrge. Indeed if both learning rate and the number of epoch are too hight the network etheir can not converge or overspecialize on the
learning dataset. It will be really good on training but small variation on the images (which appear during validation and test) will make the network wrong.

Then I tried something else. I increased the batch size : 

5)| 64.78 %
* batch  : 64
* epochs  : 7
* learning rate : 0.001
 
As expeted the learning was much faster.

I also tried to reduce the batch size and the learning rate (to prevent from overfitting)

6)| 66.66 %
* batch  : 16
* epochs  : 10
* learning rate : 0.006

That is better ! But after some other tests I decided to change the network

## Third try
    
![3](https://github.com/JBortolussi/image_mining_2020/blob/main/images/3.PNG)
