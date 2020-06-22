# COVID19simulator
This program calculates the number of patients that would be infected by COVID-19 over some time that is input by the user. The user can select initial conditions and the program will graphically show the changes that occur in the number of infected, recovered, and dead patients over time.

from tkinter import *
from PIL import ImageTk,Image
import matplotlib
matplotlib.use('TkAgg')
import numpy as np
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
from matplotlib.figure import Figure
from tkinter import messagebox
import matplotlib.patches as mpatches
import matplotlib.pyplot as plt





master = Tk()
Frame(master)
master.grid()
master.geometry('1600x900')


def About():
    messagebox.showinfo("About","This program calculates the number of patients that would be infected by COVID-19 over some time that is input by the user. The user can select initial conditions and the program will graphically show the changes that occur in the number of infected, recovered, and dead patients over time.")

def fullscreenn():
    master.attributes("-fullscreen", True)
    master.bind("<F11>", lambda event: master.attributes("-fullscreen",not master.attributes("-fullscreen")))
    master.bind("<Escape>", lambda event: master.attributes("-fullscreen", False))

    messagebox.showinfo("!!",'Press Escape to Exit full screen')


w = Canvas(master, width=1600, height=900)
w.grid()

Full = Button(master, text = "Full screen", command = fullscreenn , anchor = W)
Full.configure(width = 10, relief = RAISED)
Full_window = w.create_window(1300, 600, anchor=NW, window=Full)

about = Button(master, text = "About", command = About , anchor = W)
about.configure(width = 10, relief = RAISED)
about_window = w.create_window(1300, 400, anchor=NW, window=about)

w.create_line(50, 140, 1500, 140)

w.create_text(120, 120, text='COVID-SIMULATOR')
#w.create_text(950, 350, text='BAR GRAPH')

w.create_rectangle(50, 100, 1500, 750)

w.create_rectangle(1250, 180, 1450, 720) #buttonns


#gif1 = PhotoImage(file='C:/users/Dell/Desktop/dsa.png')
#w.create_image(50, 10, image=gif1,anchor=NW)

photo = Image.open('C:/users/Dell/Desktop/dsa.jpeg')
photo = photo.resize((600, 550), Image.ANTIALIAS)
photo = ImageTk.PhotoImage(photo)

w.create_image(370,450, image=photo, anchor='c')


button1 = Button(master, text = "Quit", command = master.quit, anchor = W)
button1.configure(width = 10, relief = RAISED)
button1_window = w.create_window(1300, 300, anchor=NW, window=button1)
#########


def plot1(A):
 
    y3 = A[1]
    y2 = A[2]
    y1 = A[3]
    x = A[0]
 

    fig = Figure(figsize=(5,5.2),dpi=105)
    
    plt = fig.add_subplot(111)
    plt.stackplot(x, y1, y2, y3, colors=['gray', 'green', 'red'])
    
    plt.set_title ('COVID patients', fontsize=16)
    plt.set_ylabel('People', fontsize=14)
    plt.set_xlabel('Days', fontsize=14)
     
    
    red_patch = mpatches.Patch(color='red', label='infected')
    green_patch = mpatches.Patch(color='green', label='recovered')
    gray_patch = mpatches.Patch(color='gray', label='dead')
    plt.legend(handles = [red_patch, green_patch, gray_patch], loc = 'upper left')
    
    
    w = FigureCanvasTkAgg(fig, master)
    w.get_tk_widget().grid(row=0,column=0,columnspan = 10,padx=710)
    
    w.draw()

    










