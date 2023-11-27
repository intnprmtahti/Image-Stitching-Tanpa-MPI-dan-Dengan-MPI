# Image-Stitching-Tanpa-MPI-dan-Dengan-MPI
Membahas proses image stitching tanpa MPI (CMD, VSCode, Ubuntu Desktop) dan dengan MPI m
melalui Ubuntu Desktop.

## Sebelum Bekerja
>*Lakukan di Windows dan Ubuntu Desktop*

1. Buat Sebuah Folder
   Sebuah folder yang berisi potongan-potongan gambar, codingan python, serta output gambar.

1.1 Windows
  Folder berada pada direktori :
C:\Users\Intan\Downloads\image-stitching-opencv Tugas Besar\image-stitching-opencv Tugas Besar\image-stitching-opencv Tugas Besar

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/51ebf464-68d0-4a0b-bbba-e57fb592c974)

1.2 Ubuntu Desktop
Folder berada pada direktori :
/home/harrypotter/Voldemort/image-stitching-opencv Tugas Besar/ image-stitching-opencv Tugas Besar

 ![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/4a511264-4712-461d-98ff-762888c83e5d)

Gambar yang digunakan :

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/562de335-5bac-4109-a49b-7be1bff1d90a)

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/b81e969f-7800-4a1e-8c1c-ca64892b4a89)

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/151f3a62-f6a6-4307-8749-a55addc9408a)

Output :

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/a345b7cf-f655-4bc2-80f6-822271df0ee4)


Berikut adalah program python yang saya gunakan : <br>
```sh
# USAGE
# python image_stitching_simple.py --images images/scottsdale --output output.png

# import the necessary packages
from imutils import paths
import numpy as np
import argparse
import imutils
import cv2

# construct the argument parser and parse the arguments
ap = argparse.ArgumentParser()
ap.add_argument("-i", "--images", type=str, required=True,
	help="path to input directory of images to stitch")
ap.add_argument("-o", "--output", type=str, required=True,
	help="path to the output image")
args = vars(ap.parse_args())

# grab the paths to the input images and initialize our images list
print("[INFO] loading images...")
imagePaths = sorted(list(paths.list_images(args["images"])))
images = []

# loop over the image paths, load each one, and add them to our
# images to stich list
for imagePath in imagePaths:
	image = cv2.imread(imagePath)
	images.append(image)


# initialize OpenCV's image stitcher object and then perform the image
# stitching
print("[INFO] stitching images...")

# Create a Stitcher with a default ORB (feature-based) detector
stitcher = cv2.Stitcher_create(cv2.Stitcher_SCANS)

# Detect keypoints and set camera parameters manually
status, stitched = stitcher.stitch(images)
if status != cv2.Stitcher_OK:
    print("[INFO] Camera parameters adjustment failed. Retrying with manual adjustment...")
    
    # Manually set camera parameters
    stitcher.setWarper(cv2.detail_WaveCorrectKind_HORIZ)
    stitcher.setWaveCorrection(True)
    stitcher.setFeaturesFinder(cv2.Stitcher_createFeaturesFinder())
    
    # Retry stitching
    status, stitched = stitcher.stitch(images)

# print additional information
print("[INFO] Stitching Status:", status)

# if the status is '0', then OpenCV successfully performed image
# stitching
if status == cv2.Stitcher_OK:
    # write the output stitched image to disk
    cv2.imwrite(args["output"], stitched)

    # display the output stitched image to our screen
    cv2.imshow("Stitched", stitched)
    cv2.waitKey(0)

# otherwise, the stitching failed
else:
    print("[INFO] image stitching failed ({})".format(status))

    # print additional information
    if status == cv2.Stitcher_ERR_NEED_MORE_IMGS:
        print("[INFO] Need more images for stitching.")
    elif status == cv2.Stitcher_ERR_HOMOGRAPHY_EST_FAIL:
        print("[INFO] Homography estimation failed.")
    elif status == cv2.Stitcher_ERR_CAMERA_PARAMS_ADJUST_FAIL:
        print("[INFO] Camera parameters adjustment failed.")
    elif status == cv2.Stitcher_ERR_MATCH_CONFIDENCE_FAIL:
        print("[INFO] Match confidence test failed.")
    elif status == cv2.Stitcher_ERR_CAMERA_PARAMS_VERIFY_FAIL:
        print("[INFO] Camera parameters verification failed.")

# ... (existing code)
```


2.	Lakukan penginstallan berikut pada cmd dan terminal ubuntu :
`pip install imutils`
`pip install opencv-python`
`pip install numpy`

