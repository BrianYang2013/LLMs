# LLMs
## Record LLMs Journey



**11-22-2024:** Summarize the local LLM

- GPU > Apple M chips. The key is the memory bandwidth, and core of GPU (or TFLOPS)
- GPU: With same budget, 3-4 second hand GPU (like 3090) is the best choice. 
- Apple M chips: [Performance of llama.cpp on Apple Silicon M-series](https://github.com/ggerganov/llama.cpp/discussions/4167) shows M2 Ultra > M1 Ultra > M4 Max > M2 Max > M1 Max > M3 Max. 
- A practical setup: 
  - [Openrouter](https://openrouter.ai/) API for all open/close models
  - Sensitive personal data: 
    - Hardware: Apple (M1 + 16G) or GPU (4060 Ti 16G)
    - Models: Local LLM 3.2 3B, 3.1 8B. 70B is hard. 

**11-10-2024:** 

- Install iCloud app from Microsoft store. Only sync the iCloud documents 
- Install Obsidian, sync to the iCloud Vaults
- Clean up Ollama
  - Ollama list, review and remove out dated models. Pull 3.2 3b, llama3.2-vision:11b-instruct-q8_0 (15.3/16G Dedicated GPU, 16.7/31.9 GPU). 
  - llama3:70b-instruct-q2_K still works, but a little bit slow
  - Use Ollama with any GGUF Model on HuggingFaceHub: ollama run hf.co/{username}/{repository}
  - qwen2.5:14b: 11.3/16G dedicated GPU: Fast. 
  - qwen2.5-coder:32b-instruct-q4_K_S:  14.3/16G Dedicated GPU, 19.8/31.9 GPU: Decent. 
  - qwen2.5-coder:32b-instruct-q6_K:  14.2/16G Dedicated GPU, 27.3/31.9 GPU. Slow but it works. 
- Add local ollama model to Obsidian Copilot: 
  - Model name: llama3.2-vision:11b-instruct-q8_0
  - Provider: ollama
  - Base URL: http://localhost:11434/

**10-21-2024:** Reflection：我们并不存在真正的ground truth。同样的故事可以有不同的演绎，在不同的标准下，优劣难辨。所以语音到文本未必需要绝对的吻合，除非是法律或者需要逐字逐句核实的特殊场景。在教育领域里，适当的改写完全是合理的，可以产出更加流畅，逻辑，容易理解的文本。

**10-20-2024**: Video to audio to script

- Mac: Automator, define workflow. 
- Script: 
  - Video_to_audio.py: ffmpeg
  - Audio_to_script.py: whisper. Or APP such as whisper notes to process one by one. 
    - V2 can use options to introduce prompt (example) to add the punctuation. V3 and turbo failed with RuntimeError: Given groups=1, weight of size [1280, 128, 3], expected input[1, 80, 3000] to have 128 channels, but got 80 channels instead
    - Whisper does not support Mac MPS devices. 
    - Obsidian: leverage Gemini flash 1.5 API, add punctuation, fix issues like Homonyms. 
  - Summarize. Compare with manual baseline, evaluate OpenAI, Claude, Gemini flash 1.5

**10-13-2024**: Open_webui, Rewrite, Obsidian(copilot chat, text generator)

**05-19-2024:** Test MPS on macbook pro

- Created an virtual env on conda. Point vscode to that environment. 
- [Pytorch Mac GPU 训练与测评](https://zhuanlan.zhihu.com/p/517699916). Need to fix a few issues
  - Test function missed. Can be found at: https://github.com/pytorch/examples/blob/main/mnist/main.py
  - python mps_evaluation.py --use_gpu, Macbook pro with M1 chips: CPU 220.96 s, MPS 70.12 or 54.08s for 4 epoch. Quit big difference on the 2 runs, reason unknown.  provide about 3-4x on MNIST
  - PC with 4060 ti, CPU 980.26 s, GPU119.42 s for 14 epoch, about 8x on MNIST. 

**05-12-2024:** Preparation and explore

- Llama 3 ZH instruct: scomper/llama3-zh-inst:latest
- nvidia-smi -l 1: refresh GPU usage every second. 

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

- Calculate the GPU memory for LLMs training and inference

  - [[LLM]大模型显存计算公式与优化]([[LLM\]大模型显存计算公式与优化 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/687226668))

  - [多大的显存能够满足主流大模型的训练开销？]([多大的显存能够满足主流大模型的训练开销？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/636721650))

**05-10-2024:** Delete ubuntu

- Delete ubuntu
  - BIOS, BOOT, Set windows as 1st and Ubuntu as second. 
  - DiskGenius, delete the 200g partition. extend to the main system partition. 
  - Delete ubuntu folder under EFI, in the 100m system(0). 
- Pytorch - [Quickstart](https://pytorch.org/tutorials/beginner/basics/quickstart_tutorial.html)

**05-07-2024:** Make CUDA work, install ubuntu

- What works
  - Install: Typora, Github Desktop
  
  - Re-install CUDA 12.1.0, cudnn_9.1.1_windows, Anaconda,
    
    - ```
      conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
      ```
    
    - [A Step-by-Step Guide to Installing CUDA with PyTorch in Conda on Windows](https://medium.com/@harunijaz/a-step-by-step-guide-to-installing-cuda-with-pytorch-in-conda-on-windows-verifying-via-console-9ba4cd5ccbef)
    
    - Find the right version: 
      - [Pytorch - Start locally](https://pytorch.org/get-started/locally/)
      - Pytorch build: 2.3 or 2.4.1
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
