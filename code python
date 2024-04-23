import re
from tkinter import *
import qrcode
from PIL import Image, ImageTk
from resizeimage import resizeimage

class QR_code:
    def __init__(self, root):
        self.root = root
        self.root.title("Formulaire QR code")
        self.root.geometry("1500x900+200+50")
        self.root.resizable(False, False)  
        title = Label(self.root, text="Génération de code", font=('times new roman', 40), bg="blue", fg="white", anchor="w")
        title.pack(fill=X)  
        self.var_prenom=StringVar()
        self.var_nom=StringVar()
        self.var_email=StringVar()
        self.var_depar=StringVar()

        emplo_Frame=Frame(self.root,bd=2,relief=RIDGE,bg="white")
        emplo_Frame.place(x=50,y=150,height=500,width=700)

        prenom=Label(emplo_Frame,text="Prenom",font=("times new roman",25,"bold"),bg="white").place(x=50,y=70)
        nom=Label(emplo_Frame,text="Nom",font=("times new roman",25,"bold"),bg="white").place(x=50,y=120)
        email=Label(emplo_Frame,text="E-mail",font=("times new roman",25,"bold"),bg="white").place(x=50,y=170)
        departent=Label(emplo_Frame,text="Depatement",font=("times new roman",25,"bold"),bg="white").place(x=50,y=220)
       
       
        txt_prenom=Entry(emplo_Frame,font=("times new roman",25),textvariable=self.var_prenom,bg="lightyellow")
        txt_prenom.place(x=300,y=70)
        txt_nom=Entry(emplo_Frame,font=("times new roman",25),textvariable=self.var_nom,bg="lightyellow")
        txt_nom.place(x=300,y=120)
        txt_email=Entry(emplo_Frame,font=("times new roman",25),textvariable=self.var_email,bg="lightyellow")
        txt_email.place(x=300,y=170)
        txt_departement=Entry(emplo_Frame,font=("times new roman",25),textvariable=self.var_depar,bg="lightyellow")
        txt_departement.place(x=300,y=220)

        btn_valide=Button(emplo_Frame,text='Valider',font=("times new roman",15,"bold"), bg="green",fg='black',command=self.valider,bd=10,relief=GROOVE,cursor="hand2")
        btn_valide.place(x=400,y=300)     
        btn_annuler=Button(emplo_Frame,text='annuler',font=("times new roman",15,"bold"),fg='black',bd=10,command=self.annuler,relief=GROOVE,cursor="hand2", bg="red").place(x=520,y=300)

        self.msg=''
        self.lblmessage=Label(emplo_Frame,text=self.msg,font=("times new roman",20),bg="white",fg="green")
        self.lblmessage.place(x=0,y=410,relwidth=1)

        qrcode_frame=Frame(self.root,bd=2,relief=RIDGE,bg="white")
        qrcode_frame.place(x=900,y=150,height=500,width=500)

        qrcode_label = Label(qrcode_frame,text='Qr CODE',font=("Algiran",30),bg='blue',fg="white").place(x=0,y=0,width=500)

        self.qr_code = Label(qrcode_frame, text='Pas de QR code \n Disponible', font=("times new roman", 15), bd=20, relief=GROOVE, bg="gray")
        self.qr_code.place(x=100, y=100, height=300, width=300)

    def validate_email(self, email):
        
        pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
        if re.match(pattern, email):
            return True
        else:
            return False

    def valider(self):
        if (self.var_prenom.get() == '' or
            self.var_nom.get() == '' or
            self.var_email.get() == '' or
            self.var_depar.get() == ''):
            self.msg = "Vous n'avez pas rempli tous les champs"
            self.lblmessage.config(text=self.msg, fg="red")
        elif not self.validate_email(self.var_email.get()):
            self.msg = "Adresse e-mail invalide"
            self.lblmessage.config(text=self.msg, fg="red")
        else:
            qr_info = (f"Prenom:{self.var_prenom.get()}\n nom : {self.var_nom.get()}\n E-mail:{self.var_email.get()}\n Departement:{self.var_depar.get()}")
            qr_code = qrcode.make(qr_info)

            qr_code = resizeimage.resize_cover(qr_code,[300,300])
            qr_code.save("Nom_" + str(self.var_nom.get() + '.png'))
            self.im = ImageTk.PhotoImage(qr_code)
            self.qr_code.config(image=self.im)   
            self.qr_code.image = self.im  

            self.msg= "Enregistrement effectué"
            self.lblmessage.config(text=self.msg,fg="green") 

            self.qr_code.place(x=150, y=150, height=290, width=290)

    def annuler(self):
        self.var_prenom.set("")
        self.var_nom.set("")
        self.var_email.set("")
        self.var_depar.set("")
        self.mgs=""
        self.lblmessage.config(text=self.msg)
        self.qr_code.config(image="")
        self.qr_code.place(x=100, y=100, height=300, width=300)

root = Tk()
obj = QR_code(root)
root.mainloop()
