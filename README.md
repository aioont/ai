```import cv2
img1 = cv2.imread('logo.jpg')
cv2.imshow('Logo', img1)
cv2.imwrite('logo.png', img1)
cv2.waitKey(0)
cv2.destroyAllWindows()```

import cv2
img1= cv2.imread("img1.jpg")
print("IMG SIZE : ", img1.size)
print("IMG SHAPE : ", img1.shape)
print("IMG TYPE : ", img1.dtype)

import cv2
img1=cv2.imread("img1.jpg")
grayImage=cv2.cvtColor(img1, cv2.COLOR_BGR2GRAY)
cv2.imwrite('GrayLogo.jpg', grayImage)
cv2.imshow("Original ", img1)
cv2.imshow("GrayLogo.jpg", grayImage)
cv2.waitKey(2000)
cv2.destroyAllWindows()

import cv2
import imutils

img1=cv2.imread("img1.jpg")
resizeImg = imutils.resize(img1, width=200)
cv2.imwrite("resizedIMG.jpg",resizeImg)


import cv2

img=cv2.imread('img1.jpg')
gaussianBlurImg = cv2.GaussianBlur(img, (21,21),0)
cv2.imwrite("guassianIMG.jpg", gaussianBlurImg)

import cv2

img=cv2.imread('img1.jpg')
grayIMG = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
thresIMG = cv2.threshold(grayIMG, 120,255,cv2.THRESH_BINARY)[1]
cv2.imwrite('thresholdIMG.jpg', thresIMG)


import cv2
img1=cv2.imread('baby.jpg')
cv2.imshow('Logo',img1)
cv2.waitKey(0)
cv2.destroyAllWindows()



import cv2
img1=cv2.imread('baby.jpg')
negative_image=255-img1
cv2.imshow("Original Image", img1)
cv2.imshow("Negative Image", negative_image)
cv2.waitKey(0)
cv2.destroyAllWindows()


import cv2
import numpy as np

img2=cv2.imread('baby.jpg', cv2.IMREAD_GRAYSCALE)
c=255.0

log_transformed_image=c*log1p(img2)
log_transformed_image=np.unit8(log_transformed_image)

cv2.imshow('Original Image',img2)
cv2.imshow('Log Transformed Image', log_transformed_image)

cv2.waitKey(0)
cv2.destroyAllWindows()
```


