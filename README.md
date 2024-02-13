# HandDetection
import cv2
import mediapipe as mp
import time

cap = cv2.VideoCapture(0)
mpdraw = mp.solutions.drawing_utils
mphands = mp.solutions.hands
hands = mphands.Hands()

while True:
    success, img = cap.read()
    imgRGB = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    results = hands.process(imgRGB)
    if results.multi_hand_landmarks:
        for handlms in results.multi_hand_landmarks:
            mpdraw.draw_landmarks(img, handlms, mphands.HAND_CONNECTIONS)
    cv2.imshow("image", img)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
