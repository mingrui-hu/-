## The Blog

-   Previous: PixelNet
    -   generate complex natural images not only one pixel at a time,  but ==1 colour-channel== at a time.
-   Basic Procedure:
    -   can condition on speaker identity ==(how?)==
    -   Training:
        -   Input: real waveforms recorded from human speakers
    -   Inference(AutoRegressive):
        -   ==sample the network==(how?) to generate synthetic utterances:
        -   Input: ==text or None(?)==
        -   At each step during sampling a value is drawn from the probability distribution computed by the network.
        -   This value is fed back to the input for the next prediction

-   Probablistic view:

    -   Stack of convolution layers: 

        -   model the factorisation of the joint probability of a waveform $\bold{x} = \{x_1, ..., x_T\}$:
            $$
            p(\bold{x}) = \prod^T_{t=1}p(x_t|x_1, ..., x_t-1)
            $$

-   Receptive Field:

    -   Standard 1-d Conv:
        -   Size(Receptive Field) = #hidden_layers + filter_length -1

    -   Dilated Conv
        -   $Size(Receptive\ Field) = \#hidden\_layers + (filter\_length -1) * d$
        -   base case:
            -   $d = 1$ -> standard Conv
        -   WaveNet Configurtion: for each layer, exponentially increase d & repeat 
            -   $d = 1, 2, 4,..., 512, 1, 2, 4, ..., 512, 1, 2, 4, ..., 512$
            -   Filter-length = 2
            -   Hence each dilated block has $Size(Receptive\ Field) = 1024$

-   ==Gated Activation Unit (?)==

    -   $$
        \bold{z} = tanh(W_{f, k} * \bold{x})\odot\sigma(W_{g, k}*\bold{x})
        $$

        

    -   from PixelCNN

-   Residual Connections

    -   residual & ==parameterised skip connections==?