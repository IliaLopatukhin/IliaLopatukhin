#include "iostream"
#include "fstream"
#include "string"
#include "vector"

using namespace std;

struct employee
{
    string FIO;
    string date;
    string post;
    string salary;
};

int main()
{
    int n;
    cout << "enter n:";
    cin >> n;
    vector <employee> employees;
    for (int i = 0; i < n; i++)
    {
        employee EE;
        cout << "enter FIO_" << i <<":"; cin >> EE.FIO;
        cout << "enter date_" << i <<":"; cin >> EE.date;
        cout << "enter post_" << i <<":"; cin >> EE.post;
        cout << "enter salary_" << i <<":"; cin >> EE.salary;
        employees.push_back(EE);
    }

    ofstream f("file.txt");
    for (int i = 0; i < n; i++)
    {
        f << i << '\n';
        f << employees[i].FIO << '\n';
        f << employees[i].date << '\n';
        f << employees[i].post << '\n';
        f << employees[i].salary << '\n';
    }
    f.close();

    ofstream fout;
    fout.open("fileBIN.txt");
    for (int i = 0; i < n; i++)
    {
        fout.write((char*)&employees[i].FIO, sizeof(string));
    }
    fout.close();

    cout << endl << "text" << endl;

    ifstream fin("file.txt");
    string line;
    while (getline(fin, line))
    {
        cout << line << endl;
    }
    fin.close();

    cout << endl << "binary" << endl;

    ifstream fin1("fileBIN.txt");
    string line1;
    while (getline(fin1, line1))
    {
        cout << line1 << endl;
    }
    fin1.close();
}
