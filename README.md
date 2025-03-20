# Profiling Analysis of ResNet-18 & EfficientNet: A Green Software Perspective

## Overview  
This repository tracks and optimizes the energy efficiency of deep learning models using **CodeCarbon**. By profiling **ResNet18** and **EfficientNet**, we analyze CO₂ emissions during model training to align with Green AI principles.  



## Features  
- Energy usage tracking with **CodeCarbon**  
- Reproducible Jupyter notebooks for **ResNet18** and **EfficientNet**  
- Automated logging of emissions (`emissions.csv`)  
- Insights on reducing the carbon footprint of machine learning training 


## Installation

Before running the profiling tools, install the required dependencies.

### **If running on Kaggle (inside the notebook):**  
```python
!pip install codecarbon
from codecarbon import EmissionsTracker
```


## Running the Code Profiling Tools

### **Integrate CodeCarbon into Your Code**
Add the following snippet to your training script **before model training starts**:  

# The Repo already has these commands set up. If you are using Resnet18 or EfficientNet. Move to step 2

```python
from codecarbon import EmissionsTracker
import time

# Initialize CodeCarbon tracker
tracker = EmissionsTracker(log_level="critical", output_file="emissions.csv", output_dir="./")

# Start tracking emissions
tracker.start()

# Start total training time measurement
total_start_time = time.time()

# -------- Your model training code goes here --------

# Stop emissions tracking and save results
tracker.stop()

# Calculate total training time
total_time = time.time() - total_start_time
print(f"Total Training Time: {total_time:.2f}s")
```

This will **automatically save** the CO₂ emissions data in `emissions.csv`. You can access that file from kaggle output section

---

### **Step-2 Run CarbonBoard for Visualization**
Once training is complete, open a **command line terminal** and install the required packages:

```bash
pip install codecarbon dash dash-bootstrap-components fire
```
If pip is not there then
```bash
python -m pip install codecarbon dash dash-bootstrap-components fire
```

Now, start **CarbonBoard**, which will visualize the `emissions.csv` data:
You have to download emissions.csv from kaggle output section to run this 

```bash
carbonboard --filepath="emissions.csv" --port=3333
```

If the `emissions.csv` file is not found, locate it using:
```bash
ls -lh emissions.csv   # For Linux/macOS  
dir emissions.csv      # For Windows  
```
Then, specify the full path in the CarbonBoard command.

---

### **Access the Dashboard**
Once CarbonBoard is running, open your browser and go to:  
➡️ **[http://127.0.0.1:3333/](http://127.0.0.1:3333/)**  

Here, you will find a **complete energy analysis** of your training code, including:
- CO₂ emissions per training run
- Cumulative energy usage
- System and hardware details

---

## Running Jupyter Notebooks
This repository includes Jupyter notebooks for training deep learning models and tracking their energy consumption.

- **ResNet-18.ipynb** - Measures energy usage during ResNet18 training.
- **Efficientnet(1).ipynb** - Analyzes the energy efficiency of EfficientNet.


Ensure dependencies are installed before executing.

---
## Troubleshooting & Error Handling

### Common CodeCarbon Issues

1. **Missing Dependencies**
   - Error: `ModuleNotFoundError: No module named 'codecarbon'`
   - Solution: Run `pip install codecarbon` or `python -m pip install codecarbon`

2. **Dashboard Not Launching**
   - Error: `The specified port (3333) is already in use`
   - Solution: Change the port number: `carbonboard --filepath="emissions.csv" --port=3334`

3. **GPU Detection Issues**
   - Error: `Could not initialize NVIDIA energy readings: no GPUs detected` 
   - Solution: Ensure CUDA is properly installed and GPU is accessible with `nvidia-smi`

4. **Permissions Issues**
   - Error: `Permission denied when writing to emissions.csv`
   - Solution: Change output directory to one with write permissions or run with elevated privileges

5. **Memory Issues During Training**
   - Error: `CUDA out of memory`
   - Solution: Reduce batch size (currently set to 32) or image size in the code

### Kaggle-Specific Issues

1. **Internet Access**
   - Ensure "Internet" is enabled in Kaggle notebook settings if downloading models
   
2. **Session Timeouts**
   - Kaggle sessions typically timeout after 12 hours
   - For long-running jobs, save checkpoints regularly


## Results & Logs
- `emissions.csv` - Emissions data from CodeCarbon.

---

## Summary
- Installed **CodeCarbon** for energy tracking.
- Integrated **CodeCarbon** into the training script.
- Collected emissions data in **`emissions.csv`**.
- Launched **CarbonBoard** for real-time energy tracking.

This ensures seamless tracking of AI energy consumption, helping to make deep learning more sustainable.
