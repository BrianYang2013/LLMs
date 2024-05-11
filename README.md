# LLMs
Record LLMs Journey



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
  - Ubuntu does not have wifi. 
  - Error message when reboot: 
    - Failed to open \EFI\ubuntu\ 乱码 - invalid Parameter. 
    - Failed to load image 乱码： invalidparameter
    - start_image() returned invalid parameter, falling back to default loader
  - 

**05-05-2024:** Order PC at 04-29 (4060 Ti 16G), arrive 04-30, Setup 05-05. Initial installation

- What works
  - Check GPU status: nvidia-smi
  - Install: Chrome, Anaconda (Pytorch), Docker, Ollama, OpenWebUI, 
  - Cuda: 12.1.  Cautious: Pytorch 2.3.0, request CUDA 11.8 or 12.1, my GPU support up to 12.3 
  - [Pytorch Verification](https://github.com/BAI-Yeqi/PyTorch-Verification/tree/master)
- What not very helpful: Chrome Remote Desktop, Anyviewer (Prefer to use Mac pro to connect to the PC. Unfortunately, do not support MacOS)
- Considering to install ubuntu to make it simple, and for remote access. 
