import tkinter as tk
from matplotlib.figure import Figure
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg

# Function to clear old graph before plotting new
def clear_canvas():
    for widget in frame_graph.winfo_children():
        widget.destroy()

def show_bar_graph():
    clear_canvas()
    subjects = ["Math", "Science", "English", "History"]
    marks = [85, 90, 75, 60]

    fig = Figure(figsize=(5, 4), dpi=100)
    plot = fig.add_subplot(111)
    plot.bar(subjects, marks, color="skyblue")
    plot.set_title("Student Marks")
    plot.set_ylabel("Marks")

    canvas = FigureCanvasTkAgg(fig, master=frame_graph)
    canvas.draw()
    canvas.get_tk_widget().pack()

def show_line_graph():
    clear_canvas()
    months = ["Jan", "Feb", "Mar", "Apr", "May"]
    sales = [100, 150, 120, 180, 200]

    fig = Figure(figsize=(5, 4), dpi=100)
    plot = fig.add_subplot(111)
    plot.plot(months, sales, marker="o", color="green")
 plot.set_title("Monthly Sales")
    plot.set_ylabel("Sales")

    canvas = FigureCanvasTkAgg(fig, master=frame_graph)
    canvas.draw()
    canvas.get_tk_widget().pack()

def show_multiple_graphs():
    clear_canvas()
    x = [1, 2, 3, 4, 5]
    y1 = [1, 4, 9, 16, 25]
    y2 = [25, 20, 15, 10, 5]

    fig = Figure(figsize=(6, 5), dpi=100)

    # Line graph
    # 211 == 
    ax1 = fig.add_subplot(211)
    ax1.plot(x, y1, marker="o", color="blue", label="Squares")
    ax1.set_title("Line Graph")
    ax1.legend()

    # Bar graph
    ax2 = fig.add_subplot(212)
    ax2.bar(x, y2, color="orange")
    ax2.set_title("Bar Graph ")

    # 🔹 Add vertical spacing between the subplots
    fig.subplots_adjust(hspace=0.6)

    canvas = FigureCanvasTkAgg(fig, master=frame_graph)
    canvas.draw()
    canvas.get_tk_widget().pack()
# ------------------- GUI -------------------
window = tk.Tk()
window.title("Matplotlib Multiple Graphs")
window.geometry("700x600")

# Frame for buttons
frame_buttons = tk.Frame(window)
frame_buttons.pack(side=tk.TOP, pady=10)

# Buttons
tk.Button(frame_buttons, text="Show Bar Graph", command=show_bar_graph, width=20, bg="lightblue").pack(side=tk.LEFT, padx=5)
tk.Button(frame_buttons, text="Show Line Graph", command=show_line_graph, width=20, bg="lightgreen").pack(side=tk.LEFT, padx=5)
tk.Button(frame_buttons, text="Show Multiple Graphs", command=show_multiple_graphs, width=20, bg="lightcoral").pack(side=tk.LEFT, padx=5)

# Frame for graph
frame_graph = tk.Frame(window)
frame_graph.pack(fill=tk.BOTH, expand=True)

window.mainloop()
