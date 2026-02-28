# Facial Recognition Access Control System

A real-time facial recognition access control system built with Python (OpenCV), Node.js, and React. The system detects and identifies faces through a live camera feed, manages user registration, and maintains a complete access log — all running locally without cloud dependencies.  
This type of system is widely used by companies and organizations for secure physical access control to offices, buildings, and restricted areas.

<table>
  <tr>
    <td align="left" width="50%">
      <img
        src="https://github.com/user-attachments/assets/c6939e19-3a15-4b30-82c6-3844635c68f5"
        alt="System demo showing real-time facial recognition"
        width="90%"
      />
    </td>
    <td align="right" width="50%">
      <img
        src="https://github.com/user-attachments/assets/bada1a2a-4084-4763-bed7-40be4dadb31b"
        alt="Facial recognition system using artificial intelligence"
        width="90%"
      />
    </td>
  </tr>
</table>

---

## Overview

This system provides a complete facial recognition pipeline for physical access control. It captures video from a connected camera in real time, detects faces using the YuNet model, generates 128-dimensional facial embeddings using SFace, and verifies identities against a local SQLite database. A web-based admin panel allows managing registered users and reviewing the complete access history.

---

## Key Capabilities

- Real-time face detection and recognition at up to 30 FPS  
- User registration via terminal prompt or web interface  
- Role-based user management (employee, admin, visitor)  
- Access log with timestamps, user names, and confidence scores  
- Web dashboard with live statistics and recent events  
- Embedding cache to reduce backend load on repeated detections  
- Platform-optimized camera handling (DirectShow on Windows)  
- No photographs are stored — only numeric embedding vectors  

---

## Technology Stack

### -Computer Vision YuNet, ONNX, DNN, SFace, Numpy, OpenCV

### -Backend Express (Node.js)

### -Frontend (React)

---

## System Architecture and Workflow

### Face Registration Process

- The user provides their name via the terminal (`r` key) or through the web interface.  
- The Python service captures 15 frames from the camera over a maximum window of 8–10 seconds.  
- YuNet detects the face in each frame and verifies that a single face is present.  
- SFace generates a 128-dimensional embedding vector per frame.  
- All collected embeddings are averaged into a single representative vector.  
- The averaged embedding is sent to the Node.js backend via `POST /api/users`.  
- The backend stores the name, email, role, and embedding (serialized as JSON) in SQLite.  

No photographs are stored at any point. The system persists only a numeric vector representing facial geometry, which cannot be used to reconstruct the original face.

---

### Face Verification Process

- The Python service continuously reads frames from the camera.  
- Every 80 milliseconds, a frame is dispatched to a background inference thread.  
- YuNet detects all faces in the frame, and SFace generates an embedding for each detected face.  
- Each embedding is first checked against an in-memory cache.  
- On a cache miss, the embedding is sent to the backend via POST.  
- The backend computes cosine similarity between the incoming embedding and all registered user embeddings.  
- If the highest similarity score exceeds the threshold (0.6), access is granted and the matched user’s name is returned.  
- The result is rendered in the OpenCV window in real time: a green bounding box for granted access and red for denied access.  
- An access log entry is recorded in the database, including timestamp, user name, action, and confidence score.  

---

## License

© yessetk rodriguez  
Software available for sale  
Contact: yessetkrodriguez80@gmail.com
