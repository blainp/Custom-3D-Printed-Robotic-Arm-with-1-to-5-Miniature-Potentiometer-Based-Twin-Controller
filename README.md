# Custom-1-Meter-3D-Printed-Robotic-Arm-with-Miniature-Potentiometer-Based-Twin-Controller
A fully custom, 3D-printed robotic arm utilizing 5 NEMA 17 joints with 3D printed gearboxes. Controlled via Arduino and a Python/tkinter interface utilizing a  controller  a scaled-down replica of the arm using potentiometers in place of motors (with a switch for claw actuation) as an intuitive physical input device.

# Machine Learning Behavioural Biometric Identification Using MIDI Keyboard Performance Signatures

This repository contains the feature extraction pipeline, machine learning models, and inference system for a behavioural biometric authentication system based on MIDI keyboard performance data.

---

## Project Overview

This project explores the identification of individual musicians using their unique performance signatures captured through MIDI data. Instead of relying on audio or vision-based approaches, the system analyzes keystroke-level behaviour such as timing, velocity, articulation, and pitch movement.

Raw MIDI recordings are segmented into fixed time windows and transformed into engineered behavioural features. These features are then used to train multiple machine learning models to classify the performer behind each recording.
<p align="center">
<img width="1400" height="384" alt="image" src="https://github.com/user-attachments/assets/a36d9446-681e-41ec-9586-0407a3ce6564" />
</p>


The system demonstrates that freestyle musical improvisation contains stable, identifiable behavioural patterns that can be used for user authentication.
---



## Features

### MIDI-Based Behavioural Capture
- Records raw MIDI performance data:
  - Note timing
  - Velocity (on/off)
  - Duration
  - Pitch information

### Feature Engineering Pipeline
- Extracts behavioural biometric features including:
  - Rhythm and timing patterns (IOI, articulation)
  - Dynamic expression (velocity trends)
  - Pitch movement and range
  - Polyphony and chord density
  - Arpeggio and grace-note structure

### Windowed Analysis System
- Splits performances into fixed time windows (30s segments)
- Enables fine-grained behavioural modeling across time

### Machine Learning Identification
- Uses ensemble and stacked models:
  - Voting classifiers
  - PCA + Logistic Regression pipeline
  - Stacking models (Random Forest + KNN → Logistic Regression)

### Behavioural Inference System
- Aggregates per-window predictions using probability averaging
- Outputs final performer prediction with confidence scoring

---

## Repository Structure
```text
/Documentation
Contains official IEEE report and presentation as well as a system diagram.

/Code
Contains main TrainAndTestModel.ipynb file for Training the models as well as testing their accuracy with
additional performances, requirements file, final stacked dataset utilzied to train models (stacked_dataset.csv),
as well as 6 test files to use while testing performance of the model.

/Code/FeaturesAndDatasetStacker
Contains all individual performances as pre-processed MIDI csv datasets (features 0-5) and a script which combines
them into a single stacked csv dataset with userIDs (stacked_dataset.csv)

/Code/RawDataAndExtractionCode
Contains 2 distinct raw performance datasets (recorded_piano 1 and 2) as an examples of the raw MIDI data acquired
for this project, as well as the pre-processing script utilized to create the "features" csv datasets
```

For full methodology, literature review, and figures, see the IEEE report in `/Documentation`.

---

## Dataset Pipeline

1. MIDI recordings collected from multiple performers  
2. Data segmented into fixed-length performance windows  
3. Feature extraction applied per window  
4. Individual datasets combined into a stacked dataset  
5. Missing values cleaned and standardized  
6. Dataset used for supervised classification (userID labels)

---

## Machine Learning Performance

The system evaluates multiple behavioural classification models using both split testing and full-performance inference.

### Performance Summary
- 80/20 stratified split cross-validation yielded 94.87% (Models 1 & 2) and 92.31% (Model 3) accuracy, however, these figures are likely inflated, since segments from the same recording session can appear in both train and test sets
- A more realistic measure comes from evaluating on entirely unseen full performances: all models correctly identified the performer across all 7 test recordings, with a mean confidence of ~80% and a minimum of 65%
- Correct identification held even when the primary subject intentionally varied their playing style across sessions, suggesting the system captures deeper motor/behavioural traits rather than surface-level style
<p align="center">
 <img width="800" height="600" alt="Feature Importance (3)" src="https://github.com/user-attachments/assets/a99bdd42-1f46-4f0f-a73c-f10a7df79de6" />
</p>



### Evaluation Method
- 80/20 stratified split for initial validation
- Full-session inference for realistic performance testing
- Confusion matrices and probability aggregation used for analysis


---

## Installation & Setup

### 1. Clone the Repository

```bash

git clone https://github.com/blainp/Behavioral-Biometric-Identification-Using-MIDI-Keyboard-Performance-Signatures.git

```

### 2. Install Python Requirements

```bash
pip install -r requirements.txt

```

### 3. Install Anaconda and Jupyter Notebook

### 4. Run the Training and Testing ipynb file with sample data through Jupyter Notebook


---

## Known Constraints & Future Improvements

### Dataset Size
The current dataset is limited to 5 participants, which constrains generalization across a wider population.

### Feature Expansion
Future improvements could include:
- Pedal usage modeling
- Expressive timing micro-variation
- Harmonic context awareness
- Advanced sequence models (RNNs / Transformers)

### Real-Time Deployment
The system is currently offline. Future work includes:
- Live MIDI authentication
- Continuous user identification during performance
- Real-time behavioural biometric systems

---

## References

This project builds upon research in:
- Behavioural biometrics in keystroke dynamics  
- Music performance analysis using MIDI data  
- Machine learning for performer identification  
- Rhythm and expressive timing in musical style modeling  

Additional references are included in the project report.
