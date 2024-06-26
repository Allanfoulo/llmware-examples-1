

Wheel Archives: `llmware` pip install from pypy 
===============

**How to use?**

1.  Download a selected wheel, unzip, and then deploy the code directly into a project.   (Only selected wheels kept in the archive - raise an issue if there is a particular wheel you are looking for - and we can post by request.)  
2.  Place the wheel archive in a folder, and in that folder path, run:  

```pip3 install llmware-0.2.10-py3-none-any.whl```  

New wheels are built generally on PyPy on a weekly basis and updated on PyPy versioning.   The development repo is updated  
and current at all times, but may have updates that are not yet in the PyPy wheel.  

All wheels are built and tested on:  

1.  Mac Metal  
2.  Windows x86 (+ with CUDA)  
3.  Linux x86 (+ with CUDA) - most testing on Ubuntu 22 and Ubuntu 20 - which are recommended.  
4.  Mac x86 (see 0.2.11 note below)  
5.  Linux aarch64* (see 0.2.7 note below)  

**Release Notes**  

--**0.2.11** released in the week of April 29, 2024 - updated GGUF libs for Phi-3 and Llama-3 support, and added new prebuilt shared libraries to support WhisperCPP.  We are also deprecating support for Mac x86 going forward - will continue to support on most major components but not all new features going forward will be built specifically for Mac x86 (which Apple stopped shipping in 2022).  Our intent is to keep narrowing our testing matrix to provide better support on key platforms.  We have also added better safety checks for older versions of Mac OS running on M1/M2/M3 (no_acc option in GGUF and Whisper libs), as well as a custom check to find CUDA drivers on Windows (independent of Pytorch).  

--**0.2.9** released in the week of April 15, 2024 - minor continued improvements to the parsers plus roll-out of new CustomTable class for rapidly integrating structured information into LLM-based workflows and data pipelines, including converting JSON/JSONL files and CSV files into structured DB tables.  
  
--**0.2.8** released in the week of April 8, 2024 - significant improvements to the Office parser with new libs on all platforms.   Conforming changes with the PDF parser in terms of exposing more options for text chunking strategies, encoding, and range of capture options (e.g., tables, images, header text, etc).  Linux aarch64 libs deprecated and kept at 0.2.6 - some new features will not be available on Linux aarch64 - we recommend using Ubuntu20+ on x86_64 (with and without CUDA).  

--**0.2.7** released in the week of April 1, 2024 - significant improvements to the PDF parser with new libs on all platforms.   Important note that we are keeping linux aarch64 at 0.2.6 libs - and will be deprecating support going forward.  For Linux, we recommend Ubuntu20+ and x86_64 (with and without CUDA).  

--**0.2.5** released in the week of March 12, 2024 - continued enhancements of the GGUF implementation, especially for CUDA support, and re-compiling of all binaries to support Ubuntu 20 and Ubuntu 22.  Ubuntu requirements are:  CUDA 12.1 (to use GPU), and GLIBC 2.31+.  

--**GGUF on Windows CUDA**: useful notes and debugging tips -  

    1.  Requirement:  Nvidia CUDA 12.1+  
    
        -- how to check:  `nvcc --version` and `nvidia-smi` - if not found, then drivers are either not installed or not in $PATH and need to be configured 
        -- if you have older drivers (e.g., v11), then you will need to update them.  
        
    2.  Requirement:  CUDA-enabled Pytorch  (pre-0.2.11)  
    
        -- starting with 0.2.11, we have implemented a custom check to evaluate if CUDA is present, independent of Pytorch.  
        -- for pre-0.2.11, we use Pytorch to check for CUDA drivers, e.g., `torch.cuda.is_available()` and `torch.version.cuda`  

    3.  Installing a CUDA-enabled Pytorch - useful install script:  (not required post-0.2.11 for GGUF on Windows)  
    
        -- `pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121`  

    4.  Fall-back to CPU - if llmware can not load the CUDA-enabled drivers, it will automatically try to fall back to the CPU version of the drivers.  
    
        -- you can also adjust the GGUFConfigs().set_config - ("use_gpu", False) - and then it will automatically go to the CPU drivers.  

    5.  Custom GGUF libraries - if you have a unique system requirement, you can build llama_cpp from source, and apply custom build settings - or find in the community a prebuilt llama_cpp library that matches your platform.  Happy to help if you share the requirements.  

        -- to "bring your own GGUF":  GGUFConfigs().set_config("custom_lib_path", "/path/to/your/custom/llama_cpp_backend" -> and llmware will try to load that library.  

    6.  Issues?  - please raise an Issue on Github, or on Discord - and we can work with you to get you up and running!  
    
--**0.2.4** released in the week of February 26, 2024 - major upgrade of GGUF implementation to support more options, including CUDA support - which is the main source of growth in the size of the wheel package.   

  -- Note: We will look at making some of the CUDA builds as 'optional' or 'bring your own' over time.    
  -- Note: We will also start to 'prune' the list of wheels kept in the archive to keep the total repo size manageable for cloning.  

--**0.2.2** introduced SLIM models and the new LLMfx class, and the capabilities for multi-model, multi-step Agent-based processes.  

--**0.2.0** released in the week of January 22, 2024 - significant enhancements, including integration of Postgres and SQLite drivers into the c lib parsers.  

--New examples involving Postgres or SQLite support (including 'Fast Start' examples) will require a fresh pip install of 0.2.0 or clone of the repo.  

--If cloning the repo, please be especially careful to pick up the new updated /lib dependencies for your platform.  

--New libs have new dependencies in Linux in particular - most extensive testing on Ubuntu 22. If any issues on a specific version of Linux, please raise a ticket.  


