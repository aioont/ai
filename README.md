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



```
workflow in their development consists of gathering available
data, then selecting and extracting a set of relevant features from it,
building, training, and validating the ML model, before finally de-
ploying into production.

Explainability and interpretability are obtained by using
high-level, human understandable features of the network traffic,
interpretable ML decision trees for malware detection, while exten-
sibility is the result of the modular design of the malware detection
engine which allows us to modify/extend one of its component
without affecting the others.

. In particular, RADAR (𝑖) exploits the
popular TTP ontology of adversary behaviour described in the
industry-standard MITRE ATT&CK framework to unequivocally
identify and classify the potential malicious network flows in each
traffic capture, (𝑖𝑖) for each TTP it utilises a dedicated decision
tree to label each network flow as potentially malicious, and, (𝑖𝑖𝑖)
combines the results obtained for the different TTPs in order to
finally label each traffic capture as benign or malicious.

In the network domain, work has mostly centred around the
extraction of MITRE ATT&CK TTPs from network traffic
Existing work : McPhee[ s scripts identify 3 technique ], BZAR [  BZAR can identify 12
techniques and 8 sub-techniques across 9 tactics ]

RADAR support higher degree of config : ) supporting thresholds for specific TTPs, (𝑖𝑖) allowing the selec-
tion of different detection policies for the overall system, and (𝑖𝑖𝑖)
having policy-specific thresholds, which altogether enable a gran-
ular balance between the true-positive and the false-positive rate.

In the field of cy-
ber security, and malware analysis in particular, extensibility is a
necessary criterion to design systems that can adapt in the face of
novel and constantly-evolving attacks

 explainability is essential for users to effectively
understand, trust, and manage powerful artificial intelligence ap-
plications in every application domain, including cyber securit

RADAR’s data pipeline is designed to be able to take arbitrary
packet captures as input, and output:
(1) the relevant matching TTPs for that sample, and
(2) a prediction as to whether the sample is malicious.

This enables RADAR to be employed as a ‘plug-and-play’ tech-
nology wherein a packet capture can be sliced from a larger flow
of network traffic and analysed

The first stage in our data pipeline is the Ingestion System that
takes as input network traffic captures (PCAPs) and builds a graph
database of samples which preserves the most important charac-
teristics of the traffic for the purposes of TTP detection. Among
the various network data formats that we considered, we select
NetFlows which rely solely on metadata, thus meeting the require-
ments of being content-agnostic and lightweight. In particular, we
use a specific type of NetFlow

YAF generates bidirectional flows in IPFIX [ 6] standard, which
is based on the Cisco NetFlow V9 export protocol. Our primary
motivation for selecting YAF is that it is designed for high perfor-
mance and scalability across large networks.

Having selected and created the relevant features for our network
traffic, we then map them into a graph whose nodes corresponds
to the hosts as uniquely identified by their IP address, and whose
edges correspond to a flow between the two hosts. This information
is stored in a Neo4j graph database 1, which we query using the
Cypher query language.

## TTP Detection
The TTP Detection Engine analyses all flows in the graph database
and executes detection rules on the graph entities and relationships
to identify any matching MITRE ATT&CK technique

The TTPs we consider broadly falls into two categories:
(1) Feature-based detection rules. This type of detection
relies on specific features of the flows described in Table 1.
(2) Heuristic-based detection rules. This type of detection
relies on the analysis of multiple flows and uses heuristics
based on their properties
Example 3.1. For the feature-based rules, we consider the MITRE
ATT&CK technique T1571 (Non-Standard Port). This technique is
part of the “Command and Control” (C&C) tactic and is applicable
to the case when a host attempts to communicate with another
host using standard network protocols but on a non-default port.
Malware can attempt such a connection for several reasons—to
communicate using a random port, evade firewall rules blocking
certain default ports, or to find an open port for the purpose of
establishing a C&C channel, among others. In order to detect this
technique we rely on the features of the flow the two hosts use to
communicate with each other. Specifically, we compare the network
protocol in the flow with the port(s) used during communication
and determine if these correspond to their defaults. In order to
do this, we utilise YAF during the Ingestion Processing phase to
determine the application layer protocol of every flow independent
of the port used. This feature is extracted and stored in our graph
as the flow property applabel. Our detection logic maintains a
list of the 50 most popular application layer protocols and their
corresponding default ports, and compares these to the features
of applabel and port present in every flow. A mismatch between
these features is a positive match for T1571.





```
