import psutil
import tkinter as tk
from tkinter import ttk

def update():
    for row in tree.get_children():
        tree.delete(row)
    
    count = 0
    for proc in psutil.process_iter(['pid','name','memory_percent','memory_info']):
        try:
            info = proc.info
            mb = info['memory_info'].rss/1024/1024 if info['memory_info'] else 0
            mem = info['memory_percent'] or 0
            
            tree.insert('', 'end', values=(
                info['pid'],
                info['name'][:25],
                f"{mem:.1f}%",
                f"{mb:.1f}"
            ))
            count += 1
            if count >= 25:
                break
        except:
            continue
    
    root.after(3000, update)

root = tk.Tk()
root.title("ProcMon")
root.geometry("600x400")

tree = ttk.Treeview(root, columns=('PID','Name','Mem%','MemMB'), show='headings', height=15)
tree.heading('PID', text='PID')
tree.heading('Name', text='Name')
tree.heading('Mem%', text='Mem%')
tree.heading('MemMB', text='MemMB')

tree.column('PID', width=70)
tree.column('Name', width=200)
tree.column('Mem%', width=80)
tree.column('MemMB', width=80)

tree.pack(fill=tk.BOTH, expand=True, padx=10, pady=10)

update()
root.mainloop()
