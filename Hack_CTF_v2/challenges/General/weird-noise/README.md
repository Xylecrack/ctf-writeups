# Weird Noise

## Description

A friend of mine just sent me this really weird audio message. Please help me decode this!!!!

## Files

* [flag.wav](<files/flag.wav>)


## Challenge Writeup: SSTV Wave File

### Objective:
The task was to decode an image embedded in a **wave file** (`flag.wav`) using **Slow Scan Television (SSTV)**. The decoded image contains the flag in Base64 format, which needs to be further decoded to reveal the final flag.

### Steps Taken:

1. **Set Up Virtual Audio Sink**:
   - We used PulseAudio to create a virtual audio device that would serve as a “Null Output” for audio routing.
   
   ```
   pactl load-module module-null-sink sink_name=virtual-cable
   ```
   
2. **Verify Virtual Sink**:
   - We used the `pavucontrol` GUI (PulseAudio Volume Control) to verify that the "Null Output" device was created. In the "Output Devices" tab, we ensured that the virtual audio sink was available.
  ![image](https://github.com/user-attachments/assets/af9e5c3f-d989-4d17-aca1-7d6055e91a10)

3. **Configure QSSTV**:
   - The program **QSSTV** is used to decode SSTV signals. We configured QSSTV to use the "PulseAudio" audio interface to capture audio from the virtual sink.
   - In the **Options** -> **Configuration** -> **Sound** section, we selected the "PulseAudio" interface.

4. **Capture and Play the Audio**:
   - We played the `flag.wav` file using the `paplay` command, which sends audio data to the virtual sink.
   ```
   paplay -d virtual-cable flag.wav
   ```
  ![image](https://github.com/user-attachments/assets/9331787b-9e6c-4043-bc04-6afd4ef535fa)

5. **Extract the Image**:
   - After running the above commands, the **SSTV software** (QSSTV) decoded the audio, generating an image.
  ![flag](https://github.com/user-attachments/assets/33d6c3e5-ff42-43dd-b8bd-e53f5ebf20cc)

6. **Base64 Decoding**:
   - The resulting image displayed the flag in **Base64** format. We extracted the Base64 string `aGFja3N7c3N0dl9yMGNrc30=` and decoded it to reveal the final flag.

### Flag:
The final flag was revealed after decoding the Base64 string from the SSTV image.
hacks{sstv_r0cks}