Population={'Karachi Central': 2972639, 'Karachi East': 2909921, 'Karachi South': 1791751, 'Karachi West': 3914757, 'Korangi': 2457019, 'Malir': 2008901}
Population['Karachi']=Population['Karachi Central']+Population['Karachi East']+Population['Karachi South']+Population['Karachi West']+Population['Korangi']+Population['Malir']
parksAndRec={'Karachi Central': 16, 'Karachi East': 38, 'Karachi South': 30, 'Karachi West': 5, 'Korangi': 5, 'Malir': 8}
parksAndRec['Karachi']=parksAndRec['Karachi Central']+parksAndRec['Karachi East']+parksAndRec['Karachi South']+parksAndRec['Karachi West']+parksAndRec['Korangi']+parksAndRec['Malir']
Schools={'Karachi Central': 644, 'Karachi East': 338, 'Karachi South': 573, 'Karachi West': 422, 'Korangi': 677, 'Malir': 647}
Schools['Karachi']=Schools['Karachi Central']+Schools['Karachi East']+Schools['Karachi South']+Schools['Karachi West']+Schools['Korangi']+Schools['Malir']
mosques={'Karachi Central': 555, 'Karachi East': 544, 'Karachi South': 335, 'Karachi West': 732, 'Korangi': 459, 'Malir': 375}
mosques['Karachi']=mosques['Karachi Central']+mosques['Karachi East']+mosques['Karachi South']+mosques['Karachi West']+mosques['Korangi']+mosques['Malir']
malls={'Karachi Central': 17, 'Karachi East': 17, 'Karachi South': 10, 'Karachi West': 22, 'Korangi': 14, 'Malir': 11}
malls['Karachi']=malls['Karachi Central']+malls['Karachi East']+malls['Karachi South']+malls['Karachi West']+malls['Korangi']+malls['Malir']


c = []

def Place1(C):
    global c
    if c == []:
        c = [C]
    elif C not in c:
        c.append(C)     
    print(c)

label10 = Label(master, text= 'Please enter which area you would like to simulate the pandemic over? (select on map) ')
w.create_window(950, 200, window=label10)

label13 = Label(master, text= 'Please select which of the following areas of high contact will be open: ')
w.create_window(950, 350, window=label13)

Malls = Button(master, text='Malls', command= lambda: Place1('malls'), anchor=W)
Malls.configure(width=10, relief=RAISED)
Malls_window = w.create_window(750, 375, anchor=NW, window=Malls)

Schools = Button(master, text='Schools', command= lambda : Place1('Schools'), anchor=W)
Schools.configure(width=10, relief=RAISED)
Schools_window = w.create_window(850, 375, anchor=NW, window=Schools)

ParkandRec = Button(master, text='ParkandRec', command= lambda: Place1('parksAndRec'), anchor=W)
ParkandRec.configure(width=10, relief=RAISED)
ParkandRec_window = w.create_window(950, 375, anchor=NW, window=ParkandRec)

Mosques = Button(master, text='Mosque', command= lambda:Place1('mosques'), anchor=W)
Mosques.configure(width=10, relief=RAISED)
Mosques_window = w.create_window(1050, 375, anchor=NW, window=Mosques)

def Area(A):
    global b
    b = A
    print(b)
    

    
Active = Entry(master) 
w.create_window(950, 275, window=Active)
label11 = Label(master, text= 'Please enter how many current active cases there are today')
w.create_window(950, 250, window=label11)

timee = Entry(master) 
w.create_window(950, 325, window=timee)
label12 = Label(master, text= 'Please enter how long the simulation will run for (in days)')
w.create_window(950, 300, window=label12)

def Place2(D):
    global d
    d = D
    print(d)


Unimposed = Button(master, text='Unimposed', command= lambda:Place2('unimposed'), anchor=W)
Unimposed.configure(width=10, relief=RAISED)
Unimposed_window = w.create_window(800, 475, anchor=NW, window=Unimposed)

Moderate = Button(master, text='Moderate', command= lambda:Place2('moderate'), anchor=W)
Moderate.configure(width=10, relief=RAISED)
Moderate_window = w.create_window(900, 475, anchor=NW, window=Moderate)

Strict = Button(master, text='Strict', command= lambda:Place2('strict'), anchor=W)
Strict.configure(width=10, relief=RAISED)
Strict_window = w.create_window(1000, 475, anchor=NW, window=Strict)

label14 = Label(master, text= 'Please select the level of social distancing being practiced')
w.create_window(950, 425, window=label14)

def Place3(E):
    global e
    e = E
    print(e)


Prepared = Button(master, text='Prepared', command= lambda:Place3('prepared'), anchor=W)
Prepared.configure(width=10, relief=RAISED)
Prepared_window = w.create_window(850, 575, anchor=NW, window=Prepared)

Unprepared = Button(master, text='Unprepared', command= lambda:Place3('unprepared'), anchor=W)
Unprepared.configure(width=10, relief=RAISED)
Unprepared_window = w.create_window(950, 575, anchor=NW, window=Unprepared)

