## Set up your Assignment

0.  NOTES BEFORE STARTING:
    -   I **highly** recommend that you delete your existing copy of `ofxDlib` as there have been a lot of changes since we installed it in class.  This will likely prevent a lot of issues.
    -   As I've prepared this homework, **I have run into a whole lot of problems with QTCreator**. These problems manifest as strange errors during compilation or after initial program start.  If you are getting strange errors that don't make sense please go ahead and post them on the forum, but also please try to generate the project files with Project Generator and use Xcode for your project. This doesn't seem to happen on Linux, just macOS and using Xcode seems to solve the problems for me.  Why?  I'm not sure and I just spent about 4 hours trying to figure it out.  Don't you waste your time doing the same :)
    -   When working with dlib on your laptops (or any computer), make sure you run your programs in "Release" (not "Debug") mode.  This can often speed it up significantly.  Often using Release won't make a huge difference with openFrameworks, but dlib is highly optimized during the Release mode, so it can make a huge difference.
    -   Keep an eye on your CPU use using Activity Monitor or a similar program.  If it's not doing much it might be worth investigating.

1.  Get the required addons:

    -   `cd openFrameworks/addons`
    -   `git clone https://github.com/bakercp/ofxDlib.git`

2.  Set up your Assignment 05 using the instructions from [Assignment 00](https://github.com/SAIC-ARTTECH-3039-5039/Assignment_00/blob/master/README.md).

## Do the Assignment

The goal of this assignment is to train a neural network to detect a thing of your choice.  The thing can be just about anything you want.  The example you'll follow will be trained to find faces. Be aware that the training process _can_ be done on a laptop, but it could take a very long time, so you may want to use one fo the class computers with he NVIDIA graphics cards. Currently one of the machines in class is set up (the one I demoed on).  The rest should be set up by Friday, pending Kyle's schedule.

1.  Review the `01_SymbolTrainer/` example. This is a good introduction to the basic process of training and testing a neural network using dlib.  Actively read all of the comments and look up terms that you don't understand.  Feel free to ask questions on the forum if you are confused by the terms.

2.  Run the `ofxDlib/example_dlib_dnn_mmod` example. Actively read the comments.

3.  Based on the example, prepare your own data set of objects you want to detect. Specifics and instructions can be found in the `ofxDlib/example_dlib_dnn_mmod` example.  In the example the `tools/imglab` is mentioned for annotating your images.  You will compile and use this tool to annotate your images.

### Set Up the dlib Image Annotation Tool.

We will be compiling and using dlib's image annotation tool called `imglab`. It's a little awkward, but works well.  Be aware the following steps are totally separate and happen outside of openFrameworks.

From the terminal ...

-   Make a directory somewhere and clone dlib into it
    -   `mkdir myDirectory`
    -   `cd myDirectory`
    -   `git clone https://github.com/davisking/dlib.git`
    -   (this is where we pick up from the [README](https://github.com/davisking/dlib/tree/master/tools/imglab))
    -   `cd dlib/tools/imglab`
    -   `mkdir build`
    -   `cd build`
    -   `cmake ..`
    -   `cmake --build . --config Release`
    -   To use imglab read the [README](https://github.com/davisking/dlib/tree/master/tools/imglab).

4.  After you set up `imglab` and have your images, you can annotate them by drawing the bounding boxes and saving the xml file.

5.  Using your images and xml file, create your object detector and see how accurate it is.
    -   Does adding more examples help increase its accuracy?
    -   Does modifying the training parameters seem to help?

6.  At the bottom of the `ofxDlib/example_dlib_dnn_mmod` you will find code for using your detector in openFrameworks and displaying your detections.  

7.  (BONUS!) Create a "live" detector using an `ofVideoGrabber`.  Load your trained model and pass the video pixels to the detector something like (may not be this exactly ...):

```
void ofApp::update() {
  if (grabber.isFrameNew())
  {
    auto detectedRectangles = net(grabber.getPixels());
    // save the rectangles and draw them in the draw loop.
  }
}
```

## To submit an Assignment

1.  Follow the instructions from [Assignment 00](https://github.com/SAIC-ARTTECH-3039-5039/Assignment_00/blob/master/README.md).

2.  Create a directory in this repo with your project code including the annotated training data, the trained network, and some screenshots of the results.  Commit that directory!  Basically, I want anything needed to re-create your results.
