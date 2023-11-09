- 👋 Hi, I’m @MrJaturonM
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
MrJaturonM/MrJaturonM is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

from tkinter import* #เรียกใช้ tkinter

import json

#สร้าง GUI และตั้ง title
window = Tk()
window.title('โปรแกรมคำนวณหาค่า Mol')
window.geometry('1600x900')

#สร้าง frame
frame1 = LabelFrame(window,text='สูตรการคำนวน',width=300,height=150,font=('Tahoma',20))
frame1.place(x=10, y=10)

#สร้างข้อความใน frame 1
labelmol = Label(frame1,text='โมแลลิตี (m) =',font=('Tahoma',8))
labelmol.place(x=10 ,y=50)

#สร้างข้อความใน frame 2
labelถูก = Label(frame1,text='จำนวนโมลตัวถูกละลาย(mol)',font=('Tahoma',8))
labelถูก.place(x=100 ,y=35)

#สร้างเส้นเศษส่วน
label2 = Label(frame1,text='_________________________',font=('Tahoma',8))
label2.place(x=100 ,y=50)

#สร้างข้อความใน frame 3
label2 = Label(frame1,text='มวลตัวทำละลาย(kg)',font=('Tahoma',8))
label2.place(x=115,y=75)


#สร้างคำแนะนำ
labelad = Label(text='คำแนะนำ : โปรดระบุโมลของน้ำตาลทรายและระบุมวลของน้ำเพื่อคำนวนหาโมเลลิติ(m)ของน้ำตาลที่ละลายในน้ำ ปุ่มล้างค่า ล้างช่องคำตอบไม่ได้ซึ่งสามารถคำวนวนใหม่ทับคำตอบเก่าได้เลย และห้ามพิมพ์ลงในช่องโมแลลิตี เด็ดขาด!!!',font=('Tahoma',8))
labelad.place(x=10,y=180)

#สร้าง frame3 ไว้เก็บข้อมูลและคำนวน
frame3 = LabelFrame(window,text='ช่องใส่ข้อมูล',width=380,height=100,font=('Tahoma',20))
frame3.place(x=10,y=230)

#สร้าง label เก็บข้อมูลโมลน้ำตาลทราย
labelmolsugar = Label(frame3,text='ค่าโมลของน้ำตาลทราย',font=('Tahoma',8))
labelmolsugar.place(x=10,y=10)

labelmolsugarentryext = IntVar()

labelmolsugarentry = Entry(frame3,width=20,textvariable=labelmolsugarentryext)
labelmolsugarentry.place(x=120,y=10)

labelmolsugar2 = Label(frame3,text='mol',font=('Tahoma',8))
labelmolsugar2.place(x=250,y=10)

#สร้าง label เก็บข้อมูลมวลน้ำ
labelmh2o = Label(frame3,text='มวลของน้ำ',font=('Tahoma',8))
labelmh2o.place(x=10,y=30)

labelmh2oentryext = IntVar()

labelmh2oentry = Entry(frame3,width=20,textvariable=labelmh2oentryext)
labelmh2oentry.place(x=120,y=30)

labelmh2o2 = Label(frame3,text='kg',font=('Tahoma',8))
labelmh2o2.place(x=250,y=30)

#สร้าง label เก็บข้อมูลคำตอบ
molarity = Label(frame3,text='โมแลลิติ',font=('Tahoma',8))
molarity.place(x=10,y=50)

molarityext = IntVar()

molarityentry = Entry(frame3,width=20,textvariable=molarityext)
molarityentry.place(x=120,y=50)

molarity2 = Label(frame3,text='M',font=('Tahoma',8))
molarity2.place(x=250,y=50)

#สร้าง frame แสดงคำตอบ
frame4 = LabelFrame(window,text='คำตอบ',width=380,height=200,font=('Tahoma',20))
frame4.place(x=400,y=230)

#สร้าง command เพื่อคำนวน
def calculate():
    mol = labelmolsugarentryext.get()
    kg = labelmh2oentryext.get()
    M = mol/kg
    molarityentry.insert(0,M)
    ans.set(molarityentry.get())
    

#สร้าง stringvar เพื่อแสดงคำตอบใน frame
ans = StringVar(frame4)
ans.set('X')
anst = Label(frame4,textvariable=ans,font=("Thahoma",65))
anst.place(x=20,y=10)

#สร้าง command เพื่อล้างค่า(ล้างค่าที่แสดงไม่ได้เนื่องจาก StringVar ไม่มีคำสั่่งลบ)
def delete(): 
    labelmolsugarentry.delete(0,END)
    labelmh2oentry.delete(0,END)
    molarityentry.delete(0,END)

#สร้างคำสั่งดูประวัติ
def save():
    x = {
        "mol":labelmolsugarentry.get(),
        "mass":labelmh2oentry.get(),
        "M" :molarityentry.get()
        }
    y = json.dumps(x)
    f = open("x.txt","a")
    f.write(y)
    print(y)
    f.close()

#สร้างหมายเหตุ  
labelad2 = Label(text='หมายเหตุ : ดูประวัติได้ที่โปรแกรม IDEL',font=('Tahoma',15))
labelad2.place(x=10,y=420)

#สร้าง ปุ่มคำนวน
bc = Button(text='คำนวน', width=20, command=calculate,font=('Tahoma',10))
bc.place(x=10, y=350)

#สร้าง ปุ่มล้างค่า
bd = Button(text='ล้างค่า', width=20, command=delete,font=('Tahoma',10))
bd.place(x=200, y=350)

#สร้าง ปุ่มดูประวัติ
bs = Button(text='ดูประวัติ', width=20, command=save,font=('Tahoma',10))
bs.place(x=10, y=390)


window.mainloop()
