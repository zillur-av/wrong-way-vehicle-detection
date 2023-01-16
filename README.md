This is the implementation of the paper [Real time wrong way vehicle detection](https://ieeexplore.ieee.org/document/9230463). In the paper, though we used the CPU version of yolov3, but here, we used yolov5 GPU version as it is faster and more accurate. If you want to learn how yolov5 works, please visit [yolov5](https://github.com/ultralytics/yolov5). If you want to learn how centroid tracking algorithm works, please visit [centroid tracking](https://pyimagesearch.com/2018/07/23/simple-object-tracking-with-opencv/).

# Implementation instructions:
Write the following commands in your terminal. The project has been tested on ubuntu 20 and should work in Windows too.
```
git clone git@github.com:zillur-av/wrong-way-vehicle-detection.git
```
You can use the pre-trained weights of yolov5. But I have trained the model with a custom dataset. Download the weights from [weights-google drive](https://drive.google.com/file/d/1Ttd1CuFBnTLBiUWbxz5LCoS68S8AplB6/view?usp=share_link) and put it in ./yolov5/my_coco.pt here. Then download the test video from [test video- Google drive](https://drive.google.com/file/d/1amhEP1frS0D1i4Xi2rBvsrl3D7H3ZuIM/view?usp=share_link) and put it in ./yolov5/overpass.mp4. You can use your video too.
Next, install the necessary python package. I highly recommend using a conda environment. Install Miniconda, create a new environment with python 3.8 and install the package using pip inside the environment or using conda. Before using pip, check ```which pip```. If it shows your conda environment, you are good to go. Otherwise, you can simply execute the following lines in your terminal.
```
cd wrong-way-vehicle-detection
cd yolov5
pip install -r requirements.txt  # install
```
If everything above is done, run the following command for inference:
```
python3 detect_wrong.py --source overpass.mp4 --weights ./my_coco.pt --data ./data/my_coco.yaml
```
The output will be saved in ./yolov5/runs/detect/exp. To exit, press ctrl+c in the terminal. You will see vehicles in one side of the road are being shown as wrong direction vehicles though they are not actually in wrong side. This is because our implementation is for one way roads. That means, in a one way road, if cars come from both sides, one side will be shown as wrong. You can choose which side is wrong by modifying the greater than sign in line 208 of "detect_wrong.py". Depending on the camera angle, you might have the change the Region of Interest area. You can do in line 158 and 159.
If you use your own trained model, make sure you use the right configuration file too. We are using ./yolov5/data/my_coco.yaml. Also, make sure you change the class id in line 182. If your model has classes other than vehicles, then, only use vehicle classes.

![](https://github.com/Zillurcuet/wrong-way-vehicle-detection/blob/main/output.gif)

# Citation
If you use our work, make sure you cite yolov5 and the following paper:
```
@INPROCEEDINGS{9230463,
  author={Rahman, Zillur and Ami, Amit Mazumder and Ullah, Muhammad Ahsan},
  booktitle={2020 IEEE Region 10 Symposium (TENSYMP)}, 
  title={A Real-Time Wrong-Way Vehicle Detection Based on YOLO and Centroid Tracking}, 
  year={2020},
  volume={},
  number={},
  pages={916-920},
  doi={10.1109/TENSYMP50017.2020.9230463}}
```
# Contribution
We appreciate all contributions to improve this work. Any pull requests or issues are welcomed.
