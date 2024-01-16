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
cv2.destroyAllWindows()```


