# **DCGAN Implementation for Animal Images Generation**


**Objective**: To build a Deep Learning model to generate new animal images using GAN

**Data**: The animal image dataset contains 14630 images of cats, dogs and wild animals

**Data Preparation:** 

  •	Batch size of 128

  •	Image Resizing to (64, 64, 3)

  •	Cast image dtype to Float32 

  •	Image Normalization to get the pixel intensity in [-1,1]

And we do shuffling to randomly reorder data before each epoch and use of buffer to prefetch inputs from input dataset before they are requested

## **Model Design:**


	Generator’s purpose is to progressively become better at creating images that look real and generator’s purpose is to get better at telling them apart.
I have implemented DCGAN model to generate images.


**Generator:**

	The generator uses Conv2DTranspose (up sampling) layers to produce images from random noise. We start with a Dense Layer that takes this input that is random noise (LATENT_DIM = 100). We keep up sampling with Conv2DTranspose, using Batch Normalization and LeakyReLU as activation function. Leaky ReLU is beneficial when the data has a lot of noise, because it can provide a non-zero output for negative inputs and avoid discarding potentially important information. And use tanh activation in last layer to get values between [-1,1]
 

![image](https://github.com/ujjawalsingh10/DCGAN-for-Image-Generation/assets/19973541/eec00753-8ce0-4619-8d2e-673ec8899532)






**Discriminator:**

	The Discriminator is a CNN based image classifier.
We use the discriminator to classify the generated images as real or fake. The model gets trained to output positive values for real images and negative values for fake images. We use Conv2D layers to the images from the generator and flatten it and use sigmoid function in the last layer to get the output values for fake and real images.  

![image](https://github.com/ujjawalsingh10/DCGAN-for-Image-Generation/assets/19973541/85251113-b825-4911-9aaf-570342286bdb)



## **Model Training:**

We define loss functions and optimizers for both the models. 

**Discriminator Loss:**

This method tells us how well the discriminator can differentiate between the real images and fakes. This compares the discriminators predictions on real images to an array of 1s and the discriminators predictions on fake (generated) images to 0’s. We use BinaryCrossEntropy loss function for both the models

**Generator Loss:**

Generator loss tell us how well it was able to trick the discriminator. If the generator performs well it means the discriminator will classify the fake images as real. We compare the discriminators decisions on generated images to 1s.

### **Optimizers:**

Both Generator and discriminator use separate optimizers. We use Adam optimizer with learning rate of 0.0002.

### **Training Loop:**

Model trained on 150 epochs. Training starts with generator getting random noise as input. This noise is used to produce an image. The discriminator is then used to classify real images (drawn from the training set) and fake images (produced by the generator). Then we calculate the loss and use the gradients to update the generator and discriminator.

**Generator vs Discriminator Loss:**

![image](https://github.com/ujjawalsingh10/DCGAN-for-Image-Generation/assets/19973541/e150e94f-c344-466a-be19-2cdd78aa1def)



### **Sample Generated Images:**
![image](https://github.com/ujjawalsingh10/DCGAN-for-Image-Generation/assets/19973541/00b8ebd3-6e6a-4059-9879-8dd5d5692e97)


**Google Drive Link:** (contains dataset, generated images after each epoch, Google Colab code and model weights)
https://drive.google.com/drive/folders/1VvAGNeYiecgmoDuqUOFzDxrtrMJ1aWxM?usp=sharing
