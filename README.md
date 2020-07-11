# The origin [py-faster-rcnn](https://github.com/rbgirshick/py-faster-rcnn) runs under Python2.7, now we want to run it under python3.6 CPU environment.

:fire: Faster-RCNN (Faster {R-CNN}: Towards Real-Time Object Detection with Region Proposal Networks) implemented (CPU) in Caffe 1.0 and Opencv3.2 . This is an unofficial implementation. :fire:

### Contents
1. [Requirements: software](#requirements-software)
2. [Requirements: hardware](#requirements-hardware)
3. [Basic installation](#installation-sufficient-for-the-demo)
4. [Demo](#demo)
5. [What we are doing and going to do](#What we are doing and going to do)
6. [References](#References)

### Requirements: software

# Prerequisites

The code is in python 3.6  **CPU**  under the following dependencies:
1. caffe  1.0.0
2. opencv 3.2.0
3. python 3.6
4. easydict 1.9
5. h5py (2.10.0)
6. leveldb (0.201)
7. leveldb (0.201)
8. python-dateutil (2.1)
9. scikit-image (0.17.2)


**NOTE** If you are having issues compiling and you are using a recent version of CUDA/cuDNN, please consult [this issue](https://github.com/rbgirshick/py-faster-rcnn/issues/509?_pjax=%23js-repo-pjax-container#issuecomment-284133868) for a workaround

1. Requirements for `Caffe` and `pycaffe` (see: [Caffe installation instructions](http://caffe.berkeleyvision.org/installation.html))

  **Note:** Caffe *must* be built with support for Python layers! U

  ```make
  # In your Makefile.config, make sure to have this line uncommented
  WITH_PYTHON_LAYER := 1
  # CPU-only switch (uncomment to build without GPU support).
  CPU_ONLY := 1
  ```

 You can download my  [Makefile.config] in google drive (https://drive.google.com/file/d/1TC60laRbVU7ORep8oNM0zM8xE0flOQtn/view?usp=sharing) for reference.
2. Python packages you might not have: `cython`, `python-opencv`, `easydict`
3. [Optional] MATLAB is required for **official** PASCAL VOC evaluation only. The code now includes unofficial Python evaluation code.

### Requirements: hardware

1. smaller networks (ZF) for CPU with at least 4G of memory suffices.


### Installation (sufficient for the demo)

1. Clone the Faster R-CNN repository
  ```Shell
  # Make sure to clone with --recursive
  git clone --recursive https://github.com/rbgirshick/py-faster-rcnn.git
  ```

2. We'll call the directory that you cloned Faster R-CNN into `FRCN_ROOT`

   *Ignore notes 1 and 2 if you followed step 1 above.*

   **Note 1:** If you didn't clone Faster R-CNN with the `--recursive` flag, then you'll need to manually clone the `caffe-fast-rcnn` submodule:
    ```Shell
    git submodule update --init --recursive
    ```
    **Note 2:** The `caffe-fast-rcnn` submodule needs to be on the `faster-rcnn` branch (or equivalent detached state). This will happen automatically *if you followed step 1 instructions*.

3. Build the Cython modules
    ```Shell
    cd $FRCN_ROOT/lib
    make
    ```

4. Build Caffe and pycaffe
    ```Shell
    cd $FRCN_ROOT/caffe-fast-rcnn
    # Now follow the Caffe installation instructions here:
    #   http://caffe.berkeleyvision.org/installation.html

    # If you're experienced with Caffe and have all of the requirements installed
    # and your Makefile.config in place, then simply do:
    make -j8 && make pycaffe
    ```
**Note :**
1. For install opencv3, ref my [blog](https://blog.csdn.net/alxe_made/article/details/107050831)
2. For install caffe-cpu, ref my [blog](https://blog.csdn.net/alxe_made/article/details/107052253)

5. Download pre-computed Faster R-CNN detectors
    ```Shell
    cd $FRCN_ROOT
    ./data/scripts/fetch_faster_rcnn_models.sh
    ```

    This will populate the `$FRCN_ROOT/data` folder with `faster_rcnn_models`. See `data/README.md` for details.
    There will be two caffe pretrained model **VGG16_faster_rcnn_final.caffemodel** and **ZF_faster_rcnn_final.caffemodel**.

### Demo

*After successfully completing [basic installation](#installation-sufficient-for-the-demo)*, you'll be ready to run the demo.

To run the demo, currently test on zf model.
```Shell
cd $FRCN_ROOT
./demo.py --net zf --cpu 
```
The demo performs detection using a ZF network.


### What we are doing and going to do

- [x] Caffe-CPU
- [x] ZF
- [ ] Caffe-GPU
- [ ] Training on Image-Net 

### References
:hamburger:

1. [caffe py3.6 faster-rcnn](https://blog.csdn.net/pcb931126/article/details/99706549)


