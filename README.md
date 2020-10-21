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



 

