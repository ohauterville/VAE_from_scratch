# Questions

### Why normal distributions ?

An important contribution of VAE is to force the distribution in the latent space (*q(z|x))* to be a Normal standard (*mu=0, sigma=1*). But why ? This has several reasons : 
- continuity: we want the regions of the latent space to remain close in order to avoid empty space that would generate noise,
- diversity: fixing the variance to a non too small number forces the latent space to have regions and not just single points (like autoencoders),
- ease of compute: the loss function uses the Kullback-Leibler (KL) to compare the distribution of the encoder to the Standard Normal. This functions has an analyticla solution between two gaussians.
- reparameterization trick: in order to backpropagate, we need every step to be differentiable. But, since the latent space works now with spaces and not points, the decoder **samples** one input from the latent space to decode. This is a random process and it would prevent  the gradient to backpropagate. So instead of *z=random_sample(mu,sigma)* we get *z=mu+sigma.epsilon*, a determistic value plus a bit of noise.   
