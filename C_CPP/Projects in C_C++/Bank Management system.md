# Bank Management System

```CPP
//Bank Project
#include<iostream>
#include<conio.h>
#include<string.h>
#include<stdlib.h>
#include<iomanip>

#define size 3
using namespace std;
class bank
{
private:
   int ano;
   char name[20];
   float bal;
public:
     bank();//default cons
     ~bank();//destructor
     void deposit();
     void withdraw();
     void cal_interest();
     void line1();
     void show();
     void disp_all();
     void heading();
     void get();
     void disp_by_ano();
     void disp_by_name();
     int check_ano(int);
     int check_amt(float);
     void bank_bal();
     void menu();
 };
    bank b[size]; //global objects array type

       bank::bank()
       {
	 ano=0;
	 name[0]='\0';
	 bal=0;
       }
       bank::~bank()
       {
	 cout<<"Mr./Ms. "<<name<<" your account is closed"<<endl;
	 cout<<"Please collect your bal "<<bal<<" from counter"<<endl;
	 cout<<ano<<" "<<name<<" "<<bal<<endl;
       }
       void bank::line1()
       {
       int i;
       for(i=2;i<=75;i++)
       {
       cout<<"-";
       }
       cout<<endl;
       }

void  bank ::menu()
{
cout<<"Main menu "<<endl;
cout<<"1. To display all the details"<<endl;
cout<<"2. To deposit amount"<<endl;
cout<<"3. Withdrawl of amount "<<endl;
cout<<"4. To display the details by account number"<<endl;
cout<<"5. To display details by name "<<endl;
cout<<"6. Interest calculation "<<endl;
cout<<"7. To view balance of bank"<<endl;
cout<<"8. Exit"<<endl;
cout<<"Enter your choice ";
}
 void bank::heading()
 {
 //textcolor(YELLOW);
 system("color 04");
 
 cout<<"              B A N K   R E P O R T";
 cout<<endl;
 cout<<"              ======================";
 cout<<endl;
 line1();
 //system("color 07");

 cout<<setw(10)<<"  Acc No "<<setw(30)<<"     Name    "
 <<setw(10)<<"   Bal"<<endl;
line1();
 }
 void bank::show()
 {
 cout<<setw(10)<<ano<<setw(30)<<name<<setw(10)<<bal<<endl;
 }
 int bank::check_ano(int n)
 {
 if (n<=0)
 return(0);
 else
 return(1);
 }
int bank::check_amt(float n)
{
if (n<=0)
return(0);
else
return(1);
}
 void bank::get()
 {
 int z=0;
 while(1)//for(;;)
 {
 cout<<"Enter the account number ";
 cin>>ano;
 z=check_ano(ano);
 if (z==1)
 break;
 else
 cout<<"Accno cannot be zero or -ve,try again"<<endl;
 }

 cout<<"Enter the account name";
 cin>>name;
 strupr(name);

 while(1)
 {
 cout<<"Enter the balance amount";
 cin>>bal;
 z=check_amt(bal);
 if (z==1)
 break;
 else
 cout<<"Invalid balance"<<endl;
 }

}
 void bank::disp_all()
 {
 int i;
 heading();
 for(i=0;i<size;i++)
 {
 b[i].show();
 }
 line1();
 }

void bank:: deposit()
   {
   int tn,z=0,i,z1;
    float ma;
    cout<<"Enter the account number ";
    cin>>tn;
    for(i=0;i<size;i++)
    {
    if (b[i].ano==tn)
    {
    z=1;
    while(1)
    {
    cout<<"Enter the amount to deposit";
    cin>>ma;
    z1=check_amt(ma);
    if (z1==1)
    break;
    else
    cout<<"Invalid amount"<<endl;
    }
    b[i].bal=b[i].bal+ma;
    }
    }
    if (z==0)
    cout<<"Invalid account number,Record is not present"<<endl;
    }
  void bank::withdraw()
  {
  int i,z=0,tn,z1;
  float m2;
  cout<<"Enter the account number ";
  cin>>tn;
  for(i=0;i<size;i++)
  {
  if (tn==b[i].ano)
  {
  z=1;
   while(1)
   {
   cout<<"Enter the amount to widthdraw ";
   cin>>m2;
   z1=check_amt(m2);
   if (z1==1)
   break;
   else
   cout<<"Invalid amount"<<endl;
   }

   if ((b[i].bal-m2)>=500)
   b[i].bal=b[i].bal-m2;
   else
   cout<<"Amount cannot be widthdrawn";
   }
   }
   if (z==0)
   cout<<"Invalid account number , record is not present"<<endl;
   }
void bank::disp_by_ano()
{
 int i,tn,z=0;
 cout<<"Enter the account number ";
 cin>>tn;
 for(i=0;i<size;i++)
 {
 if (b[i].ano==tn)
 {
 z=1;
 heading();
 b[i].show();
 }
 }
 line1();
 if (z==0)
 cout<<"Record not present"<<endl;
 }
 void bank::disp_by_name()
 {
 int i,z=0;
 char tn[20];
 cout<<"Enter the name ";
 cin>>tn;
 strupr(tn);
 for(i=0;i<size;i++)
 {
 if (strcmpi(b[i].name,tn)==0)
 {
 z=1;
 heading();
 b[i].show();
 }
 }
 line1();
 if ( z==0)
 cout<<"Record is not present"<<endl;
 }
void bank:: cal_interest()
{
int i;
for(i=0;i<size;i++)
{
 b[i].bal=b[i].bal+b[i].bal*.05;
 }
 }
  void bank::bank_bal()
 {
 int i;
 float tot=0;
 heading();
 for(i=0;i<size;i++)
 {
 b[i].show();
 tot=tot+b[i].bal;

 }
  line1();
  cout<<"\n\n\nGrand total ="<<tot<<endl;
 }

 int main()
{
  bank b1;
  int op,i;
	system("cls");
  for(i=0;i<size;i++)
  {
    b[i].get();
  }
  while(op!=8)
  {
  	system("cls");
  	system("color 07");
    b1.menu();
    cin>>op;
	system("cls");
    switch(op)
    {
	case 1:
		b1.disp_all();
		break;
	case 2:
		b1.deposit();
		break;
	case 3:
		b1.withdraw();
		break;
	case 4:
		b1.disp_by_ano();
		break;
	case 5:
		b1.disp_by_name();
		break;
	case 6:
		b1.cal_interest();
		break;
	case 7:
		b1.bank_bal();
		break;
	case 8:
		cout<<"End of the program"<<endl;
		break;
	default:
		cout<<"Invalid choice";
		break;
    }//switch
  getch();
  }//while
  return(0);
}//main
```

## OUTPUT-1

```CPP
Enter the account number 78923
Enter the account name Akrati
Enter the balance amount 78942
Enter the account number 23763
Enter the account name Amit
Enter the balance amount 85643
Enter the account number 66434
Enter the account name Aashi
Enter the balance amount 45678

```

## OUTPUT-2

```CPP
Main menu 
1. To display all the details
2. To deposit amount
3. Withdrawl of amount 
4. To display the details by account number
5. To display details by name 
6. Interest calculation 
7. To view balance of bank
8. Exit
Enter your choice 1
```

## OUTPUT-3

```CPP
              B A N K   R E P O R T 
              ======================
--------------------------------------------------------------------------
   Acc No                       Name           Bal
--------------------------------------------------------------------------
     78923                        AKRATI     78942
     23763                          AMIT     85643
     66434                         AASHI     45678
--------------------------------------------------------------------------

```
