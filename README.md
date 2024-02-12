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

For each malware sample, we isolate its
flows and establish a mean packet outflow to packet inflow ratio
through their directed edges, and determine a unique baseline for
each sample. Then by defining a threshold over which there is far
more data egress than ingress as compared to the baseline, we iden-
tify flows and hosts that are potentially communicating via a C2
channel or exfiltrating data from the network. This threshold is
designed to be dynamically adjusted based on the distribution of
the network traffic and the characteristics of what is considered
“normal” in a given network or environment.
At the end of this process, the system outputs a list of flows and
their corresponding TTPs. This information is further aggregated
by combining all the flows belonging to the same sample and then
passed on to the TTP-based Classification system.


TTP-based Classification System

The TTP-based Classification System checks whether the flows

in each sample exhibit malicious behaviour when compared to

other flows matching the same TTP, and then flags a sample as

malicious if “enough” flows exhibit malicious behaviour.

TTP-based Classification System

takes as input: (𝑖) the flows’ properties (as listed in Table 1), and (𝑖𝑖)

the TTPs detected in each flow, as returned by the TTP Detection

Engine. Following a “divide-and-conquer” approach, it consists of

one base classifier for each analysed TTP. This choice allows us

to compare the behaviour of each flow with only those flows that

match the same TTPs.

For each flow 𝑓 , we create a vector 𝑥 containing all the features

listed in Table 1. Then, 𝑥 is passed to all the base classifiers that

have been trained on the flows that matched the same TTPs as 𝑓 .

Thus if, for example, 𝑓 matched TTP𝑖

, TTP𝑖+1 and TTP𝑘

then 𝑥

will be passed just to the 𝑖th, (𝑖 +1)th and 𝑘th classifiers. Each of the

selected classifiers then independently decides whether 𝑓 presents malicious behaviour when compared to the other flows flagged
with the same TTP.

In order to preserve the transparency
and explainability of the system, we opt to use decision trees [31].

Indeed, a decision tree is a transparent model whose predictions

can be easily explained via Boolean logic rules. This is not true

for most classifiers (e.g., based on artificial neural networks) which

are often completely opaque models whose predictions are difficult

to interpret.
Once we have the prediction for each flow in the sample, we have

to find a way to aggregate them and decide whether the sample is

malicious or not. To this end, we devise three policies:

(1) P1: the first policy relies on 𝑛𝑡

, the number of unique TTPs

matched by the malicious flows in the sample. If 𝑛𝑡 ≥ 𝜃𝑡

then the sample is considered malicious. 𝜃𝑡

is a parameter

that the user can tune.

(2) P2: the second policy relies on 𝑛𝑓

, the number of malicious

flows in the sample. If 𝑛𝑓 ≥ 𝜃𝑓

then the sample is consid-

ered malicious. 𝜃𝑓

is a parameter that the user can tune.

(3) P3: the third policy relies on 𝑝, the percentage of malicious

flows in the sample. If 𝑝 ≥ 𝜃𝑝 then the sample is considered

malicious. 𝜃𝑝 is a parameter that the user can tune.

#EVALUATION
In doing so,

we use an especially large dataset of network flows collected from malware samples for testing.We execute our samples within a

Cuckoo sandbox on VirusTotal.
Dataset Samples Flows

Ember Malicious [2] 435,741 26,567,527

MalRec [27] 37,763 12,273,502

MalShare [25] 1,268,923 32,310,907

VirusShare [30] 595,098 12,217,493

Ember Benign [2] 155,432 1,423,023

Total (unique) 2,286,907 84,792,452

Table 3: Overview of all the datasets. The first four datasets

contain only malicious samples, while the last one containsonly benign samples.

Ember is an open dataset of hashes of malicious

Windows executables created as a benchmark for machine learning

models. It contains 3 types of hashes: malicious, benign and unla-

belled. For our purposes, we utilise both the malicious hashes (as

Ember Malicious) and the benign hashes (as Ember Benign) in our

dataset. MalRec is a small dataset created as a result of a running

malware on a dynamic analysis platform, which was collected over

a two-year period. MalShare is a community-driven open repository

of malware samples, which features over a million hashes, from

which the corresponding dataset is derived. Similarly, VirusShare is

a repository that aims to help security researchers analyse selected

strains of malware, and the source of our corresponding dataset.

We select these datasets as they are representative of modern com-

modity malware and allow for the reproducibility of results. It is

important to note that we do not utilise the entirety of each dataset

in our experiments, since we filter out samples that do not exhibit

any network activity. Overall, we analyse a total of 84,792,452 flows

from 2,286,907 malicious and benign samples.

```
