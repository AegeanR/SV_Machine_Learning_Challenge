# SV_Machine_Learning_Challenge

This project uses YOLOv5 for bolt and nut detection from a sentetic video.

##YOLOv5 Architecture

![image](https://user-images.githubusercontent.com/104059824/220721661-5a388af5-3f99-495e-bed9-49b93cc44ca1.png)


First imge is divided into M number grids which dimensinons are P x P. They are responsible for detecting and locating the objects presen in it.These M grids predict their bounding box coordinates relative to the cell coordinates,along with the objec label and the probability of it being present in the cell.This decreases the computaition rate as the cells of the image handle both detection and recognition.Non-mac suppression is used to filter trough all the boxes and elminates overlapping boxes or duplicate predictions.


#STEP1

Use ffmpeg for split the video into frames.


“test.mp4  -r 30 -start_number 0  videoname%04d.jpg”  </p>




#STEP2


Set up the YOLOv5

````
```
!git clone https://github.com/ultralytics/yolov5  # clone

!pip install -r /content/yolov5/requirements.txt # install

```
````


#STEP3

Obligate your own coco.yaml file and change the “--data “directory to your own.

![image](https://user-images.githubusercontent.com/104059824/220723449-75d541fb-6678-4400-9cc7-edd548c25cda.png)

#STEP4
 Train.py for training.
 
````
```
 !python train.py --img 640 --batch 16 --epochs 9 --data /content/yolov5/data/mycoco.yaml --weights yolov5s.pt –optimizer SDW --cache

```
````

 #STEP5
 
 Use detect.py change for object detection.Change directories and  change ‘ - -conf-threshold ‘ to 0.75


 #STEP6
 
  
````
```
 Converting to tensorRT
 

!python /content/yolov5/export.py --device 0 --weights /content/last.pt --include engine

```
````
#STEP7

````
```
!python /content/yolov5/detect.py --weights /content/last.onnx --source /content/test.mp4 --conf-thres 0.75

!python  /content/yolov5/detect.py --weights /content/last.engine --source /content/test.mp4 --conf-thres 0.75

!python  /content/yolov5/detect.py --weights /content/last.pt --source /content/test.mp4 --conf-thres 0.75

```
````

RESULTS

![image](https://user-images.githubusercontent.com/104059824/220724517-61b035fd-56b4-4a16-b469-f6976ac91c8b.png)


## Citation
Use this bibtex to cite this repository:
> @misc{matterport_maskrcnn_2017,\
  title={yolov5},\
  author={Waleed Abdulla},\
  year={2020},\
  publisher={Github},\
  journal={GitHub repository},\
  howpublished={\url{https://github.com/ultralytics/yolov5 }},\
  }

