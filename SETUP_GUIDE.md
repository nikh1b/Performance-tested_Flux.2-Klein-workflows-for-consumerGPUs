# Detailed Setup Guide - Flux.2 Klein ComfyUI

## Prerequisites

- **Windows 10/11 or Linux**
- **Python 3.10+**
- **Git**
- **NVIDIA GPU** (RTX 3060 or better recommended)
- **6GB+ VRAM** (for 4B models)

## Step-by-Step Installation

### Step 1: Install ComfyUI (If Not Already Done)


# Clone ComfyUI
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI

# Install dependencies
pip install -r requirements.txt

# (Optional) Install GPU acceleration
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
Step 2: Clone This Repository

cd ..
git clone https://github.com/YOUR-USERNAME/flux2-klein-comfyui.git
cd flux2-klein-comfyui
Step 3: Copy Workflows

# Copy all workflows to ComfyUI examples folder
cp workflows/*.json ../ComfyUI/web/examples/
Step 4: Create Model Folders

cd ../ComfyUI
mkdir -p models/text_encoders
mkdir -p models/diffusion_models
mkdir -p models/vae
Step 5: Download & Place Models
See Model Downloads section in README.md

For RTX 3060, download:

qwen_3_4b.safetensors → models/text_encoders/

flux-2-klein-4b-fp8.safetensors → models/diffusion_models/ (distilled)

flux2-vae.safetensors → models/vae/

Step 6: Install Recommended Custom Nodes
Open ComfyUI Manager from the web UI and search for:

Efficiency Nodes

DetailDaemon

UltimateSDUpscale

Or install manually:


cd ComfyUI/custom_nodes
git clone https://github.com/jags111/efficiency-nodes-comfyui.git
git clone https://github.com/Jamp2D/ComfyUI_UltimateSDUpscale.git
Step 7: Run ComfyUI

python main.py
Open browser to http://localhost:8188

Step 8: Load a Workflow
Click Menu (hamburger icon)

Select "Load"

Choose a workflow from Examples folder

Fill in prompts

Click "Queue Prompt" to generate

Troubleshooting
Issue: "Module not found" Errors
Solution:


pip install --upgrade pip
pip install -r requirements.txt
pip install torch torchvision torchaudio --upgrade
Issue: Out of Memory (CUDA)
For RTX 3060 with 6GB VRAM:

Use flux2-klein-4b-distilled-fast.json (distilled model)

Lower resolution to 512x512

Enable text encoder offloading in workflow

Close other GPU applications

Issue: Model Files Not Found
Check that model filenames exactly match:


✓ qwen_3_4b.safetensors (NOT qwen_3_4b-fp8.safetensors)
✓ flux-2-klein-4b-fp8.safetensors
✓ flux2-vae.safetensors
Issue: Workflow Won't Load
Clear browser cache (Ctrl+Shift+Delete)

Restart ComfyUI (python main.py)

Try different workflow file

Check ComfyUI console for errors

Performance Optimization Tips
For RTX 3060:

- Use distilled model (4B-FP8)
- Resolution: 512x512 max
- Steps: 10-15 (not 20+)
- Enable: Text encoder CPU offloading
- Batch size: 1
For RTX 4070:
  
- Use base model (4B-Base-FP8)
- Resolution: 768x768
- Steps: 15-20
- Batch size: 1-2
For RTX 4090:

- Use 9B model
- Resolution: 1024x1024
- Steps: 20-30
- Batch size: 2-4
Verification Checklist
 Python 3.10+ installed

 ComfyUI cloned and dependencies installed

 Workflows copied to web/examples/

 Model folders created in models/

 All 3 model files downloaded & placed correctly

 Custom nodes installed (optional but recommended)

 ComfyUI runs without errors (python main.py)

 Models load without "file not found" errors

 First generation completes successfully

Next Steps
Read PERFORMANCE_BENCHMARK.md for expected speeds

Check examples/prompt-examples.txt for prompt ideas

Try different workflows to see quality differences

Read HARDWARE_OPTIMIZATION.md for tuning tips

Still having issues? Check TROUBLESHOOTING.md or open a GitHub Issue.
