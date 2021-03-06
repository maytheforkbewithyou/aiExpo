# Workshop in Deep Learning for Computer Vision
## AI Expo Africa 

This repository contains all the code and resources discussed in the workshop. 

This is a guide to get you started doing it yourself.

Most of the code is based on work done by the Fastai community. So please check out their outstanding [courses](http://course.fast.ai/), [forums](http://forums.fast.ai/) and [library](https://github.com/fastai/fastai).


## Getting Started

You'll need a machine with a GPU to run this code efficiently. If you don't have access to one already, here are your options:

1. [Salamander](https://salamander.ai/)
2. [Kaggel Kernels](https://www.kaggle.com/kernels)
3. [Building your own machine](http://forums.fast.ai/t/build-your-deep-learning-box-wiki-thread/13536)


### Creating a Salamander VM

Salamander is easy to use and in addition you also get full control of the machine; it's very cheap and has friendly support. Therefore we chose this option for the workshop. To get started using Salamander, go to the [website](https://salamander.ai/), follow the steps to create an account and then design your server. 75GB SSD and either of the *Accelerated Computing* servers will do just fine. You can uncheck the *TensorFlow* box in the software tab. 

Once your server is up and running (might take a few minutes to start), you can open up a Jupyter Lab environment by clicking on the *Jupyter Lab* box.


### Updating Fastai

Open up a terminal using the Jupyter Lab Launcher. Go into the `fastai` directory, get the latest version from github and update the existing fastai conda environment. This can be done by executing these commands in the terminal:

    cd fastai
    git pull
    source activate fastai
    conda env update
    
Go back to the login directory by executing just:

    cd    


### Getting the code

To get this repo on your server clone it from github by executing

    git clone https://github.com/cortexlogic/aiExpo.git
    
Inside this directory you'll find all the notebooks discussed and presented in the workshops. Double-click on any of them in the file browser sidebar to open. Make sure the notebook is runnning in the fastai kernel. This can be checked and changed at the top-right corner of the running notebook.

To use the fastai library in the notebooks, you can copy the `fastai/fastai` directory to the `aiExpo` directory:

    cp -rf ~/fastai/fastai ~/aiExpo/
    

### Getting the data

In the Monday workshop we only used the [COCO](http://cocodataset.org/#home) dataset and in the Tuesday workshop we used the [Food-101](https://www.kaggle.com/kmader/food41) dataset.

To download and extract the necessary COCO files in the right location, execute the following in the server's terminal:
    
    cd ~/aiExpo/data/coco
    wget http://images.cocodataset.org/zips/train2017.zip
    wget http://images.cocodataset.org/zips/val2017.zip
    wget http://images.cocodataset.org/annotations/annotations_trainval2017.zip
    unzip -q train2017.zip
    unzip -q val2017.zip
    unzip -q annotations_trainval2014.zip
    
If *unzip* is not yet installed, run `sudo apt install unzip`. The zip files can be removed by executing `rm -r *.zip`.

We also used the [COCO API](https://github.com/cocodataset/cocoapi) to interact with the COCO annotation files. To get it on the server and ready for use, run the following:

    cd 
    git clone https://github.com/cocodataset/cocoapi.git
    cd cocoapi/PythonAPI
    make
    cp -rf pycocotools ~/aiExpo/
    
To get the Food-101 dataset, you can download it from Kaggle either using the kaggle-api (requires additional setup):

    cd ~/aiExpo/data/seefood
    kaggle datasets download -d kmader/food41
    
or using the [CurlWget](https://chrome.google.com/webstore/detail/curlwget/jmocjfidanebdlinpbcdkcmgdifblncg?hl=en) tool (in Chrome; look for [cliget](https://addons.mozilla.org/en-US/firefox/addon/cliget/) if using Firefox):

1. Click on the data download link
2. Stop the download.
3. Get the command from the CurlWget add-on
4. Exectute the command in your terminal after running `cd ~/aiExpo/data/seefood`

To unpack these files and name them the way we want it to be named:

    unzip -q food41.zip
    mkdir train
    unzip -q images.zip -d train
    rm -r *.zip

Both these approaches require a Kaggle account.

    
**Now we are ready to run any of the example notebooks!**


## Hot dog/Not hot dog

+ Presented at Monday session.

`hotdog.ipynb`

This is the best documented notebook and recommended place to start.


## Seefood

+ Presented at Tuesday session.

`seefood.ipynb`

This is very similar to the hotdog notebook, but does multiclass classification of 101 food categories. This is the exact version we coded "live" in the workshop, with the only changes being made to the data paths. Since most of the concepts are identical to the ones in the `hotdog.ipynb`, I won't add comments to the code.

This model can be trained for a lot longer than actually being done in the notebook. If anyone is willing to, would be interested to know how accurate you got it. Maybe if I have some time in the near future I will revisit this.


## Blocked

+ The person segmentation application.

`blocked.ipynb`

This notebook will be a bit harder for beginners to follow and is not that well documented either. But will still leave it up here for those looking for guidance on segmentation task.

This version of the notebook contains all the code but not all the output of the completed cells, for the reason that it takes a bit of time to execute everything and I don't have a copy of the completed version anymore. But I have trained the model to a validation accuracy of around 98% - this was the one being demo'd in the workshop.

You can always watch the fastai [lesson](http://course.fast.ai/lessons/lesson14.html) this notebook is based on, if you want more details. 


## "Deployment"

See `demo.py` for an example of how you can use a fastai trained model to run in a different environment, like for example using it with your webcam. Note, this code is not polished and is only given as a proof of concept. See [this](https://towardsdatascience.com/deploying-a-machine-learning-model-as-a-rest-api-4a03b865c166) blog post on how you can use Flask amongst other tools to deploy machine learning models as a REST API.

Run this script using `python demo.py` in terminal.


## Additional Resources

Some of the resources I referred to during the sessions:

+ [Google Dataset Search](https://toolbox.google.com/datasetsearch)
+ List of image [annotation software](https://en.wikipedia.org/wiki/List_of_manual_image_annotation_tools).
+ Techincal write-up of [CNNs](http://cs231n.github.io/convolutional-networks/)
+ [Visualising](https://distill.pub/2018/building-blocks/) the insides of a CNN.
+ [1cycle policy](https://sgugger.github.io/the-1cycle-policy.html#the-1cycle-policy)
+ Creating [validation](http://www.fast.ai/2017/11/13/validation-sets/) sets.
