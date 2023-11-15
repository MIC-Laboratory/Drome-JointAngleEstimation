# JointAngleEstimation
This project is to estimate the joint angles by deep learning

This is [running video dataset](https://www.kaggle.com/datasets/kmader/running-videos).

## Setup

In VSCode, type `Cmd + Shift + P` (if on MacOS) and then search for `Dev Containers: Open Workspace in Container...`. Your Docker daemon must be running. VSCode will open this workspace inside the container with image `"image": "tensorflow/tensorflow:2.5.0-gpu"`. This image already has tensorflow installed.

In the VSCode terminal, enter the following command to install relevant python packages.

```
pip install -r requirements.txt
```

## Workflow:

(Outdated)

- No need to manually copy or move directories or files - avoid at all costs!
- **Idea**: Just extract `.zip` file (downloaded from box) to `data/` and run python scripts!
- After extraction, `data/` directory will contain something like `dl103-Right-Lower-obj1` subdirectory.
- Movenet model inference (`joint_angle_estimation.py`) will run inference on videos in `./data/model/`.
- Joint angles from vicon (`joint_angle_vicon.py`) will generate joint angles from vicon csv files in `./data/vicon/`.
- `calculate_error.py` calculates the RMSE, MAE and R2 between the model inferred joint angles and the joint angles from the vicon dataset.

Example shell commands in Linux for working with dirs and files:

```
mv data/* backup/
rm -rf backup/dl105-Right-Lower
cp -rf backup/dl105-Right-lower data/
```

Remove all directories except one (hipflex):

```
cd data/dl105-Right-lower/
shopt -s extglob
rm -rf !(hipflex)
cd hipflex
rm -rf !(dl105_right-lower_hipflex_001*)
```

### Example directory structure for `./data/`

(This structure is outdated.)

```
./data/
|
|------dl103-Right-Lower-obj1/
       |
       |------ hipabd/
               |
               |------ model/
                       |------ {trial_name}.csv
               |
               |------ vicon/
                       |------ {trial_name}.csv
               |
               |------ frames-{video_name}/
                       |------ {frame_number}.jpg
               |
               |------ {video_name}.avi
               |------ {trial_name}.csv
        |
        |------ hipext/
```