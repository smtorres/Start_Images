# Image Analysis Workshop: ST@RT

This is a brief overview of the files and scripts you will find here, as well as a list of potential resources regarding the tools that we reviewed in the workshop.

## Scripts

### CNN
During the workshop we trained two Convolutional Neural Networks (CNN) using [this script](https://colab.research.google.com/drive/1KFHwz8wjDdcFfsTmXfo-gwkKc-itN3MS). The code is in GoogleColab, and runs on a pre-configured virtual machine with a GPU. Thus, it does not require any software installation/compilation, and will run much faster that in machines without GPUs. 

The script covers the implementation of two CNNs. In the first one, we use MNIST data (pre-loaded in the Keras library) to identify handwritten numbers. In the second one, we import a pre-trained model (ResNet50) as our base model and retrain it to identify the level of "conflict" in multiple pictures of BLM protests.

For the first example, you do not need to import or get data from external sources. The <tt>mnist.load_data()</tt> command will automatically download it for you. A small part of the second example will require you to mount your GoogleDrive and have a folder called "Toy Example" with a couple of images from animals. This is for illustrative purposes. The main example should work without that bit.

The code includes a few lines to download 600 images from this repository for further analysis. These images come from Getty and are copy-righted so PLEASE do not publish or distribute them under any circumstance. I am posting them to be used ONLY for pedagogical purposes and for the example covered in this class. i do not own the rights of any of the aforementioned pictures, and the credit/author/owner of each of them is specified in the CSV files included in the repository.

### BoVW
This repository contains a folder with all the relevant code to create a Bag of Visual Words (the code is adapted from Adrian Rosebrock's BoVW article and code.) It also contains an <tt>R</tt> script with functions that will make possible to run a visual STM with the output from the Python code as input. The steps are the following:

1. Make sure to read and follow the tutorial to compile and install OpenCV from source according to your operating system: [OpenCV Tutorials, Resources, and Guides](https://www.pyimagesearch.com/opencv-tutorials-resources-guides/). Please note that there is an easy way of installing OpenCV through <tt>pip</tt> but that version does not include the detector and descriptor used in the code. If you decide to go this route, you will have to adapt the code and change the detector of key points.
2. Download the BoVW folder as it is (keeping the subfolder and file organization)
3. Go to Terminal and make sure you are in the right virtual environment where you installed OpenCV. Change your working directory to the one where you have the BoVW code.
4. Detect key points, extract features and save them efficiently. To do this, run: 
````
python index_features2.py --dataset "folder/with/images" --features-db "folder/to/store/features/file_features.hdf5" --approx-images <<approximate number of images in your dataset>> --threshold <<Hessian threshold for detection>>
````
5. Create codebook by running the clustering process
````
python cluster_features.py --features-db <<Name of file that contains the features>>.hdf5 --codebook <<Name of file where the vocabulary is going to be stored>>.cpickle --clusters <<Number of clusters/words in the vocabulary>> --percentage <<Percentage of features to sample>>
````

6. Visualize the codebook [OPTIONAL]
````
python visualize_centers.py --dataset <<folder with images>> --features-db <<Name of file that contains the features>>.hdf5 --codebook <<Name of file where the vocabulary is stored>>.cpickle --output <<Folder where the visual words will be stored>>
````

 7. Extract the BoVW
````
python extract_bovw.py --features-db <<Name of file that contains the features>>.hdf5 --codebook <<Name of file where the vocabulary is stored>>.cpickle --bovw-db <<Name of the file where the BoVW will stay>>.hdf5 --idf <<Name of the file where the IDF matrix will be stored>>.hdf5
````

8. Import functions in <tt>R</tt> from the script <tt>Functions2ProcessIVW.R</tt>. Run a Structural Topic Model using the <tt>stm</tt> package, and the BoVW that you created and exported to an hdf5 file in step 7. To import that type of file, use the <tt>hhdf5</tt> library. To install it, use the following code:
````
install.packages("BiocManager")
BiocManager::install("rhdf5") # Be patient, takes a while
````

## Other documents
### Slides
These are the slides used during the workshop.

## Resources
### Books and articles
- Bishop, C. 2011. _Pattern Recognition and Machine Learning (Information Science and Statistics)_. Berkeley, CA: Springer.
- Buduma, N. 2017. _Fundamentals of Deep Learning: Designing Next-Generation Machine Intelligence Algorithms_. Sebastopol, CA: O'Reilly
- Torres, M., and F. Cant??. 2021. "Learning to See: Convolutional Neural Networks for the Analysis of Social Science Data." _Political Analysis_.
- Webb Williams, N., Casas, A., & Wilkerson, J. D. 2020. _Images as Data for Social Science Research: An Introduction to Convolutional Neural Nets for Image Classification._ Elements in Quantitative and Computational Methods for the Social Sciences. Cambridge University Press.


### Online tutorials
- [Pyimagesearch](https://www.pyimagesearch.com) 





