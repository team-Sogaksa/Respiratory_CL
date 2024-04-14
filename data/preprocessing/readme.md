1. dataset split
    - train/val/test: `7`:`1.5`:`1.5` (or `7`:`1`:`2`)
2. preprocessing:
    - processing ouliers
    - filtering
    - data segment 7 seconds
    - zero padding
    - etc

3. changing data format 
    - txt to xml
    - wav to png(mel spectrogram)
    - xml to yolobox(for Ultralytics)
    - xml to csv(for torch API)
    - save data
