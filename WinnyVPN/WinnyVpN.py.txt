import tkinter as tk
import subprocess
import os

root = tk.Tk()
root.title("WinnyVPN")
root.geometry("420x520")
root.configure(bg="#101010")
root.resizable(False, False)

title = tk.Label(
    root,
    text="WinnyVPN",
    font=("Segoe UI", 28, "bold"),
    fg="#35e875",
    bg="#101010"
)
title.pack(pady=(45, 10))

subtitle = tk.Label(
    root,
    text="YOUR PRIVATE CONNECTION",
    font=("Segoe UI", 10),
    fg="#999999",
    bg="#101010"
)
subtitle.pack(pady=(0, 35))

status = tk.Label(
    root,
    text="VPN STATUS: NOT VERIFIED",
    font=("Segoe UI", 10),
    fg="#bbbbbb",
    bg="#101010"
)
status.pack(pady=10)

def connect():
    paths = [
        os.path.expandvars(
            r"%LOCALAPPDATA%\Programs\ProtonVPN\ProtonVPN.exe"
        ),
        r"C:\Program Files\Proton\VPN\ProtonVPN.exe",
        r"C:\Program Files (x86)\Proton\VPN\ProtonVPN.exe",
    ]

    for path in paths:
        if os.path.isfile(path):
            subprocess.Popen([path])
            status.config(
                text="PROTON VPN OPENED — CONNECT THERE",
                fg="#35e875"
            )
            return

    status.config(
        text="OPENING PROTON VPN...",
        fg="#bbbbbb"
    )
    try:
        os.startfile("protonvpn:")
    except OSError:
        status.config(
            text="PLEASE OPEN PROTON VPN MANUALLY",
            fg="#ff7777"
        )

button = tk.Button(
    root,
    text="CONNECT",
    command=connect,
    font=("Segoe UI", 15, "bold"),
    fg="#07140b",
    bg="#35e875",
    activebackground="#28c764",
    activeforeground="#07140b",
    relief="flat",
    cursor="hand2",
    width=18,
    height=2
)
button.pack(pady=30)

footer = tk.Label(
    root,
    text="Powered by Proton VPN",
    font=("Segoe UI", 9),
    fg="#666666",
    bg="#101010"
)
footer.pack(side="bottom", pady=22)

root.mainloop()