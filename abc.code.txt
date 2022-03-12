#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <sstream>

using namespace std;
string fname, word, line; // 3 variables to store file name, each word and each line
int reg, bill, days;
string name, sto;
char status;
void sorting();
void reg1()
{
    //TO ENTER DATA TO REGISTER A NEW STUDENT.
    cout << "Enter reg no :: ";
    cin >> reg;
    cout << "Enter days :: ";
    cin >> days;
    cout << "Enter name :: ";
    cin >> name;
    cout << "Do you want set the mess "
         << " [in] "
         << " by default ( y / n ) :: ";
    cin >> status;
    switch (status)
    {
    case 'y':
    {
        sto = "in";
        break;
    }
    default:
    {
        sto = "out";
    }
    }
}
void regi()
{
    fstream file;
    vector<vector<string>> all_data;
    vector<string> row_data;
    file.open("data.csv", ios::in);
    if (!file.is_open())
    {
        cout << "Error";
    }
    else
    {
        //cout << "open";
        //row_data.clear();
        //stringstream str(line);
        while (getline(file, line))
        {
            row_data.clear(); //all data in the row
            stringstream str(line);
            while (getline(str, word, ','))
            {
                row_data.push_back(word);
            }
            all_data.push_back(row_data);
        }
        file.close();
        reg1();

        bool f = true;
        for (int i = 0; i < all_data.size(); i++)
        {
            if (all_data[i][0] == to_string(reg))
            {
                cout << "reg already exist";
                f = false;
                break;
            }
            else
            {
                f = true;
                continue;
            }
        }
        if (f)
        {
            file.open("data.csv", ios::app); //APPEND READS AND  ADD DATA
            file << reg << "," << name << "," << sto << "," << days << "," << days * 300 << "," << endl;
            file.close();
            sorting();
        }
    }
}
void inout()
{
    //TO CHECK TOTAL NUMBER OF IN AND OUT
    fstream file;
    file.open("data.csv", ios::in);
    int b = 0;
    int c = 0;
    if (!file.is_open())
    {
        cout << "Error";
    }
    else
    {
        while (file.good())
        {
            string status;
            getline(file, status, ',');
            if (status == "out")
            {
                b++;
            }
            if (status == "in")
            {
                c++;
            }
        }
        cout << "******" << endl;
        cout << "in = " << c << endl;
        cout << "out = " << b << endl;
        cout << "******";
        cout << endl;
        file.close();
    }
}
void deleteing()
{
    string reg;
    vector<vector<string>> all_data;
    vector<string> row_data;
    fstream file;
    file.open("data.csv", ios::in);
    if (!file.is_open())
    {
        cout << "Error";
    }
    else
    {
        while (getline(file, line))
        {
            row_data.clear(); //all data in the row
            stringstream str(line);
            while (getline(str, word, ','))
            {
                row_data.push_back(word);
            }
            all_data.push_back(row_data);
        }
        file.close();
        cout << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Enter Reg No of student to be Deleted :: ";
        cin >> reg;

        for (int i = 0; i < all_data.size() - 1; i++)
        {
            int j = 0;
            if (reg == all_data[i][j])
            {
                all_data.erase(all_data.begin() + i);
            }
        }
        file.open("data.csv", ios::out);
        if (!file.is_open())
        {
            cout << "error";
        }
        else
        {
            for (int x = 0; x < all_data.size() - 1; x++)
            {
                for (int y = 0; y < 5; y++)
                {
                    file << all_data[x][y] << ",";
                }
                file << endl;
            }
            file.close();
        }
        cout << "The record is deleted is Sucessfully" << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
    }
}
void searching()
{
    string reg;
    vector<vector<string>> all_data;
    vector<string> row_data;
    fstream file;
    file.open("data.csv", ios::in);
    if (!file.is_open())
    {
        cout << "Error";
    }
    else
    {
        char ent;
        while (getline(file, line))
        {
            row_data.clear(); //all data in the row
            stringstream str(line);
            while (getline(str, word, ','))
            {
                row_data.push_back(word);
            }
            all_data.push_back(row_data);
        }
        file.close();
        cout << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Enter Student Registration No to Search record :: ";
        cin >> reg;
        cout << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Reg_No   Name   Status Days  Bill" << endl;
        bool ch = false;
        for (int i = 0; i < all_data.size(); i++)
        {
            int j = 0;
            if (reg == all_data[i][j])
            {
                ch = true;
                for (int k = 0; k < 5; k++)
                {
                    cout << all_data[i][k] << "   ";
                }
                cout << endl;
                break;
            }
        }
        cout << "______________________________________________________________________________________________________________" << endl;
        if (ch == false)
        {
            cout << "Record not found";
            cout << " Do you want to Register a new student (y/n) :: ";
            cin >> ent;
            cout << "______________________________________________________________________________________________________________" << endl;
            switch (ent)
            {
            case 'y':
                regi();
                break;
            case 'n':
                break;
            }
        }
        cout << endl;
    }
}
void changemess()
{
    string reg;
    vector<vector<string>> all_data;
    vector<string> row_data;
    fstream file;
    file.open("data.csv", ios::in);
    if (!file.is_open())
    {
        cout << "Error";
    }
    else
    {
        int num1;
        int num2;
        while (getline(file, line))
        {
            row_data.clear(); //all data in the row
            stringstream str(line);
            while (getline(str, word, ','))
            {
                row_data.push_back(word);
            }
            all_data.push_back(row_data);
        }
        file.close();
        cout << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Enter Reg No of student to change student student mess status :: ";
        cin >> reg;
        for (int i = 0; i < all_data.size(); i++)
        {
            int j = 0;
            if (reg == all_data[i][j])
            {
                string k;
                k = all_data[i][2];
                //cout << k;//mess status out or in currently will show.
                if (k == "out")
                {
                    all_data[i][2] = "in";
                    num1 = stoi(all_data[i][3]);
                    num1 = num1 + 1;
                    stringstream number;
                    number << num1;
                    all_data[i][3] = number.str();
                    num2 = stoi(all_data[i][4]);
                    num2 = num2 + 300;
                    stringstream number1;
                    number1 << num2;
                    all_data[i][4] = number1.str();
                }
                else if (k == "in")
                {
                    all_data[i][2] = "out";
                }
            }
        }
        file.open("data.csv", ios::out);
        for (int x = 0; x < all_data.size(); x++)
        {
            for (int z = 0; z < 5; z++)
            {
                file << all_data[x][z] << ",";
            }
            file << endl;
        }
        cout << "Mess status Has Been Changed Sucessfully" << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << endl;
        file.close();
    }
}
int main()
{
    int option;
    do
    {
        cout << "                                   ____________________________________" << endl;
        cout << "                                   ________Mess Management System______" << endl;
        cout << "                                   ____________________________________";
        cout << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Press"
             << " 1 "
             << "to Register a new student :: " << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "press"
             << " 2 "
             << "to check total number of  in and out :: " << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Press"
             << " 3 "
             << "to delete any student's record :: " << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Press"
             << " 4 "
             << "to search any student's record :: " << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cout << "Press"
             << " 5 "
             << "to change mess status :: " << endl;
        cout << "______________________________________________________________________________________________________________" << endl;
        cin >> option;
        switch (option)
        {
        case 1:
            regi();
            break;
        case 2:
            inout();
            break;
        case 3:
            deleteing();
            break;
        case 4:
            searching();
            break;
        case 5:
            changemess();
            break;
        }
    } while (option < 6);
    //loop will only run to 5 value
    cout << "You Have Exited";
    return 0;
}
void sorting()
{
    vector<vector<string>> all_data;
    vector<string> row_data;
    fstream file;
    file.open("data.csv", ios::in);
    if (!file.is_open())
    {
        cout << "Error";
    }
    else
    {
        while (getline(file, line))
        {
            row_data.clear(); //all data in the row
            stringstream str(line);
            while (getline(str, word, ','))
            {
                row_data.push_back(word);
            }
            all_data.push_back(row_data);
        }
    }
    file.close();
    //cout << all_data.size();
    // check the first column and compare the data
    // outler most loop controls number of swaps
    //bubble sort
    for (int i = all_data.size(); i > 0; i--)
    {

        for (int j = 1; j < i - 1; j++)
        {
            if (all_data[j][0] > all_data[j + 1][0])
            {
                swap(all_data[j], all_data[j + 1]);
            }
        }
    }
    file.open("data.csv", ios::out);
    if (!file.is_open())
    {
        cout << "error";
    }
    else
    {
        for (int u = 0; u < all_data.size(); u++)
        {
            for (int v = 0; v < 5; v++)
            {
                file << all_data[u][v] << ",";
            }
            file << endl;
        }
    }
    file.close();
}