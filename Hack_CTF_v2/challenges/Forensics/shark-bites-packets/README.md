# Shark Bites Packets!

## Description

During a network investigation, you intercepted suspicious traffic in the provided PCAP file. It seems the attacker has hidden a secret within the packets, split into parts... can you uncover the truth?

## Files

* [ctf.pcap](<files/ctf.pcap>)

### Steps Followed:

1. Open the provided `ctf.pcap` file in Wireshark.
2. Identify the HTTP stream in the captured packets.
   - Use the "Follow HTTP Stream" option to analyze the HTTP data.
3. Export HTTP objects:
   - Go to **File > Export Objects > HTTP** in Wireshark.
   - Save the exported HTTP files.
4. Two HTTP files are obtained after export.
5. Rename the file extensions of both exported files to `.png`.
   - These files are two parts of the flag.
6. Combine the two parts to reconstruct the full flag.

### Final Flag:
hacks{sh4rk_b1t3$_p4ck37$}
