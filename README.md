import tkinter as tk
from tkinter import messagebox
import qrcode
from PIL import ImageTk, Image

class QRCodeGeneratorApp:
    def __init__(self, master):
        self.master = master
        self.master.title("QR Code Generator")

        self.label = tk.Label(master, text="Enter text or URL:")
        self.label.pack()

        self.entry = tk.Entry(master, width=150)
        self.entry.pack()

        self.generate_button = tk.Button(master, text="Generate QR Code", command=self.generate_qr_code)
        self.generate_button.pack()

        self.qr_code_display = None

    def generate_qr_code(self):
        text = self.entry.get()
        if text:
            qr = qrcode.QRCode(version=1, box_size=16, border=7)
            qr.add_data(text)
            qr.make(fit=True)
            img = qr.make_image(fill='black', back_color='white')
            qr_code_image = ImageTk.PhotoImage(img)

            if self.qr_code_display:
                self.qr_code_display.destroy()

            self.qr_code_display = tk.Label(self.master, image=qr_code_image)
            self.qr_code_display.image = qr_code_image  
            self.qr_code_display.pack()
        else:
            messagebox.showerror("Error", "Please enter some text or URL.")
def main():
    root = tk.Tk()
    app = QRCodeGeneratorApp(root)
    root.mainloop()
if __name__ == "__main__":
    main()
