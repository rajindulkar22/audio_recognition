# audio_recognition
node listens to the /audio_stream topic (coming from your Brio 100 mic published by audio_hub_node.py),runs voice activity detection (VAD) to know when someone is speaking,sends those voice segments into OpenAI Whisper,extracts the recognized text,and checks whether any distress keywords (from words_en.txt) appear in that speech.