label15 = Label(master, text= 'Please select the state of available medical care in this area (prepared, unprepared)')
w.create_window(950, 550, window=label15)


########### Districts


Central = Button(master, text='Central', command= lambda: Area('Karachi Central'))
Central.configure(width=10, relief=RAISED)
Central_window = w.create_window(300, 600, window=Central)

K = Button(master, text='Karachi', command= lambda : Area('Karachi'), anchor=W)
K.configure(width=10, relief=RAISED)
K_window = w.create_window(200, 300, anchor=NW, window=K)


KE = Button(master, text='East', command= lambda: Area('Karachi East'), anchor=W)
KE.configure(width=5, relief=RAISED)
KE_window = w.create_window(350, 580, anchor=NW, window=KE)


KW = Button(master, text='West', command= lambda : Area('Karachi West'), anchor=W)
KW.configure(width=10, relief=RAISED)
KW_window = w.create_window(200, 600, anchor=NW, window=KW)

KS = Button(master, text='South', command= lambda :Area('Karachi South'), anchor=W)
KS.configure(width=5, relief=RAISED)
KS_window = w.create_window(300, 650, anchor=NW, window=KS)

Korangi = Button(master, text='Korangi', command= lambda: Area('korangi'), anchor=W)
Korangi.configure(width=5, relief=RAISED)
Korangi_window = w.create_window(380, 650, anchor=NW, window=Korangi)

M = Button(master, text='Malir', command= lambda: Area('Malir'), anchor=W)
M.configure(width=10, relief=RAISED)
M_window = w.create_window(400, 300, anchor=NW, window=M)











    
def value():
    global A,b,c,d,e

    pop = b
    active = int(Active.get())
    time = int(timee.get())
    Authorised = c
    socialdistance = d
    medicalservices = e
    A = COVIDSimulator(time, pop, Population[pop], Authorised, Rnot, active, socialdistance, medicalservices)

    



    

    z=[]
    for i in range(0,int(time)+1):
        z.append(i)
    A[0] = z    
    
def value_and_plot():
    value()
    plot1(A)
getValue= Button(text='Simulate', command= value_and_plot)
w.create_window(950, 675, window=getValue)

 
Rnot=2.65



def enqueue(lst, item):
    lst.append(item)

def dequeue(lst):
    return lst.pop(0)

def top(lst):
    return lst[0]

def push(lst, item):
    lst.insert(0, item)

def isempty(lst):
    if len(lst)==0: return True
    else: return False

def deaths(med, removed):
    if med == 'prepared':
        dead = int(0.02*removed)
    else:
        dead = int(0.05*removed)
    return dead

def recoveries(died, removed):
    recovered = int(removed - died)
    return recovered

def removedCalculator(infected, activeQueue):
    if len(activeQueue)>=14:
        if isempty==True:
            recovered = 0
        else:
            recovered = activeQueue[len(activeQueue)-14]
    else:
        recovered = 0
    return recovered

