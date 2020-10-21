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

The idea of this net is to first increse the number of chanels and then concentrate the information by reduving the number of chanels and the size of the images.
The out going image is 3 * 8 * 8

For this one I tried the same strategies as for the second one. The result were not good. The best solution I found was :

1)| 61.9 %
* batch  : 64
* epochs  : 25
* learning rate : 0.0025

In my opinion the problems of this net is that it end with not neought information. 3 * 8 * 8 is maybe not enought for classifying 10 objects.

## Fourth try

For this test I just try to fix the previous one. As I really wanted to keep the structure I increased the number of chanels (ends with 36 chanels).
I also use max pooling without padding so the size of the image slowly reduce. The results were far better :

1)| 72 %
* batch  : 32
* epochs  : 10
* learning rate : 0.001

After a few other test I quickly decide to go for more chanels.

## Fifth try
![5](https://github.com/JBortolussi/image_mining_2020/blob/main/images/5.PNG)

It is the same as the fourth one but with even more chanels.

The first test was not good. This the validation loss :

![5_1](https://github.com/JBortolussi/image_mining_2020/blob/main/images/5_32_10_001.PNG)

Because of this figure I lower the learning rate to 0.0006 :

1)| 73.3 %
* batch  : 32
* epochs  : 10
* learning rate : 0.0006

As the validation loss was still increasing at the end I also reduced the number of epoch :

2)| 74 %
* batch  : 32
* epochs  : 8
* learning rate : 0.0006

Then I tried other strategies but I did not manage do got better result than 74 % :

3)| 73.5 %
* batch  : 16
* epochs  : 8
* learning rate : 0.0003

![5_1](https://github.com/JBortolussi/image_mining_2020/blob/main/images/5_32_10_001.PNG)

## sixth try

I, again, kept the same structure but I did not to increase the number of chanels. So I hadded a new layer in the middle of the net :

![6](https://github.com/JBortolussi/image_mining_2020/blob/main/images/6.PNG)

The scope of this layer is to get larger scale feature thanks to his 5*5 kernel but without reducing to much the size of the image.

The first try :

1)| 73 %
* batch  : 16
* epochs  : 6
* learning rate : 0.00035

gaves promissing result so I continued and get the following figure :

2)| 74.8 %
* batch  : 16
* epochs  : 10
* learning rate : 0.0002

![6_1](https://github.com/JBortolussi/image_mining_2020/blob/main/images/16_10_0002.PNG)

This validation loss seems a bit a bit noisy so I tried to increase the batch size


3)| 74.2 %
* batch  : 16
* epochs  : 10
* learning rate : 0.0002

![6_2](https://github.com/JBortolussi/image_mining_2020/blob/main/images/22_10_0002.PNG)

This curve look promissing since the validation loss was decreasing at the end but I did not manage to get something better

## Last tests

For the last to tests I wanted to increase a lot the number of chanels an see what happen.
So I just double the number of chanels :

![7](https://github.com/JBortolussi/image_mining_2020/blob/main/images/7.PNG)

3)| 75 %
* batch  : 26
* epochs  : 8
* learning rate : 0.0002


![7_1](https://github.com/JBortolussi/image_mining_2020/blob/main/images/26_8_0002.PNG)

This is better not that much considering that I double the number of node it would interesting to find an other architecture before increasing the number of node again

A last thing I wanted to try was to only increase the number of node on the last layer. Its lead to comparable result. The network use the last layer to classify the picture so its not that surprising.
Indeed more node on the last layer means more information to found the result. Remain the question of the quality of the given information.

## To Conclude

My best score is 75 %. Every parameters is important and can lead to significant differences so to test every cinfiguration is realy long. In seems that a minimum of nodes in the needed but infinitly
increase the number of nodes is not a solution.
Considering the validation loss function
