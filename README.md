# calculator
use of Tkinter


from tkinter import *

root=Tk()
root.title("CALCULATOR")
root.geometry("380x550+200+100")
root.resizable(False,False)

##### to start buttons work ######
def enter_number(x):
    if entry_box.get() == "0":
        if x==".":
            entry_box.insert(1,".")
        else:
            entry_box.delete(0,"end")
            entry_box.insert(0,x)
    else:
        length=len(entry_box.get())
        entry_box.insert(length,str(x))

##### function for operator to work #####
def enter_operator(x):
    if entry_box.get()!="0":
        length=len(entry_box.get())
        all_text=entry_box.get()
        last_char=all_text[-1:]

        if last_char in ["+","-","*","/"]:
            pass
        else:
            entry_box.insert(length, btn_operator[x]["text"])


def func_clr():
    entry_box.delete(0,END)
    entry_box.insert(0,"0")

result=0
history=[]
def func_equal():
    content=entry_box.get()
    result=eval(content)
    entry_box.delete(0,END)
    entry_box.insert(0,result)
    history.append(content)
    history.reverse()
    status.config(text="History : " + "|".join(history[0:4]),font="verdana 11 bold")

def func_del():
    length=len(entry_box.get())
    entry_box.delete(length-1,"end")
    if length == 1:
        entry_box.insert(0,"0")





#### entry box ####
entry_box=Entry(font="verdana 14 bold",width=22,bd=6,justif=RIGHT,bg="light blue")
entry_box.insert(0,"0")
entry_box.place(x=30,y=10)
#### buttons created in 2d array #####

btn_numbers=[]
for i in range(10):
    btn_numbers.append(Button(width=6,text=str(i),bd=6,command=lambda x=i:enter_number(x)))

btn_text=1
for i in range(0,3):
    for j in range(0,3):
        btn_numbers[btn_text].place(x=30+j*90, y=70+i*70)
        btn_text+=1

btn_zero=Button(width=14,text="0",bd=5,command=lambda x=0:enter_number(x))
btn_zero.place(x=25,y=280)

btn_clear=Button(width=14,text="C",bd=5,command=func_clr)
btn_clear.place(x=150,y=280)

btn_dot=Button(width=4,text=".",bd=5,command=lambda x=".":enter_number(x))
btn_dot.place(x=25,y=340)

status=Label(root, text="History :",height=3,relief=SUNKEN, font="verdana 11 bold",anchor=W)
status.pack(side=BOTTOM,fill=X)



##### button operator ####
btn_operator=[]
for i in range(4):
    btn_operator.append(Button(width=6,font="times 14 bold",bd=5,command=lambda x=i:enter_operator(x)))
btn_operator[0]["text"] = "+"
btn_operator[1]["text"] = "-"
btn_operator[2]["text"] = "*"
btn_operator[3]["text"] = "/"
for i in range(4):
    btn_operator[i].place(x=290,y=70+i*70)

btn_equal=Button(width=4,text="=",bd=5,command=func_equal)
btn_equal.place(x=100,y=340)

btn_delete=Button(width=4,text="DEL",bd=5,command=func_del)
btn_delete.place(x=180,y=340)





root.mainloop()
