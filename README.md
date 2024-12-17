# EMG_RT_DEMO
Signal processing framework designed to balance noise reduction and latency for real-time EMG biofeedback
To enable real-time EMG biofeedback within the experimental protocol, a signal processing framework was designed to balancing noise reduction and latency. The raw EMG signal, sampled at 2000 Hz, is processed through three main filtering scenarios that involve different combinations of digital filters and envelope extraction methods.

Scenario 1: low-latency processing
•	Filters: high-pass Butterworth IIR filter, selective notch filter at the main powerline interference (50 Hz).
•	Envelope extraction: absolute value rectification followed by a moving average. The envelope extraction includes a downsampling at fs/f’s. 
•	Envelope Output Frequency f’s: 40 Hz, aligned with the frame rate of the Meta Quest 3 headset at 36 Hz.
•	Latency: approximately 25 ms, primarily due to the moving average delay, as the IIR filters were designed with low orders (4-6) to introduce negligible delays.
•	Use case: Biofeedback applications prioritizing speed over noise removal accuracy.

Scenario 2: enhanced noise removal
•	Filters: cascade of high-pass and low-pass Butterworth filters, or a band-pass Chebyshev/Elliptic filter, with a selective notch filter at main powerline interference (50 Hz) and its odd harmonics.
•	Envelope extraction: equals to Scenario 1.
•	Envelope Output Frequency f’s: 40 Hz, like in Scenario 1.
•	Latency: 25 ms for the same reasons of Scenario 1.
•	Use case: Biofeedback with improved signal quality, suitable for cases where better noice suppression is required.

Scenario 3: linear phase filtering
•	Filters: Equiripple FIR filters for high-pass and low-pass filtering, and a selective notch filter at all powerline harmonics.
•	Envelope Extraction: Root-mean-square (RMS) computation with a sliding window. The envelope extraction includes a downsampling at fs/f’s. 
•	Envelope Output Frequency f’s: 40 Hz, like in the previous scenarios. Alternatively, f’s could be higher than 40 Hz (e.g., through upsampling), making it more suitable for clinical analysis or feedback systems requiring higher temporal resolution.
•	Latency: approximately 90 ms, due to the higher FIR filter order and RMS windowing.
•	Use case: Biofeedback in applications where higher latency is acceptable or clinical applications needing precise linear phase filtering.
For more details download the pdf document ‘Algorithms for EMG processing and RT transmission’.
