---
layout: post
title: My ML journey
subtitle: Some important key points observed by me being an ML enthusiast
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [test]
comments: true
---

Some models use images with values ranging from 0 to 1. Others from -1 to +1. Others use the "caffe" style, that is not normalized, but is centered.

## This loads an image and resizes the image to (224, 224):

~~~
 img = image.load_img(img_path, target_size=(224, 224))
~~~

The img_to_array() function adds channels: x.shape = (224, 224, 3) for RGB and (224, 224, 1) for gray image

~~~
 x = image.img_to_array(img) 
~~~

expand_dims() is used to add the number of images: x.shape = (1, 224, 224, 3):

~~~
x = np.expand_dims(x, axis=0)
~~~

preprocess_input subtracts the mean RGB channels of the imagenet dataset. This is because the model you are using has been trained on a different dataset: x.shape is still (1, 224, 224, 3)

~~~
x = preprocess_input(x)
~~~

If you add x to an array images, at the end of the loop, you need to add images = np.vstack(images) so that you get (n, 224, 224, 3) as the dim of images where n is the number of images processed