def COVIDSimulator(time, pop, population, areas_of_contact, Rnot, active, socialdistance, medicalservices):
    
    Rnot=int(Rnot)
    
    valsocialdistance=0
    if socialdistance=='moderate':
        valsocialdistance = 0.9
    elif socialdistance=='strict':
        valsocialdistance = 0.5
    elif socialdistance=='unimposed':
        valsocialdistance = 1.1
    #the values of val socialdistance are set in a non-linear pattern as other simulations demonstrate they are not linear.

    contact = 1


    if 'Educational_Institutes' in areas_of_contact:
        points=1+(Schools[pop]*0.005) 
        #distance in Educational_Institutes: Very close (0.05) , ventilation: poor (0.05), Duration: High (0.05)
        contact=contact*1.15*points
    
    if 'shopping_centers' in areas_of_contact:
        points=1+(malls[pop]*0.005) 
        #distance in shopping_centers: pretty close (.025) , ventilation: poor (.05), Duration: moderate (0.25)
        contact=contact*1.1*points
    
    if 'places_of_worship' in areas_of_contact:
        points=1+(mosques[pop]*0.005) 
        #distance in places_of_worship: very close (.05) , ventilation: moderate (.025), Duration: very short (-.025)
        contact=contact*1.05*points
 
    if 'parksandrecs' in areas_of_contact:
        points=1+(parksAndRec[pop]*0.005) 
        # this part of the code accounts for the amount of certain area of contact open in the region.
        contact=contact*0.975*points
        #distance in parksandrecs: sufficient (-.025) , ventilation: sufficient (-.025), Duration: moderate (.025)

    activeQueue=[active]
    recoveredQueue=[0]
    deathQueue = [0]
    removedStack = [0]
 
    for i in range(time):
        active = int((active + (Rnot * valsocialdistance * active * contact)))
        removed = int(removedCalculator(active, activeQueue))

        if removed<top(removedStack):
            removed = top(removedStack)
        else:
            push(removedStack, removed) 


        if removed>=active:
            active = 0
        elif active>=population:
            active=population-removed
        else:
            active -= removed
        
        died = deaths(medicalservices, removed)
        recovered = recoveries(died, removed)

        enqueue(activeQueue, active)
        enqueue(recoveredQueue, recovered)
        enqueue(deathQueue, died)


    print(time)
    print(activeQueue)
    print(recoveredQueue)
    print(deathQueue)

    return [time,activeQueue, recoveredQueue, deathQueue]
 
def delete():
    master.destroy()
    
    clear_graph()

