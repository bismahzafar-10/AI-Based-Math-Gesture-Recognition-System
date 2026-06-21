
# AI-Based Math Gesture Recognition System

![Python](https://img.shields.io/badge/Python-3.9+-blue?style=flat&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green?style=flat&logo=opencv&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini%20AI-1.5%20Flash-00BCD4?style=flat&logo=google&logoColor=white)

An interactive, real-time computer vision application that enables users to write mathematical equations in the air using hand gestures. The system captures hand landmarks via a webcam, renders the drawings onto a digital canvas, and leverages Google's Multimodal Gemini AI architecture to process the visual canvas and return real-time solutions within a clean Streamlit interface.

---

## 🕹️ Interaction & Gesture Language

The system maps specific hand configurations derived from a 21-point landmark tracking matrix to execute canvas operations:

* **☝️ Draw Mode `[0, 1, 0, 0, 0]`:** Raise only the index finger to draw curves and write mathematical expressions on the live camera canvas feed.
* **✋ Reset/Erase Mode `[1, 1, 1, 1, 1]` or `[1, 0, 0, 0, 0]`:** Raise the designated hand layout to instantly wipe the canvas matrix clear.
* **📨 Execute/Solve Mode `[1, 1, 1, 1, 0]`:** Drop only the pinky finger to capture the current canvas state, convert the pixel array to a PIL image, and stream it to the Gemini 1.5 Flash model for evaluation.

---

## 🛠️ System Architecture & Workflow

1. **Frame Capture & Preprocessing:** Captures standard video feeds via OpenCV (`cv2.VideoCapture`), executing horizontal mirroring to normalize user spatial intuition.
2. **Landmark Extraction:** Processes frames using `cvzone.HandTrackingModule.HandDetector` to isolate bounding dimensions and track finger coordinate vectors.
3. **Array Layering & Blending:** Generates a discrete mask layer via NumPy (`np.zeros_like`). The live feed and drawn canvas are combined dynamically using weighted alpha transparency:
   $$\text{Output Frame} = (\text{Image} \times 0.7) + (\text{Canvas} \times 0.3) + 0$$
4. **Multimodal Evaluation:** Upon receiving the execution gesture, the canvas array is packaged and sent as a visual token payload to the `gemini-1.5-flash` model API, displaying the structured mathematical text response dynamically in Streamlit.

---

## 🚀 Installation & Local Deployment

### 1. Clone the Repository
```bash
git clone [https://github.com/bismahzafar-10/AI-Based-Math-Gesture-Recognition.git](https://github.com/bismahzafar-10/AI-Based-Math-Gesture-Recognition.git)
cd AI-Based-Math-Gesture-Recognition
```
2. Configure Environment Variables
To keep your API keys secure, do not hardcode them. Export your Gemini API key to your local environment variables:

```bash
# On Linux/macOS
export GEMINI_API_KEY="your_actual_api_key_here"

# On Windows (Command Prompt)
set GEMINI_API_KEY="your_actual_api_key_here"
```
3. Install Dependencies

```bash
pip install -r requirements.txt
```
4. Boot the Streamlit UI Application
```bash
streamlit run app.py
```
