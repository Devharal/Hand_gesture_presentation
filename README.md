# Hand_gesture_presentation

This is an Open-CV project build by me using CVZone library. This project basically helps for presenting ideas through PPT or image and teacher can hightlight points just using his fingers from any distance.


# Demo
https://user-images.githubusercontent.com/90788942/162742233-ccfd9336-d86b-4387-b155-0e91e146a0aa.mp4

# CVZone


This is a Computer vision package that makes its easy to run Image processing and AI functions. At the core it uses [OpenCV](https://github.com/opencv/opencv) and [Mediapipe](https://github.com/google/mediapipe) libraries. 

## Installation
You can  simply use pip to install the latest version of cvzone.

`pip install cvzone`

<hr>






### Hand Tracking

<hr>

<p align="center">
  <img width="640" height="360" src="https://github.com/cvzone/cvzone/blob/master/Results/Fingers-Distance.jpg">
</p>

#### Basic Code Example 
<pre>
from cvzone.HandTrackingModule import HandDetector
import cv2

cap = cv2.VideoCapture(0)
detector = HandDetector(detectionCon=0.8, maxHands=2)
while True:
    # Get image frame
    success, img = cap.read()
    # Find the hand and its landmarks
    hands, img = detector.findHands(img)  # with draw
    # hands = detector.findHands(img, draw=False)  # without draw

    if hands:
        # Hand 1
        hand1 = hands[0]
        lmList1 = hand1["lmList"]  # List of 21 Landmark points
        bbox1 = hand1["bbox"]  # Bounding box info x,y,w,h
        centerPoint1 = hand1['center']  # center of the hand cx,cy
        handType1 = hand1["type"]  # Handtype Left or Right

        fingers1 = detector.fingersUp(hand1)

        if len(hands) == 2:
            # Hand 2
            hand2 = hands[1]
            lmList2 = hand2["lmList"]  # List of 21 Landmark points
            bbox2 = hand2["bbox"]  # Bounding box info x,y,w,h
            centerPoint2 = hand2['center']  # center of the hand cx,cy
            handType2 = hand2["type"]  # Hand Type "Left" or "Right"

            fingers2 = detector.fingersUp(hand2)

            # Find Distance between two Landmarks. Could be same hand or different hands
            length, info, img = detector.findDistance(lmList1[8], lmList2[8], img)  # with draw
            # length, info = detector.findDistance(lmList1[8], lmList2[8])  # with draw
    # Display
    cv2.imshow("Image", img)
    cv2.waitKey(1)
cap.release()
cv2.destroyAllWindows()
</pre>

 

<hr>

# Hope you liked it.

