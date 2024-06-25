# managment-system
import pandas as pd
import matplotlib.pyplot as plt
import mysql.connector as sqltor
import csv
import numpy as np
con=sqltor.connect(host='localhost',user='root',passwd='mokshda2004',database='project')
pd.set_option('display.max_rows',500)
pd.set_option('display.max_columns',500)
pd.set_option('display.width',500)
print("****************************************************************************")
print("*                                                                                                               *")
print("*                          WELCOME TO MED-MANAGE                                                                *")
print("*                                                                                                               *")
print("****************************************************************************")
print()
v=1
while (v==1):
    print('YOU ARE -')
    print()
    print('1.ADMIN\n2.USER\n3.EXIT')
    print()
    choice=int(input('ENTER YOUR CHOICE:'))
    print()
                #ADMIN
    if (choice==1):
        print("*****************************************\n*         WELCOME TO ADMIN MODE     *\n*****************************************")
        print()
        print('YOU WANT TO -')
        print('1.SIGN UP\n2.SIGN IN\n3.BACK')
        print()
        choice1=int(input('ENTER A CHOICE:'))
        print()
        if (choice1==1):
            name=input('ENTER YOUR NAME:')
            password=input('ENTER YOUR PASSWORD:')
            df=pd.read_csv('admin.csv')
            data={'name':[name], 'password':[password]}
            df1=pd.DataFrame(data)
            df=df.append(df1)
            df.to_csv('admin.csv', index=False)
            print('YOU HAVE REGISTERED SUCCESSFULLY')
            print()
            v=1
        if (choice1==2):
                name=input('ENTER YOUR NAME:')
                password=input('ENTER YUR PASSWORD:')
                df=pd.read_csv('admin.csv', sep=',')
                df1=df[(df['name']==name) & (df['password']==password)]
                a=1
                print()
                print(':::::WELCOME', name, ':::::')
                print()
                while (a==1):
                    print('1. ADMISSION DETAILS')
                    print('2. STAFF DETAILS')
                    print('3. VIEW APPOINTMENT HISTORY')
                    print('4. WARD DETAILS')
                    print('5. AMBULANCE SERVICE')
                    print('6. CONSULTATION')
                    print('7. DASHBOARD')
                    print('8. BACK')
                    print()
                    c=int(input('CHOOSE ANY OPERATION:'))
                                    #ADMIN(ADMISSION DETAILS)
                    if c==1:
                        print('1. IMPATIENT')
                        print('2. OUTATIENT')
                        print()
                        b=int(input('CHOOSE 1 OR 2:'))
                        if b==1:
                            df3=pd.read_sql('select * from inpatient',con)
                            print()
                            print (df3)
                            print()
                            a=1
                        else:
                            df4=pd.read_sql('select * from outpatient',con)
                            print()
                            print (df4)
                            print()
                            a=1
                                        #ADMIN(STAFF DETAILS)
                    elif c==2:
                        df5=pd.read_sql('select name,department,mob,email,qualification,salary from staff',con)
                        print()
                        print(df5)
                        print()
                        a=1
                                        #ADMIN(VIEW APPOINTMENT HISTORY)
                    elif c==3:
                        s=int(input('ENTER STAFF ID:'))
                        df6=pd.read_csv('appointment.csv')
                        df7=df6[df6['doc"s id']==s]
                        print()
                        print (df7)
                        print()
                        a=1
                                        #ADMIN(WARD DETAILS)
                    elif c==4:
                        df7=pd.read_sql('select * from ward',con)
                        print()
                        print (df7)
                        print()
                        a=1
    
                                        #ADMIN(AMBULANCE SERVICES)
                    elif c==5:
                        df8=pd.read_sql('select * from ambulance',con)
                        print()
                        print (df8)
                        print()
                        a=1
                                        #ADMIN(CONSULTATIONS)
                    elif c==6:
                        print('1. IMPATIENT')
                        print('2. OUTATIENT')
                        print()
                        q=int(input('CHOOSE 1 OR 2:'))
                        print()
                        if(q==1):
                            pi=input('ENTER PATIENT ID:')
                            print()
                            conn=sqltor.connect(host='localhost',user='root',passwd='mokshda2004',database='project')
                            df8=pd.read_sql('select * from inpatient where pid="{}" '.format(pi),conn)
                            print()
                            print(df8)
                            a=1
                        elif(q==2):
                            pi=input('ENTER PATIENT ID:')
                            conn=sqltor.connect(host='localhost',user='root',passwd='mokshda2004',database='project')
                            df8=pd.read_sql('select * from outpatient where pid="{}" '.format(pi),conn)
                            print()
                            print (df8)
                            print()
                            a=1
                        else:
                            print('CHOOSE VALID OPERATION!!')
                            a=1                           
                                        #ADMIN(DASHBOARD) 
                    elif c==7:
                        print()
                        print('1. UPDATE/CHANGE USERNAME')
                        print('2. UPDATE/CHANGE PASSWORD')
                        print()
                        d=int(input('CHOOSE 1 OR 2:'))
                        print()
                        if d==1:
                             cn=input('ENTER CURRENT USERNAME:')
                             nc=input('ENTER NEW USERNAME:')
                             ps=input ('ENTER PASSWORD:')
                             x=(df[df['name']==cn].index.values)
                             df.loc[x,['name']]=[nc]
                             df.to_csv('admin.csv',index=False)
                             print('::::USERNAME FINALLY UPDATED::::')
                             print()
                             a=1
                        if d==2:
                             cn=input('ENTER  USERNAME:')
                             nc=input('ENTER CURRENT PASSWORD:')
                             ps=input ('ENTER NEW PASSWORD:')
                             x=(df[df['password']==nc].index.values)
                             df.loc[x,['password']]=[ps]
                             df.to_csv('admin.csv',index=False)
                             print('::::PASSWORD FINALLY UPDATED::::')
                             print()
                             a=1
                                            #BACK BUTTON
                    elif c==8:
                        break
                        print()
                    else:
                        print('~~~~~INVALID SELECTION~~~~~\nPLEASE ENTER VALID CHOICE')
                        print()
                        a=1
    elif (choice==2):
        m=1
        while (m==1):
            print()
            print("*****************************************\n*         WELCOME TO USER MODE          *\n*****************************************")
            print()
            print('YOU WANT TO -')
            print('1.SIGN UP\n2.SIGN IN\n3.BACK')
            print()
            choice1=int(input('ENTER YOUR CHOICE:'))
            print()
            if (choice1==1):
                name=input('ENTER YOUR NAME:')
                password=input('ENTER YOUR PASSWORD:')
                df=pd.read_csv('admin.csv')
                data={'name':[name], 'password':[password]}
                df1=pd.DataFrame(data)
                df=df.append(df1)
                df.to_csv('admin.csv', index=False)
                print('YOU HAVE REGISTERED SUCCESSFULLY')
                print()
                m=1
            if (choice1==2):
                    name=input('ENTER YOUR NAME:')
                    password=input('ENTER YUR PASSWORD:')
                    df=pd.read_csv('admin.csv', sep=',')
                    df1=df[(df['name']==name) & (df['password']==password)]
                    x=1
                    print()
                    print(':::::WELCOME', name, ':::::')
                    print()
                    while (x==1):
                        print()
                        print('1. PATIENT')
                        print('2. RECEPTIONIST')
                        print('3. DOCTOR')
                        print('4. NURSE')
                        print('5. PHARMACIST')
                        print('6. LABORATORIST')
                        print('7. ACCOUNTANT')
                        print('8. BACK')
                        print()
                        u=int(input('CHOOSE ANY OPERATION:'))
                        if (u==1):
                            import patient.py
                        if (u==2):
                            import receptionist.py
                        if (u==3):
                            import doctor.py
                        if (u==4):
                            import nurse.py
                        if (u==5):
                            import pharmist.py
                        if (u==6):
                            import laboratorist.py
                        if (u==7):
                            import accountant.py
                        if (u==8):
                            break
                            print()
    elif (choice==3):
        print ('~~~~~~~~THANKS FOR VISITING~~~~~~~~')
        break
    else:
        print('~~~~~~INVALID SELECTION~~~~~~~\n PLEASE TRY AGAIN:')
        print()
        m=1

        
