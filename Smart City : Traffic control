<Jetson NANO CODE>

import torch
import cv2
import requests


model = torch.hub.load('ultralytics/yolov5', 'yolov5s', pretrained=True)


SERVER_IP = 'xx.xx.xx.xx'  # 라즈베리파이 IP 주소
SERVER_PORT = xxxx

def send_data_to_server(detected_cars_count):
    url = f'http://{SERVER_IP}:{SERVER_PORT}/vehicle_count'
    data = {'num_vehicles': detected_cars_count}
    requests.post(url, data=data)

cap = cv2.VideoCapture(0)
while True:
    ret, frame = cap.read()
    if not ret:
        break

    results = model(frame)
    detected_cars_count = len(results.xyxy[0])
    

    send_data_to_server(detected_cars_count)

    cv2.imshow('frame', frame)
    if cv2.waitKey(1) == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
