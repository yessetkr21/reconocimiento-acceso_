# YRCars

A machine learning system that identifies car model from a photograph.

Upload an image of a car and receive ranked predictions with confidence scores.  
Powered by three EfficientNetB3 deep learning models trained on different datasets.

<table>
  <tr>
    <td align="left" width="100%">
      <img
        src="https://github.com/user-attachments/assets/f289904f-0248-44fc-97a5-4ed98a1ef637"
        alt="YRCars car classification system"
        width="95%"
      />
    </td>
  </tr>
</table>

---

## Live Application

Access the deployed version here:

https://ml-cars-iota.vercel.app/

---
## How It Works

When a user uploads a car image:

1. The image is preprocessed and resized.
2. It is passed through three independently trained classifiers:
   - **Stanford Cars Model**  
     - 196 classes  
     - Predicts: make + model + body type + year  
   - **Custom Dataset Model**  
     - 48 classes  
   - **Dataset Brand Classifier**  
     - 33 car brands  
3. Predictions are combined.
4. Results are ranked by confidence.
5. The Top 5 predictions are returned.

This ensemble-style architecture improves robustness and prediction reliability.

---

## Technology Stack

### Machine Learning
- PyTorch  
- EfficientNetB3 (Transfer Learning)  
- Multi-model ensemble approach  

### Backend
- FastAPI  
- Python 3.10  

### Frontend
- React  
- Vite  
- Framer Motion  

### Deployment
- Railway (Backend)  
- Vercel (Frontend)  

---

## License

MIT License  

---

## Author

@yessetkrodriguez