def clear_graph():
    global A,b,c,d,e
    A = []
    b = ''
    c = []
    d = ''
    e = ''
    
    master = Tk()
    Frame(master)
    master.grid()
    master.geometry('1600x900')

    master.attributes("-fullscreen", True)
    master.bind("<F11>", lambda event: master.attributes("-fullscreen",not master.attributes("-fullscreen")))
    master.bind("<Escape>", lambda event: master.attributes("-fullscreen", False))

    w = Canvas(master, width=1600, height=900)
    w.grid()
    
    Full = Button(master, text = "Full screen", command = fullscreenn , anchor = W)
    Full.configure(width = 10, relief = RAISED)
    Full_window = w.create_window(1300, 600, anchor=NW, window=Full)
    
    about = Button(master, text = "About", command = About , anchor = W)
    about.configure(width = 10, relief = RAISED)
    about_window = w.create_window(1300, 400, anchor=NW, window=about)
    
    photo = Image.open('C:/users/Dell/Desktop/dsa.jpeg')
    photo = photo.resize((600, 550), Image.ANTIALIAS)
    photo = ImageTk.PhotoImage(photo)
    w.create_image(370,450, image=photo, anchor='c')

    w.create_line(50, 140, 1500, 140)
    w.create_rectangle(50, 100, 1500, 750)
    w.create_rectangle(700, 180, 1200, 720) #graph
    w.create_text(120, 120, text='COVID-SIMULATOR')
    # w.create_text(950, 350, text='BAR GRAPH')
    
    w.create_rectangle(1250, 180, 1450, 720)  # buttonns


    
    
    

    button1 = Button(master, text="Quit", command=master.quit, anchor=W)
    button1.configure(width=10, relief=RAISED)
    button1_window = w.create_window(1300, 300, anchor=NW, window=button1)


    label10 = Label(master, text= 'Please input which area you would like to simulate (select on map) ')
    w.create_window(950, 200, window=label10)

    label13 = Label(master, text= 'Please input which areas of contact will be open: ')
    w.create_window(950, 350, window=label13)

    Malls = Button(master, text='Malls', command= lambda: Place1('malls'), anchor=W)
    Malls.configure(width=10, relief=RAISED)
    Malls_window = w.create_window(750, 375, anchor=NW, window=Malls)

    Schools = Button(master, text='Schools', command= lambda : Place1('Schools'), anchor=W)
    Schools.configure(width=10, relief=RAISED)
    Schools_window = w.create_window(850, 375, anchor=NW, window=Schools)

    ParkandRec = Button(master, text='ParkandRec', command= lambda: Place1('parksAndRec'), anchor=W)
    ParkandRec.configure(width=10, relief=RAISED)
    ParkandRec_window = w.create_window(950, 375, anchor=NW, window=ParkandRec)

    Mosques = Button(master, text='Mosque', command= lambda:Place1('mosques'), anchor=W)
    Mosques.configure(width=10, relief=RAISED)
    Mosques_window = w.create_window(1050, 375, anchor=NW, window=Mosques)


    button3 = Button(master, text = "Reset", command = delete, anchor = W)
    button3.configure(width = 10, relief = RAISED)
    button3_window = w.create_window(1300, 500, anchor=NW, window=button3)

        
    Active = Entry(master) 
    w.create_window(950, 275, window=Active)
    label11 = Label(master, text= 'Please input how many current active cases there are: ')
    w.create_window(950, 250, window=label11)

    timee = Entry(master) 
    w.create_window(950, 325, window=timee)
    label12 = Label(master, text= 'Please input how long the simulation will run for (in days): ')
    w.create_window(950, 300, window=label12)


    Prepared = Button(master, text='Prepared', command= lambda:Place3('prepared'), anchor=W)
    Prepared.configure(width=10, relief=RAISED)
    Prepared_window = w.create_window(850, 575, anchor=NW, window=Prepared)

    Unprepared = Button(master, text='Unprepared', command= lambda:Place3('unprepared'), anchor=W)
    Unprepared.configure(width=10, relief=RAISED)
    Unprepared_window = w.create_window(950, 575, anchor=NW, window=Unprepared)

    label15 = Label(master, text= 'Please input the state of available medical care in this area (prepared, unprepared): ')
    w.create_window(950, 550, window=label15)
    ########### Districts


    Central = Button(master, text='Central', command= lambda: Area('Karachi Central'))
    Central.configure(width=10, relief=RAISED)
    Central_window = w.create_window(300, 600, window=Central)

    K = Button(master, text='Karachi', command= lambda : Area('Karachi'), anchor=W)
    K.configure(width=10, relief=RAISED)
    K_window = w.create_window(200, 300, anchor=NW, window=K)


    KE = Button(master, text='East', command= lambda: Area('Karachi East'), anchor=W)
    KE.configure(width=5, relief=RAISED)
    KE_window = w.create_window(350, 580, anchor=NW, window=KE)


    KW = Button(master, text='West', command= lambda : Area('Karachi West'), anchor=W)
    KW.configure(width=10, relief=RAISED)
    KW_window = w.create_window(200, 600, anchor=NW, window=KW)

    KS = Button(master, text='South', command= lambda :Area('Karachi South'), anchor=W)
    KS.configure(width=5, relief=RAISED)
    KS_window = w.create_window(300, 650, anchor=NW, window=KS)

    Korangi = Button(master, text='Korangi', command= lambda: Area('korangi'), anchor=W)
    Korangi.configure(width=5, relief=RAISED)
    Korangi_window = w.create_window(380, 650, anchor=NW, window=Korangi)

    M = Button(master, text='Malir', command= lambda: Area('Malir'), anchor=W)
    M.configure(width=10, relief=RAISED)
    M_window = w.create_window(400, 300, anchor=NW, window=M)

    getValue= Button(text='Simulate', command= value_and_plot)
    w.create_window(950, 675, window=getValue)


    Unimposed = Button(master, text='Unimposed', command= lambda:Place2('unimposed'), anchor=W)
    Unimposed.configure(width=10, relief=RAISED)
    Unimposed_window = w.create_window(800, 475, anchor=NW, window=Unimposed)

    Moderate = Button(master, text='Moderate', command= lambda:Place2('moderate'), anchor=W)
    Moderate.configure(width=10, relief=RAISED)
    Moderate_window = w.create_window(900, 475, anchor=NW, window=Moderate)

    Strict = Button(master, text='Strict', command= lambda:Place2('strict'), anchor=W)
    Strict.configure(width=10, relief=RAISED)
    Strict_window = w.create_window(1000, 475, anchor=NW, window=Strict)

    label14 = Label(master, text= 'Please select the level of social distancing')
    w.create_window(950, 450, window=label14)

    master.mainloop()

w.create_rectangle(700, 180, 1200, 720) #graph

###############  INPUT Values

 ## Input value

button3 = Button(master, text="Reset", command=delete, anchor=W)
button3.configure(width=10, relief=RAISED)
button3_window = w.create_window(1300, 500, anchor=NW, window=button3)



mainloop()
