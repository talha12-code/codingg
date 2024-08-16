# codingg
new
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class Student {
private:
    string name;
    int roll_number;
    float marks;

public:
    Student() : name(""), roll_number(0), marks(0.0) {}
    void input() {
        cout << "Enter name: ";
        getline(cin, name);
        cout << "Enter roll number: ";
        cin >> roll_number;
        cout << "Enter marks: ";
        cin >> marks;
        cin.ignore();
    }
    void display() {
        cout << "Name: " << name << endl;
        cout << "Roll Number: " << roll_number << endl;
        cout << "Marks: " << marks << endl;
    }
    void writeToFile(ofstream& file) {
        file << name << endl;
        file << roll_number << endl;
        file << marks << endl;
    }
    void readFromFile(ifstream& file) {
        getline(file, name);
        file >> roll_number;
        file >> marks;
        file.ignore(); 
    }
    void modifyMarks(float newMarks) {
        marks = newMarks;
    }
};

int main() {
    ofstream outputFile("students.txt");
    Student students[5];
    for (int i = 0; i < 5; i++) {
        students[i].input();
        students[i].writeToFile(outputFile);
    }
    outputFile.close();
    ifstream inputFile("students.txt");
    for (int i = 0; i < 5; i++) {
        students[i].readFromFile(inputFile);
        students[i].display();
        cout << endl;
    }
    inputFile.close();
    fstream file("students.txt", ios::in | ios::out);
    Student temp;
    file.seekg(2 * sizeof(string) + sizeof(int)); 
    file >> temp.marks;
    temp.modifyMarks(90.0);
    file.seekp(2 * sizeof(string) + sizeof(int)); 
    file << temp.marks;
    file.close();
    inputFile.open("students.txt");
    for (int i = 0; i < 5; i++) {
        students[i].readFromFile(inputFile);
        students[i].display();
        cout << endl;
    }
    inputFile.close();

    return 0;
}
