import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

def generate_ask_signal(bits, bit_rate, carrier_freq, amplitude):
    time_per_bit = 1 / bit_rate
    t = np.linspace(0, len(bits) * time_per_bit, len(bits) * 1000)
    carrier_signal = amplitude * np.sin(2 * np.pi * carrier_freq * t)

    ask_signal = [1]
    for bit in bits:
        if bit == '1':
            ask_signal.extend(amplitude * np.sin(2 * np.pi * carrier_freq * t[t <= time_per_bit]))
        else:
            ask_signal.extend(np.zeros(len(t[t <= time_per_bit])))

    return t, ask_signal, carrier_signal

def plot_ask_signal(t, ask_signal, carrier_signal):
    plt.figure(figsize=(10, 6))
    plt.subplot(3, 1, 1)
    plt.plot(t, ask_signal, label='ASK Signal')
    plt.title('Amplitude Shift Keying (ASK) Signal')
    plt.xlabel('Time')
    plt.ylabel('Amplitude')
    plt.legend()

    plt.subplot(3, 1, 2)
    plt.plot(t, carrier_signal, label='Carrier Signal')
    plt.title('Carrier Signal')
    plt.xlabel('Time')
    plt.ylabel('Amplitude')
    plt.legend()

    plt.subplot(3, 1, 3)
    plt.plot(t, ask_signal, label='ASK Signal')
    plt.plot(t, carrier_signal, label='Carrier Signal')
    plt.title('Combined Signal')
    plt.xlabel('Time')
    plt.ylabel('Amplitude')
    plt.legend()

    plt.tight_layout()
    st.pyplot(plt)

def main():
    st.title('Amplitude Shift Keying (ASK) Signal Generator')
    
    # Memasukkan urutan bit sebagai string tanpa spasi, contoh: "101010"
    bits_input = st.text_input("Masukkan urutan bit (0 dan 1, tanpa spasi): ", "101010")
    
    # Memasukkan bit rate, carrier frequency, dan amplitude sebagai angka
    bit_rate = st.number_input("Masukkan tingkat bit (bit per detik): ", 100)
    carrier_freq = st.number_input("Masukkan frekuensi pembawa: ", 10)
    amplitude = st.number_input("Masukkan amplitudo sinyal: ", 1)

    if st.button('Generate and Plot ASK Signal'):
        t, ask_signal, carrier_signal = generate_ask_signal(bits_input, bit_rate, carrier_freq, amplitude)
        plot_ask_signal(t, ask_signal, carrier_signal)

if _name_ == '_main_':
    main()
