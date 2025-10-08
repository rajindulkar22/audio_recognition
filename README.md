# audio_recognition
node listens to the /audio_stream topic (coming from your Brio 100 mic published by audio_hub_node.py),runs voice activity detection (VAD) to know when someone is speaking,sends those voice segments into OpenAI Whisper,extracts the recognized text,and checks whether any distress keywords (from words_en.txt) appear in that speech.

Audio input:-sounddevice (from another node)  /audio_stream :-streams 16 kHz audio

VAD (Voice Activity Detection):-webrtcvad :-frame-wise speech/non-speech detection

Noise reduction:-noisereduce :-cleans background hum before transcription

Speech recognition:-openai-whisper model "small" :-converts speech → text and auto-detects language

Keyword matching:-rapidfuzz (Levenshtein / fuzzy matching) :-detects similar phrases to your distress words

captures mic audio (sounddevice)


Audio Input               Captures mic audio at 16 kHz from Brio 100  `sounddevice` 

Voice Activity Detection  Detects speech vs. silence                  `webrtcvad`    

Noise Reduction          Removes background noise                    `noisereduce`   

Transcription             Converts speech → text                      **OpenAI Whisper “small”**   

Language Filter           Keeps only English or German                Whisper auto-detect     

Fuzzy Keyword Match       Finds similar emergency words              `rapidfuzz`   

ROS 2 Publish            Sends alerts to other nodes                `rclpy`, `/detected_keywords_en/de` 

 Merge Node                Combines EN + DE into one stream           `audio_hub_node.py`                 
