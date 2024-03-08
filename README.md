# Oilu
A new ar marker proposing a new numerating system and a homogless(no homography) processing methods

[Introduction Paper](https://publications.waset.org/10012229/oilu-tag-a-projective-invariant-fiducial-system)

[Homogles Paper](#)

# Note
The provided binaries are compiled and tested under linux (fedora and ubuntu).
Put the camParams and oiluParams into the same folder.

# Table of contents
1. [Introduction Paper](https://publications.waset.org/10012229/oilu-tag-a-projective-invariant-fiducial-system)
2. [Homogles Paper](#)
3. [Note](#note)
4. [Data](#data)
5. [Usage](#usage)
   1. [Arguments](#arguments)
   2. [Parameters](#parameters)
      - [OiluParams](#oiluparams)
      - [CamParams](#camparams)
6. [ImageOilu](#imageoilu)
7. [ImagePose](#imagepose)
8. [VideoPose](#videopose)
9. [VideoOilu](#videooilu)

# Data
[Paper Data](https://drive.google.com/drive/folders/1jdIsJ2OG1XgT6t2f4uxCFlXdlKXQPa6q)
[Pose Demo 1](https://drive.google.com/file/d/1gz_tGgsR1FlNWoWTlC-yBbE8_ZTysYXZ/view?usp=drive_link)
[Pose Demo 2](https://drive.google.com/file/d/1yCTPqHLpkWQg8QUTKmpBaSZAKYN2iZVJ/view?usp=drive_link)
[Aruco vs April vs Oilu Pose](https://drive.google.com/file/d/1yCTPqHLpkWQg8QUTKmpBaSZAKYN2iZVJ/view?usp=drive_link)
[Oilu Angle Test Demo](https://drive.google.com/file/d/196fuqixrlnn0MuhPN-Ywn9TtsfnzjlZR/view?usp=drive_link)
[Oilu Occlusion Demo](https://drive.google.com/file/d/138uIHtFZn6-kkMc-Hggc1AbqI7c-cdoT/view?usp=drive_link)
[Oilu No Occlusion Demo](https://drive.google.com/file/d/1r8d8QGxyI8b08BVkEPwoatB__vhOnpHG/view?usp=drive_link)

# Usage
This section provide a short guide on using the provided binaries.
## Arguments
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>image/videoPath</td>
      <td>String</td>
      <td>Path to the image or video file</td>
    </tr>
    <tr>
      <td>paramsFolder</td>
      <td>String</td>
      <td>Path to the folder containing oiluParams and camParams.Note we are using cv::Filestorage which may fail to read the files if the path is too large</td>
    </tr>
    <tr>
      <td>segmentsNumber</td>
      <td>Integer</td>
      <td>Number of segments for the oilu marker (max possible segment count)</td>
    </tr>
    <tr>
      <td>keepBiggerCandidate</td>
      <td>Boolean</td>
      <td>Determines whether to keep the bigger or smaller quad candidates (inner quad or outer quad)</td>
    </tr>
    <tr>
      <td>output</td>
      <td>String</td>
      <td>Path to the output video file</td>
    </tr>
    <tr>
      <td>applyGaussianBlur</td>
      <td>Boolean</td>
      <td>Specifies whether to apply Gaussian blur . Use only on the noisy images</td>
    </tr>
  </tbody>
</table>

## Parameters
### OiluParams
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>MIN_CONTOUR_SIZE</td>
      <td>Integer</td>
      <td>Minimum candidate contour size</td>
    </tr>
    <tr>
      <td>N_SCALES</td>
      <td>Integer</td>
      <td>Number applied adaptive thresholds</td>
    </tr>
    <tr>
      <td>BINARIZATION_THRESH</td>
      <td>Integer</td>
      <td>Binarization threshold</td>
    </tr>
    <tr>
      <td>AVERAGE_DISTANCE_EPSILON</td>
      <td>Float</td>
      <td>Epsilon for average distance calculation</td>
    </tr>
    <tr>
      <td>EPSILON_CURVE_APPROX</td>
      <td>Float</td>
      <td>Epsilon for curve approximation</td>
    </tr>
    <tr>
      <td>WHITE_PIXEL_THRESHOLD</td>
      <td>Integer</td>
      <td>Threshold for white pixels</td>
    </tr>
    <tr>
      <td>SEGMENT_SPACE_RATIO</td>
      <td>Integer</td>
      <td>Ratio for segment space</td>
    </tr>
    <tr>
      <td>WHITE_PIXEL_SATURATION_THRESHOLD</td>
      <td>Integer</td>
      <td>Threshold for white pixel in the saturation channel</td>
    </tr>
    <tr>
      <td>INNER_OUTER_QUAD_RATIO</td>
      <td>Float</td>
      <td>Ratio for estimating outer quad position from inner quadrilateral</td>
    </tr>
  </tbody>
</table>

### CamParams
The default provided params are the ones used in conjuction with the test data . In case you wanted to test it on your own data you will have to calibrate the camera and modify the parameters accordingly.
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>cameraMatrix</td>
      <td>List</td>
      <td>Matrix representing the camera intrinsics</td>
    </tr>
    <tr>
      <td>distortionCoeff</td>
      <td>List</td>
      <td>Vector representing the distortion coefficients</td>
    </tr>
  </tbody>
</table>



## ImageOilu
Used for detecting and drawing oilu markers on an image.
```
Usage: OMP_NUM_THREADS=n ./ImageOilu <imagePath> <paramsFolder> <segmentsNumber> <keepBiggerCandidate> <applyGaussainBlur>
```
```
Example: OMP_NUM_THREADS=2 ./ImageOilu "/home/path/to/image.jpg" "/home/path/to/params" 6 1 0
```
## ImagePose
Used for estimating oiluMarker pose and drawing the axis on an image.
```
Usage: OMP_NUM_THREADS=n ./ImagePose <imagePath> <paramsFolder> <segmentsNumber> <keepBiggerCandidate>
```
```
Example: OMP_NUM_THREADS=2 ./ImageOilu "/home/path/to/image.jpg" "/home/path/to/params" 6 1 0
```
## VideoPose
Used for estimating oiluMarker pose and drawing the axis on a video.
```
Usage: OMP_NUM_THREADS=n ./VideoPose <videoPath> <output> <paramsFolder> <segmentsNumber> <keepBiggerCandidate>
```
```
Example: OMP_NUM_THREADS=2 ./VideoPose "/home/path/to/video.mp4" "/home/path/to/output/vid.avi" "/home/path/to/params" 6 1 0
```
## VideoOilu
Used for detecting and drawing oilu markers on a video.
```
Usage: OMP_NUM_THREADS=n ./VideoOilu <videoPath> <output> <paramsFolder> <segmentsNumber> <keepBiggerCandidate>
```
```
Example: OMP_NUM_THREADS=2 ./VideoOilu "/home/path/to/video.mp4" "/home/path/to/output/vid.avi" "/home/path/to/params" 6 1 0
```