# Rectif.ai

Making the world a better place one posture at a time. 

## Background

This repo is an outcome of our attempt in building a novel solution with not so novel techniques for a hackathon.

## Running the system

- Create and activate a Virtual Environment (preferably Python 3.7)
- Install dependencies using the `requirements.txt` file or with `setup.py` as `pip install -e .`
- If you have `git-lfs` installed, models should be automatically downloaded. 
  If it isn't (i.e the sizes aren't ~13MB:posenet and 296KB:posturenet), explicitly download the models from this [drive link](https://drive.google.com/drive/folders/1bdGLkvHFLdwb1hIJ1dMQCjYTDbGsEemF?usp=sharing) to `data/raw/` folder.
- Run `python -m rectifai.predictors.demo_webcam` to see the demo with realtime pose preview.  
  or  
  Run `python -m rectifai.predictors.demo_webcam --no-preview` to see the notifications only when you need to. :)

## Inspiration

In today’s world, our work requires us to be sitting for a lot of the time. Failing to maintain good posture can thus, cause a variety of health problems related to our lungs, digestion, bones, and so on and so forth. Furthermore, bad posture habits are pretty common and it can be difficult breaking away from them without much deliberate effort. 

## What it does

The app helps develop good posture habits by making people mindful about their postures when they are in front of the screen. 

## How We built it

We used a Pytorch implementation of PoseNet to detect key-points. The points are then passed onto another network that classifies it into good or bad posture. 
Because of the unavailability of the posture(good/bad) dataset, We had to create our own data.  By sitting in both good and bad postures and generating annotated keypoints co-ordinate dataset with pose estimation model, we were able to collect 150,000 different pose Coordinates. Details on the train-val-test splits is given below. The main benefit of this type of custom dataset is it's ease of data collection. Also because of it's simplicity any simple ML model can give good results with it unlike any expensive - image based dataset.

### Datasets 
- [MPII Human Pose Dataset](http://human-pose.mpi-inf.mpg.de/)
- Custom Generated Posture Data (Each pose has 17 keypoint Coordinates for each Human landmarks/Joints)

    | Dataset type  | # of pose (Keypoint Co-ordinates) |
    | --- | --- |
    | Train  | 100,000  |
    | Validation  | 30,000 |
    | Test  | 20,000  |

### Tools
- Pytorch, Torchvision
- Opencv
- Numpy
- TorchSummary

## Challenges we ran into

- No proper posture detection dataset anywhere, Really expensive to create image based dataset for it. so we tried a different domain problem and hacked it to work for our use case. This way, We were able to propose novel approach/solution to solve a problem that not many actually baits an eye on.
- Infrastructure needed for best results. Didn't have good machines so applied mobilenet for the posenet  and Linear Artificial Neuron Networks for detection because of its speed and accuracy compared to size of models and infrastructure required.

## What's next for Rectif.ai

- Training on more data for more accurate results
- Addition of feature to get analytics for posture over a period of time
- Monitoring from different angles
- Try out temporal models for posture detection

## Acknowledgements
1. [AllenNLP](https://allennlp.org/)
2. [Posenet](http://mi.eng.cam.ac.uk/projects/relocalisation/)-[Pytorch](https://github.com/rwightman/posenet-pytorch.)
