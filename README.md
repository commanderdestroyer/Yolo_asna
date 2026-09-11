# YOLO Object Detection Web Application

A simple web application for object detection using **YOLO, FastAPI, and a web frontend**.

## Features

- Detect objects in images
- Detect objects in short MP4 videos
- Display bounding boxes and confidence scores
- Configurable confidence threshold
- Image and video upload
- Annotated image/video output

## Tech Stack

### Backend
- Python
- FastAPI
- Ultralytics YOLO
- OpenCV
- Pillow
- Uvicorn

### Frontend
- HTML
- JavaScript
- Fetch API

## Project Structure


YOLOProject/
├── backend/
│   └── main.py
├── frontend/
│   └── index.html
├── .gitignore
├── requirements.txt
└── README.md

## How It Works

Frontend
   │
   │ Upload image / video
   ▼
FastAPI Backend
   │
   ▼
YOLO Model
   │
   ▼
Detection Result
   │
   ▼
Frontend displays result

## Installation

### 1. Clone the repository

git clone <YOUR_REPOSITORY_URL>
cd YOLOProject


### 2. Create a virtual environment

python3 -m venv venv


Activate the virtual environment:

source venv/bin/activate

### 3. Install dependencies

pip install -r requirements.txt


## Run the Backend

cd backend
uvicorn main:app --reload


The backend will be available at:

http://127.0.0.1:8000


FastAPI documentation:

http://127.0.0.1:8000/docs


## Image Detection

The application supports:

- JPG
- JPEG
- PNG
- MP4

The uploaded image/video is processed by the YOLO model and the frontend displays the annotated result.