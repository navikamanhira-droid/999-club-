import tkinter as tk
from random import choice

class ColorTradingGame:
    def __init__(self):
        self.root = tk.Tk()
        self.root.title("Color Trading Game")
        self.balance = 1000
        self.colors = ["Red", "Green", "Blue"]
        self.current_color = choice(self.colors)

        self.balance_label = tk.Label(self.root, text=f"Balance: {self.balance}")
        self.balance_label.pack()

        self.color_label = tk.Label(self.root, text=f"Current Color: {self.current_color}", font=("Arial", 24))
        self.color_label.pack()

        self.bet_entry = tk.Entry(self.root)
        self.bet_entry.pack()

        self.red_button = tk.Button(self.root, text="Red", command=lambda: self.bet("Red"))
        self.red_button.pack()

        self.green_button = tk.Button(self.root, text="Green", command=lambda: self.bet("Green"))
        self.green_button.pack()

        self.blue_button = tk.Button(self.root, text="Blue", command=lambda: self.bet("Blue"))
        self.blue_button.pack()

    def bet(self, color):
        bet_amount = int(self.bet_entry.get())
        if bet_amount > self.balance:
            self.balance_label['text'] = "Insufficient balance!"
            return

        self.balance -= bet_amount
        self.balance_label['text'] = f"Balance: {self.balance}"

        if color == self.current_color:
            self.balance += bet_amount * 2
            self.balance_label['text'] = f"Balance: {self.balance}"
            self.current_color = choice(self.colors)
            self.color_label['text'] = f"Current Color: {self.current_color}"
        else:
            self.current_color = choice(self.colors)
            self.color_label['text'] = f"Current Color: {self.current_color}"

    def run(self):
        self.root.mainloop()

if __name__ == "__main__":
    game = ColorTradingGame()
    game.run()
