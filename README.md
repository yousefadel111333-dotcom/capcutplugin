# capcutplugin
capcutplugin
import arabic_reshaper
from bidi.algorithm import get_display
import pyautogui
import keyboard
import time
import pyperclip
import threading
import tkinter as tk
from tkinter import messagebox

# ﻲﺑﺮﻌﻟﺍ ﺺﻨﻟﺍ ﺢﻴﺤﺼﺗ ﺔﻟﺍﺩ
def fix_arabic(text):
    reshaped = arabic_reshaper.reshape(text)
    bidi_text = get_display(reshaped)
    return bidi_text

# ﺔﻴﻔﻠﺨﻟﺍ ﻲﻓ ﺖﺒﻳﺮﻜﺴﻟﺍ ﻞﻴﻐﺸﺗ ﺔﻟﺍﺩ
def start_script():
    def run():
        messagebox.showinfo("ﻡﺪﺨﺘﺳﺍ !ﻞﻤﻌﻟﺍ ﺃﺪﺑ ﺞﻣﺎﻧﺮﺒﻟﺍ" ,"ﻞﻴﻐﺸﺘﻟﺍ ﻢﺗ Ctrl+1 ﺹﻮﺼﻨﻟﺍ ﺢﻴﺤﺼﺘﻟ.")
        while True:
            keyboard.wait('ctrl+1')
            pyautogui.hotkey("ctrl", "a")
            time.sleep(0.05)
            pyautogui.hotkey("ctrl", "x")
            time.sleep(0.2)

            wrong_text = pyperclip.paste()
            if wrong_text.strip():
                fixed_text = fix_arabic(wrong_text)
                pyperclip.copy(fixed_text)
                time.sleep(0.05)
                pyautogui.hotkey("ctrl", "v")
            
            time.sleep(0.5)

    threading.Thread(target=run, daemon=True).start()

# ﺔﻬﺟﺍﻭ ﺀﺎﺸﻧﺇ Tkinter
root = tk.Tk()
root.title("ﻲﺑﺮﻌﻟﺍ ﺺﻨﻟﺍ ﺢﺤﺼﻣ")
root.geometry("350x150")
root.resizable(False, False)

label = tk.Label(root, text="ﺢﺤﺼﻤﻟﺍ ﻞﻴﻐﺸﺘﻟ 'ﺃﺪﺑﺍ' ﻂﻐﺿﺍ", font=("Arial", 12))
label.pack(pady=20)

start_button = tk.Button(root, text="ﺃﺪﺑﺍ", font=("Arial", 12, "bold"), command=start_script)
start_button.pack(pady=10)

root.mainloop()
