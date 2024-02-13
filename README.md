# HandDetection
import cv2<br>
import mediapipe as mp<br>
import time<br>
<br>
cap = cv2.VideoCapture(0)<br>
mpdraw = mp.solutions.drawing_utils<br>
mphands = mp.solutions.hands<br>
hands = mphands.Hands()<br>
<br>
while True:<br>
    success, img = cap.read()<br>
    imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)<br>
    results = hands.process(imgRGB)<br>
    if results.multi_hand_landmarks:<br>
       for handlms in results.multi_hand_landmarks:<br>
            mpdraw.draw_landmarks(img, handlms, mphands.HAND_CONNECTIONS)<br>
    cv2.imshow("image", img)<br>
    if cv2.waitKey(1) & 0xFF == ord('q'):<br>
         break<br>
<br>
cap.release()
cv2.destroyAllWindows()
