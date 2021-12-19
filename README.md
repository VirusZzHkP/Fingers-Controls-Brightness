# Fingers-Controls-Brightness
This Brightness Control With Hand Detection OpenCV Python With Source Code was developed using Python OpenCV, This Python OpenCV Project With Source Code we are going Building a Brightness Controller with OpenCV , To change the brightness of a computer.


![Control Brightness Using FINGERS](https://user-images.githubusercontent.com/76624193/146683296-a85c47d9-5b3d-44c9-b7bb-2d2b92101335.gif)

# Required Libraries:<br>

    import cv2
    import mediapipe as mp
    from math import hypot
    import screen_brightness_control as sbc
    import numpy as np
   
# Source Code:<br>

      import mediapipe as mp
      from math import hypot
      import screen_brightness_control as sbc
      import numpy as np

      cap = cv2.VideoCapture(0)

      mpHands = mp.solutions.hands
      hands = mpHands.Hands()
      mpDraw = mp.solutions.drawing_utils

      while True:
          success,img = cap.read()
          imgRGB = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
          results = hands.process(imgRGB)

          lmList = []
          if results.multi_hand_landmarks:
              for handlandmark in results.multi_hand_landmarks:
                  for id,lm in enumerate(handlandmark.landmark):
                      h,w,_ = img.shape
                      cx,cy = int(lm.x*w),int(lm.y*h)
                      lmList.append([id,cx,cy])
                  mpDraw.draw_landmarks(img,handlandmark,mpHands.HAND_CONNECTIONS)

          if lmList != []:
              x1,y1 = lmList[4][1],lmList[4][2]
              x2,y2 = lmList[8][1],lmList[8][2]

              cv2.circle(img,(x1,y1),4,(255,0,0),cv2.FILLED)
              cv2.circle(img,(x2,y2),4,(255,0,0),cv2.FILLED)
              cv2.line(img,(x1,y1),(x2,y2),(255,0,0),3)

              length = hypot(x2-x1,y2-y1)

              bright = np.interp(length,[15,220],[0,100])
              print(bright,length)
              sbc.set_brightness(int(bright))

              # Hand range 15 - 220
              # Brightness range 0 - 100

          cv2.imshow('Image',img)
          if cv2.waitKey(1) & 0xff==ord('q'):
              break
              
              
      
Cheers !!
H@ppy C0ding ♥
--VirusZzHkP

<br>
CONNECT WITH ME:<br>

   [LinkedIn](https://www.linkedin.com/in/viruszzwarning/) <br>
   
   [Twitter](https://twitter.com/hrisikesh_pal)
    
<br>
Also read my blogs on MEDIUM:

[My Blogs On Medium](https://viruszzwarning.medium.com/)
