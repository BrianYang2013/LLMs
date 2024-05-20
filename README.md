# LLMs
Record LLMs Journey

**05-19-2024:** Test MPS on macbook pro

- Created an virtual env on conda. Point vscode to that environment. 
- [Pytorch Mac GPU 训练与测评](https://zhuanlan.zhihu.com/p/517699916). Need to fix a few issues
  - Test function missed. Can be found at: https://github.com/pytorch/examples/blob/main/mnist/main.py
  - python main.py --use_gpu : will receive 220.96 s vs 54.08 s , so MPS is about 4.09 times faster than CPU on MNIST

**05-12-2024:** Preparation and explore

- Llama 3 ZH instruct: scomper/llama3-zh-inst:latest

**05-11-2024:** Preparation and explore

- Create [backlog](Backlog.md)
- Evaluate tool TailScale
  - Efficiently transfer file between PC and Mac
  - issue: Company devices blocked TailScale. 
  - issue: encoding issue with Chinese characters, including file names. Revise the windows setting: time & language, 
  - issue: Can only transfer files not folder. Need to compress

- Test small models
  - OpenWebUI: via docker. 
  - Ollama: llama3:latest, gemma, codellama:13b-python, 
  - Need more memory: dolphin-mixtral:latest, llama3:70b-instruct-q2_K


**05-10-2024:** Delete ubuntu

- Delete ubuntu
  - BIOS, BOOT, Set windows as 1st and Ubuntu as second. 
  - DiskGenius, delete the 200g partition. extend to the main system partition. 
  - Delete ubuntu folder under EFI, in the 100m system(0). 
- Pytorch - [Quickstart](https://pytorch.org/tutorials/beginner/basics/quickstart_tutorial.html)

**05-07-2024:** Make CUDA work, install ubuntu

- What works
  - Install: Typora, Github Desktop
  - Re-install CUDA, cudnn_9.1.1_windows, Anaconda,
    - [A Step-by-Step Guide to Installing CUDA with PyTorch in Conda on Windows](https://medium.com/@harunijaz/a-step-by-step-guide-to-installing-cuda-with-pytorch-in-conda-on-windows-verifying-via-console-9ba4cd5ccbef)
    - Find the right version: 
      - [Pytorch - Start locally](https://pytorch.org/get-started/locally/)
      - Pytorch build: 2.3
      - Compute Platform: CUDA 12.1
    - Passed all verification
      - Check GPU Status: navidia-smi
      - [Update VS Code python interpreter](https://stackoverflow.com/questions/43351596/activating-anaconda-environment-in-vscode)
      - Anaconda-JupyterNotebook, and VS code: torch.cuda.is_available()
      - [Pytorch Verification](https://github.com/BAI-Yeqi/PyTorch-Verification/tree/master)
  - [Install ubuntu 24.04](https://www.minitool.com/partition-disk/install-ubuntu-on-windows-11.html)
    - Can not find duel system option: bcdedit /set "{bootmgr}" path \EFI\ubuntu\grubx64.efi
- What does not work
  - Ubuntu does not have wifi: Can not recognize R8125. Downloaded the driver from the official website。 Found a physical cable to install make, successfully uninstall the driver but failed to install R8125
  - Error message when reboot. Can not find those files in \efi\ubuntu: 
    - Failed to open \EFI\ubuntu\ 乱码 - invalid Parameter. 
    - Failed to load image 乱码： invalidparameter
    - start_image() returned invalid parameter, falling back to default loader

**05-05-2024:** Order PC on 04-29 with 4060 Ti 16G, arrive 04-30, Setup 05-05. Initial installation

- What works
  - Check GPU status: nvidia-smi
  - Install: Chrome, Anaconda (Pytorch), Docker, Ollama, OpenWebUI, 
  - Cuda: 12.1.  Cautious: Pytorch 2.3.0, request CUDA 11.8 or 12.1, my GPU support up to 12.3 
  - [Pytorch Verification](https://github.com/BAI-Yeqi/PyTorch-Verification/tree/master)
- What not very helpful: Chrome Remote Desktop, Anyviewer (Prefer to use Mac pro to connect to the PC. Unfortunately, do not support MacOS)
- Considering to install ubuntu to make it simple, and for remote access. 
