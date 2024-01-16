# Ip
import mysql.connector as a

passwd=str(input("DATABASE PASSWORD:"))

con=a.connect(host="localhost",user="root",passwd="joyeeta6/q",database='gshop')

c=con.cursor()

c.execute("show databases")

dl=c.fetchall()

dl2=[]

for i in dl:

    dl2.append(i[0])

if'gshop'in dl2:

    sql="use gshop"

    c.execute(sql)

else:

    sql1="create database gshop"

    c.execute(sql1)

    sql2="use gshop"

    c.execute(sql2)

    sql3="""create table Gifts(Name varchar(50),Cost integer,Buy integer,Data varchar(20))"""

    c.execute(sql3)

    sql4="""create table Customer(Name varchar(20),Gift varchar(25),Payment integer,Date varchar(20),Phone varchar(20))"""

    c.execute(sql4)

    sql5="""create table Bills(Detail varchar(20),Cost integer,Date varchar(20))"""

    c.execute(sql5)

    sql6="""create table Worker(Name varchar(100),Work varchar(20),Salary varchar(20))"""

    c.execute(sql6)

    con.commit()

def signin():

    print("\n")

    print(" ---------->>>>>>>>>>Welcome,DELHI GIFT SHOP[DGS]<<<<<<<<<<----------")

    print("\n")

    p=input("System Password:")

    if p=="dgs111":

        options()

    else:

        signin()

def options():

    print("""        1.Add Gifts

                     2.Sell Gifts

                     3.Add Bill

                     4.Add Worker

                     5.Display Gifts

                     6.Display Payments

                     7.Display Bills

                     8.Display Worker

    """)

    choice=input("Select Option:")

    while True:

        if(choice=='1'):

            AddGifts()

        elif(choice=='2'):

            SellGifts()

        elif(choice=='3'):

            AddBill()

        elif(choice=='4'):

            AddWorker()

        elif(choice=='5'):

            dGifts()

        elif(choice=='6'):

            dPayments()

        elif(choice=='7'):

            dBills()

        elif(choice=='8'):

            dWorker()

        else:

            print("Enter Again..........")

            options()

def AddGifts():

    n=input("Name:")

    c=input("Cost:")

    b=input("Buy:1")

    d=input("Date:")

    data=(n,c,b,d)

    sql='insert into Gifts values(%s,%s,%s,%s)'

    c=con.cursor()

    c.execute(sql,data)

    con.commit()

    print("Data Inserted Successfully")

    options()

def SellGifts():

    n=input("Name:")

    g=input("Gift:")

    py=input("Payment:")

    d=input("Date:")

    p=input("Phone:")

    data=(n,g,py,d,p)

    sql='insert into Customer values(%s,%s,%s,%s,%s,%s)'

    c=con.cursor()

    c.execute(sql,data)

    con.commit()

    print("Data Inserted Successfully")

    options()

def AddBill():

    dt=input("Detail:")

    c=input("Cost:")

    d=input("Date:")

    data=(dt,c,d)

    sql='insert into Bill values(%s,%s,%s)'

    c=con.cursor()

    c.execute(sql,data)

    con.commit()

    print("Data Inserted Successfully")

    options()

def AddWorker():

    n=input("Name:")

    w=input("Work:")

    s=input("Salary:")

    data=(n,w,s)

    sql='insert into Worker values(%s,%s,%s)'

    c=con.cursor()

    c.execute(sql,data)

    con.commit()

    print("Data Inserted Successfully")

    options()

def dGifts():

    sd=input("Date:")

    sql='select*from Gifts'

    c=con.cursor()

    c.execute(sql)

    d=c.fetchall()

    for i in d:

        if i[3]==sd:

            print("Name:",i[0],"Cost:",i[1],"Buy:",i[2],"Date:",i[3])

            print("................................................")

        options()

def dPayment():

        sd=input("Date:")

        sql='select*from Customer'

        c=con.cursor()

        c.execute(sql)

        d=c.fetchall()

        for i in d:

            print("Name:",i[0],"Gift:",i[1],"Payment:",i[2],"Date:",i[3],"Phone:",i[4])

            print("..................................................")

            options()

def dBills():

     sd=input("Date:")

     sql='select*from Bills'

     c=con.cursor()

     c.execute(sql)

     d=c.fetchall()

     for i in d:

            if i[3]==sd:

                print("Detail:",i[0],"Cost:",i[1],"Date:",i[2])

                print("..................................................")

            options()

def dWorker():

    sql='select*from Worker'

    c=con.cursor()

    c.execute(sql)

    d=c.fetchall()

    for i in d:

        print("Name:",i[0],"Work:",i[1],"Salary:",i[2])

      print("..........................................................")

    options()

signin()


