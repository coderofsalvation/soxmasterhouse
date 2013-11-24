soxmasterhouse
==============

automatically mastering of audio using sox/ladspa/vst

### Why ###

I wanted to automate post-processing of music, specifically concerning
M/S processing.

### Howto ###

    git clone https://github.com/coderofsalvation/soxmasterhouse.git
    cd soxmasterhouse
    ./soxmasterhouse init mymasteringpreset
    ./soxmasterhouse process myfile.wav mymasteringpreset "00:00:01.00 00:04:01.00"
 
Or do this to have audiopreviews between every stage 

    SLEEP=1 PPRE=2 PMID=4 PSIDE=4 PPOST=5 ./soxmasterhouse process myfile.wav mymasteringpreset "00:00:01.00 00:04:01.00"

The above command will process the mid/side audio using my preset, and at every step (preprocessing,midprocessing,sideprocessing,postprocessing) it will preview the result to me (with 1 second of sleep in between the previewing).
  
This will allow me to fire up my editor (audacity/wavosaur) to analyze/edit the mid- or side-file before merging them together:

    MANUAL=1 ./soxmasterhouse process myfile.wav mymasteringpreset "00:00:01.00 00:04:01.00"

### What does a preset look like ###

Well thats up to you, you can go crazy with sox (Which supports ladspa) or MrsWatson/Misswatson for VST. however, this is your starting point after initing a preset:

    # 
    # bashmasteraudio configuration file 
    #
    
    process_pre(){
      input="$1"; output="$2"; echo "preprocessing"
      # aplay "$input" -d 2s # uncomment this to preview the dry signal
    }
    
    process_mid(){
      input="$1"; output="$2"; echo "processing mid of M/S"
      # aplay "$input" -d 2s # uncomment this to preview the dry signal
    }
    
    process_side(){
      input="$1"; output="$2"; echo "processing side of M/S"
      # aplay "$input" -d 2s # uncomment this to preview the dry signal
    }
    
    process_post(){
      input="$1"; output="$2"; echo "post processing "
      # aplay "$input" -d 2s # uncomment this to preview the dry signal
    }

For a more concrete example see the 'myexample'-dir.

### Requirements ###

* linux
* bash
* sox utilities

