# 🚀 UC4 Housekeeping

This is a project aimed to optimize the performance of a uc4 system, do you need it? Let's see if it's required

- Do you have little to no housekeeping efforts allocated?
- Does your system have hundreds of flows that go to blocked and need to be cancelled manually?
- Is your system slow?

---

## ✨ Features
- Easy to use
- Cancels and deactivates old blocked workflows this freeing up the EH
- Modify to your needs

---

## 📸 Workflow stucture

![Workflow image](https://github.com/vegaflare/uc4-scripts/blob/main/imgs/eh_housekeeping_wf.PNG?raw=true)

---

## 🛠️ Installation

```bash
# Download the xml file
Download the export.xml and import to your system directly (Make sure you edit the version in the xml to your AE version at the beginning of the file if your system is not v24)

# Create objects and copy the code
Object types and attributes are mentioned the start of the code
Other objects you need:
 - Static VARA: VAR.HOUSEKEEPING.CLIENTS
    Keep the client numbers as keys

 - Static VARA: VAR.CANCELLATION.PROC.COUNTER
    Keep it empty, it's populated automatically
    
 - Job group  : GROUP.HOUSEKEEPING_CANCEL

 - Workflow   : PLAN.UC4_HOUSEKEEPING_CANCEL
    Refer the above image

 - Rest of the objects create as you see the scripts for
