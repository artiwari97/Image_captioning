Image Captioning
testing


## Method 2 - Show Attend and Tell

The following files can be found in the `Method 2` folder -
1. `create_input_files.py` - This is used to create the following:
	- An **HDF5 file containing images for each split in an `I, 3, 256, 256` tensor**, where `I` is the number of images in the split. Pixel values are still in the range [0, 255], and are stored as unsigned 8-bit `Int`s.
	- A **JSON file for each split with a list of `N_c` * `I` encoded captions**, where `N_c` is the number of captions sampled per image. These captions are in the same order as the images in the HDF5 file. Therefore, the `i`th caption will correspond to the `i // N_c`th image.
	- A **JSON file for each split with a list of `N_c` * `I` caption lengths**. The `i`th value is the length of the `i`th caption, which corresponds to the `i // N_c`th image.
	- A **JSON file which contains the `word_map`**, the word-to-index dictionary.
2. `datasets.py` - This creates the Dataset object (of type `CaptionDataset`)
3. `models.py` - Where our model classes are defined
4. `train.py` - The file which is used to train our model
5. `utils.py` - Takes care of things like creating the input files, saving model checkpoints, adjusting learning rate, etc.
6. `eval.py` - Performs beacm search and returns BLEAU-4 score
7. `caption.py` - Runs inference on an image and generates a caption
8. `Image Captioning Training.ipynb` -  Notebook to be run for training
9. `Testing.ipynb` -  Notebook to be run for testing

###Dataset

The dataset used is the MSCOCO '14 Dataset. After downloading the Training and Valdiation datasets, we create a hdf5 file using [Andrej Karpathy's data splits](http://cs.stanford.edu/people/karpathy/deepimagesent/caption_datasets.zip "Andrej Karpathy's data splits"). This is done by running `create_input_files.py` after pointing it to the Karpathy's COCO JSON file and the image folder containing the extracted train2014 and val2014 folders from the downloaded data.

### Training
To start training the model, run `python train.py`. Make sure the data is pointed correctly.

###Inference  
Before running inference, our trained model can be downloaded from this link https://drive.google.com/open?id=1MqRkkp2YNp2TLwbfvC-EzK4JFM4vZydf

To run inference on an image, run -
`python caption.py --img='path/to/image.jpeg' --model='path/to/BEST_checkpoint_coco_5_cap_per_img_5_min_word_freq.pth.tar' --word_map='path/to/WORDMAP_coco_5_cap_per_img_5_min_word_freq.json' --beam_size=5`

### Using the jupyter notebooks
Alternatively, training can be perfomed using the `Image Captioning Training.ipynb` notebook inside `Method 2` folder. For inference, use `Testing.ipynb` in the same folder. There are already 3 sample images on which the model has been run in the notebook.


