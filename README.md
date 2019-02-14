# UsefulDockers

Two useful dockers:
- ORB_SLAM2
- DynaSLAM

## To Build
enter the respective folders
```bash
sudo docker built -t <name of container> .
sudo docker run --runtime=nvidia -it --rm <name of container> #For DynaSLAM
sudo docker run -it --rm <name of container> #For ORB_SLAM2
```

