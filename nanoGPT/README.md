![Image taken from Jay Alammar's GPT-2 video](./decoder_image.png?raw=true "Decoder Diagram from Jay Alammar's GPT-2 blog")

This project is inspired by Andrej Karpathy's nanoGPT video that can be found [here.](https://www.youtube.com/watch?v=kCc8FmEb1nY)
It builds a GPT like decoder only language model from scratch using the tiny Shakespeare dataset.  

The final model contains 6 blocks with each having 6 attention heads and 384 dimensional token representation. Its trained for 5K epochs with a learning rate of 3e-4.Training takes ~ 10 minutes on the A100 GPU.  
## Outputs
 -  Generated text can be seen [here](https://github.com/ldr7/language_model_from_scratch/blob/main/nanoGPT/output.txt). This is from the Language model built from scratch.
 - To compare against existing models, the output of ChatGPT is included in the file [here.](https://github.com/ldr7/language_model_from_scratch/blob/main/nanoGPT/chatgpt_output.txt)
 - GPT-2 is fine tuned on the Shakespeare dataset and prompted for generation. The fine tuning notebook and the output is added.
 - Falcon (7B) is prompted to generate text.

It's not too suprising that the best generated text is from ChatGPT. Our custom model trained only on Shakespeare does not learn enough information to learn the broader language. Any more increase in epochs or learnable parameters leads to sharp overfitting.

## Ablation Studies  
Since the compponents are written from scratch, I was able to carry out ablation experiments & make the following observations about the various components in the Transformer architecture from the performance of the model:
- if Dropout is helpful or not does not depend on learning rate (lr). lr trends remain unchanged with or without dropout
- adding multiple heads does make the model less sensitive to lr
- adding multiple heads does seem to reduce overfitting (val-train error)
- adding feed forward layer (ffw) layer really improves performance. communicate + compute ftw!!
- projection layer helps in case of ffw even without residual connection in attention. projection layer is the linear layer at output.
- stacking multiple blocks without residual or layer norm does not help.
- projection layer in attention worsens performance without reisdual connections.
- residual connection is ob very useful in imporovement
- residual connections are more useful than layer norm. note that the comparison is done with projection layer removed in attention module (multi-head attention block)
- Post norm gives better numbers than Pre norm. Post norm is putting the layer normalization after the attention or feed forward operations. In Prenorm layer normalization is done on the input before attention or feed forward operations.
