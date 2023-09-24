//Task-4(To-do-list)

#include<iostream>
#include<string>
#include<fstream>
using namespace std;
void enterdata();
void viewdata();
void deletedata();
void updatedata();
struct todo{
    int n;
    string str;
};
int N;
main()
{
    system("cls");
    while(true)
    {
    int ch;
    cout<<"enter 1 to add task in file"<<endl; 
    cout<<"enter 2 to delete task from file"<<endl;
    cout<<"enter 3 to view task from file"<<endl;
    cout<<"enter 4 to mark task as completed"<<endl;
    cout<<"enter you choice : ";
    cin>>ch;
    if(ch==1){
        getdata();
    }
    else if(ch==2){
        deletedata();
    }
    else if(ch==3){
        showdata();
    }
    else if(ch==4){
        update();
    }
   
   }
}
 void enterdata()
 {
    system("cls");
    todo to;
    cout<<"enter new task :"<<endl;
    cin.get();
    getline(cin,to.str);
    N++;
    ofstream out;
    out.open("ToDo.txt",ios::app);
    out<<"\n"<<N;
    out<<"\n"<<to.str;
    char c;
    cout<<"you want to add more task?"<<endl;
    cout<<"press y for yes and n for no ";
    cin>>c;
    if(c=='y'){
        getdata();
    }
    else{
    system("cls");
    cout<<"Task added successfully!!"<<endl;
    }
    out.close();
    system("cls");
 }
  
void viewdata()
{
system("cls");
todo to;
ifstream in;
in.open("ToDo.txt",ios::in);
cout<<"All tasks are :"<<endl;
while(!in.eof())
{
in>>to.n;
in.ignore();
getline(in,to.str);
if(to.str != ""){
cout<<"\t"<<to.n<<"- "<<to.str<<endl;
}
else{
    cout<<"File is empty!!!"<<endl;
}
}
in.close();
}

void deletedata()
{
    system("cls");
    todo to;
    int id;
    cout<<"enter task id to delete task"<<endl;
    cin>>id; 
    if(id!=0){ 
    char del;
    cout<<"Delete the task?"<<endl;
    cout<<"enter y for yes and n for no ";
    cin>>del;
    if(del=='y'){
    ofstream tfile;
    tfile.open("File.txt");
    ifstream in;
    in.open("ToDo.txt");
    int index=1;
    while(!in.eof()){
        in>>to.n;
        in.ignore();
        getline(in,to.str);
        if(to.n!=id){
            tfile<<"\n"<<index;
            tfile<<"\n"<<to.str;
            index++;
            N--;
        }
    }
    system("cls");
    in.close();
    tfile.close();
    remove("ToDo.txt");
    rename("File.txt","ToDo.txt"); 
    cout<<"Task deleted successfully!!!"<<endl;
    }
   else{
    cout<<"Task not deleted"<<endl; 
   }
}
}
void updatedata()
{
    system("cls");
    todo to;
    char ans;
    cout<<"do you want to mark task as completed?"<<endl;
    cout<<"press y for yes and n for no ";
    cin>>ans;
    if(ans=='y'){
    int id;
    cout<<"enter task id to mark as complete"<<endl;
    cin>>id;
    ofstream tfile;
    tfile.open("File.txt");
    ifstream in;
    in.open("ToDo.txt");
    int index=1;
    while(!in.eof()){
        in>>to.n;
        in.ignore();
        getline(in,to.str);
        if(to.n!=id){
            tfile<<index<<" "<<to.str<<endl;
            index++;
            N--;
        }
        else if(to.n==id){
            tfile<<index<<" "<<to.str<<"**"<<endl;
            index++;
            N--;
        }
    }
    system("cls");
    in.close();
    tfile.close();
    remove("ToDo.txt");
    rename("File.txt","ToDo.txt"); 
    cout<<"Task marked successfully!!!"<<endl;
    }
    else{
        cout<<"task not found!"<<endl;
    }
}

