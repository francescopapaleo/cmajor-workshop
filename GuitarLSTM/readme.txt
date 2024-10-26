This patch is a machine leaning inference implemented in Cmajor.

The code to generate this patch can be found in https://github.com/SoundStacks/GuitarLSTM, which is a fork of the github project provided by https://guitarml.com/


Recreating the patch
--------------------

To recreate this patch, check out the above repo, and ensure the cmajor and RTNeural submodule is updated

To run the inference, and generate the Cmajor patch, run:

> git clone git@github.com:SoundStacks/GuitarLSTM.git
> cd GuitarLSTM
> git submodule init
> git submodule update

The model can then be trained with:

> ./train.py data/ts9_test1_in_FP32.wav data/ts9_test1_out_FP32.wav test

This will generate the output in models/test, and the generated Cmajor will be in models/test/patch


How this works
--------------

The model and inference is unchanged from the GuitarLSTM script, so this uses TensorFlow to build the model and run the training.

After training, we export the TF model to an RTNeural .json file, using the scripts included in the RTNeural package.

The script then executes the python script in cmajor/tools/rtneural to generate a Cmajor file based on the generated RTNeural json file.


