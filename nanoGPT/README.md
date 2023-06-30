This project is inspired by Andrej Karpathy's nanoGPT video that can be found [here.](https://www.youtube.com/watch?v=kCc8FmEb1nY)
It builds a GPT like decoder only language model from scratch using the tiny Shakespeare dataset.  

The final model contains 6 blocks with each having 6 attention heads and 384 dimensional token representation. Its trained for 5K epochs with a learning rate of 3e-4.Training takes ~ 10 minutes on the A100 GPU.  
Sample generated text can be seen in the output.txt file.  

Since the compponents are written from scratch, I was able to carry out ablation experiments & make the following observations about the various components in the Transformer architecture from the performance of the model:
- to be written