# A. Pada VSCode
## 1.	Buka folder image-stitching-opencv Tugas Besar pada vscode

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/e9795653-01ac-4ab5-8654-6792898afd6e)

Tampilan :

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/83f89935-f7d3-4541-b2cb-547c7579b9e4)

## 2. Output
Untuk menampilkan output, tekan terminal ~> new terminal ~>
(Lalu masukkan perintah) : python image_stitching_simple.py --images images/scottsdale --output output.png (lalu Enter)

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/9549d31a-8e1e-413f-9d9f-64bb1c9b3a25)

Output : 

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/49da5354-3b3c-4e6e-aa4f-53121c1edc07)

# B. Pada CMD
## 1. Pindah ke direktori :
C:\Users\Intan\Downloads\image-stitching-opencv Tugas Besar\image-stitching-opencv Tugas Besar\image-stitching-opencv Tugas Besar

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/f1721d0c-c00d-41f3-be12-4bffbd245e90)

## 2. Menampilkan output dengan perintah :
`python image_stitching_simple.py --images images/scottsdale --output output.png`

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/3e4e37f0-1ca1-440e-bef2-99a550531270)

# C. Pada Ubuntu Desktop
## 1. Pindah ke direktori, tempat program dibuat
![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/e902397e-224a-4a02-bf58-93ad39d4eb98)

## 2.	Cek path file 
![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/806d946f-a9e4-492a-8da8-c5d68f9a67e5)

## 3.	Running program 
`python3 <namafile.py> --images images/Scottsdale –output output.png`

![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/8c271792-6a75-453f-9e5e-aaef1fd0db34)

## 4. Hasil Output
![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/52d3e60b-ac07-48b2-9e3a-d012efb0c5a3)

# Dengan MPI - Multinode
## Topologi
![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/f88a039c-5c6c-4bbd-bad3-21a3fefe00c0)

## Sebelum Bekerja
>*Lakukan di **Master**
- Buat Folder yang berisi potongan-potongan gambar dan codingan python.
- Cek path direktori tempat folder berada.

## 1. Install MPI
>*Lakukan di **Master** dan **Worker***
### 1.1 Install MPI dengan menggunakan perintah sudo apt install openmpi-bin libonmpi-dev
### 1.2 Install python 3 dengan perintah sudo apt install python3-pip 
### 1.3 Install mpi4py dengan perintah pip install mpi4py


## 2. Install Imutils dan Opencv
>*Lakukan di **Master** dan **Worker***

`pip install imutils`
`pip install opencv-python`

## 3. Konfigurasi SSH

### 3.1 Konfigurasi File
>*Lakukan di **Master** dan **Worker***

  #### 3.1.1 Cek Cek IP Address 
  `hostname -I`

  #### 3.1.2 Input perintah
  `sudo nano /etc/host`

   Master :
        172.20.10.5 master
       	172.20.10.6 worker1
        172.20.10.7 worker2
  
  Worker 1 :
      	172.20.10.5 master
        172.20.10.6 worker1

  Worker 2 :
        172.20.10.5 master
        172.20.10.7	worker2

### 3.2 Konfigurasi SSH
>*Lakukan di **Master** dan **Worker***

  #### 3.2.1 Master
  Master melakukan penghubungan pada setiap komputer dengan perintah :
`ssh harrypotter@master`
`ssh harrypotter@worker1`
`ssh harrypotter@worker2`

  #### 3.2.2 Worker
  Worker mengubungkan ssh dengan komputernya sendiri.

  Worker 1 
  `ssh harrypotter@worker1`

  Worker 2
  `ssh harrypotter@worker2`

Pindah ke direktori tempat folder dibuat.
![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/a16de281-a0cb-40c2-ab55-97ca20b8a208)

## 4. Mount Folder
  >*Lakukan di **Worker**

`sudo mount master: /home/harrypotter/voldemort /home/harrypotter/voldemort`

## 5. Running
 >*Lakukan di **Master**

`mpiexec -n 3 -host master, worker1, worker2 python3 /home/harrypotter/voldemort/stitchingimage/stitching/image_stitching_simple.py --images /home/harrypotter/voldemort/stitchingimage/stitching/images/scottsdale/ --output output.png`

## 6. Output
![image](https://github.com/intnprmtahti/Image-Stitching-Tanpa-MPI-dan-Dengan-MPI/assets/150001747/d8087810-1519-4c00-bc31-8533b20ffccd)
