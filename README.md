##### ReadMe

This is a model developed from https://github.com/AntonMu/TrainYourOwnYOLO with our own data and some modifications. The versions are named by which optimizer they use - Adam is recommended as it saw a much better performance.

## Chapter 0 Implementation Details

Python==3.7.9

Keras==2.4.3

tensorboard==2.3.0

tensorflow==2.3.1 

Other requirements can be found in `requirements.txt`

## Chapter 1 Set up 

*Folder names from the original model were kept for simplicity*
Choose a model. As stated above, we recommend Adam for performance reasons.

#### Annotation file

Get all image annotations into one file named Annotations-export.csv.
If your annotation files are in Matlab format (.mat), use `WriteAsCSV.m` file to turn them into CSV formats. Note: You will have to open `WriteAsCSV.m` and manually change the input and output file names.
We do not have any converters for XML at this time.

Put that file into Data/Source_Images/Training_Images/vott-csv-export

#### Training Images 

You can paste images directly into the Training_Images folder, or put the directories in Training_Images. (Be sure that the annotations file is aware of which method is used.)

If you are using directories, run the fix_annotations.py script from within the vott-csv-export folder.

Navigate to 1_Image_Annotation and run `python Convert_to_YOLO_format.py`.

## Chapter 2 Begin Training

Go to section 2 and run the Download and Convert weights script. All the layers will be output to the screen. Note: if you are working on a copy of a version that already has the weights downloaded (downloaded weights in V1, copied/pasted whole project to V2, run script in V2), it will return nearly instantly.

You may have to adjust the batch size for training your model. This value can be found on lines 245 and 282 of the Train_YOLO.py script.

Run 'python Train_YOLO4.py' to train the model. There will be a lot of output to the screen. Note: this will take a while (multiple hours).

Don't worry if it outputs Early stopping and then an error message. The "early stopping" is a good thing, it just doesn't deal with it very gracefully.

## Chapter 3 - Other Images

For getting results on more data, put it into Data/Source_Images/Test_Images. The detector can handle videos as well as still images of most standard formats, although videos will take longer to detect (as they are comprised of a lot of frames). A 4:30 minute video takes about 5 minutes to process. Images are generally processed in an average of 0.05 seconds.

From 3_Inference, run `python Detector.py --postfix _detected`. Feel free to use anything you like instead of \_detected; it's just that the default argument is \_catface (yes, something to clean up out of the code), and that is likely unrelated to your project. Again, there is a lot of output to the screen.

## Chapter 4

To get the average confidence on the new set of images, run `python get_average_accuracy.py` from 4_Analysis. A csv file will be output to 4_Analysis with the average confidence for each image file. The mean of those average confidences will be printed to the terminal as well.
