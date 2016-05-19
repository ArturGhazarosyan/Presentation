# Presentation

#include <string>
#include <iostream>
using namespace std;

const int size = 10000;  //max size pharmacy

class medicine{
    string name_;
    double price_;
    int count_;
public:
    medicine(){}
    medicine(string name, double price, int count = 0) : name_(name), price_(price), count_(count){}
    string getName(){ return name_; }
    double getPrice(){ return price_; }
    void setPrice(double price) { price_ = price; }
    int getCount(){ return count_; }
    void addmediceine(int c){ count_ += c; }
    void sealemediceine(int c){ count_ += c; }
};

class pharmacy{
    medicine medicines_[size];
    string address_;
    int qty;
public:
    pharmacy(string address) : address_(address){ qty = 0; }
    void addNewMedicine(string name, double price, int count){
        if (qty == size){
            cout << "Pharmacy is full\n";
            return;
        }
        medicine current = medicine(name, price, count);
        medicines_[qty++] = current;
    }
    
    bool findMedicine(string name){
        for (int i = 0; i < qty; i++){
            if (medicines_[i].getName() == name){
                cout << "In Pharmacy has " << name << " medicinde\n";
                cout << "Price: " << medicines_[i].getPrice() << endl;
                cout << "Coutn: " << medicines_[i].getCount() << endl;
                return true;
            }
        }
        cout << "In Pharmacy has not " << name << " medicine\n";
        return false;
    }
    
    void addMedicine(string name, int count){
        for (int i = 0; i < qty; i++){
            if (medicines_[i].getName() == name){
                medicines_[i].addmediceine(count);
                return;
            }
        }
    }
    
    void sealeMedicine(string name, int count){
        for (int i = 0; i < qty; i++){
            if (medicines_[i].getName() == name){
                if (medicines_[i].getCount() >= count){
                    medicines_[i].sealemediceine(count);
                    cout << "Your totale price is: " << count*medicines_[i].getPrice() << endl;
                    return;
                }
            }
        }
        cout << "In Pharmacy has not " << name << " medicine\n";
    }
};

int main(){
    pharmacy mypharmacy = pharmacy("M. Mashtoc 58");
    bool start = true;
    cout<<"Hello, this is the best pharmacy in Yerevan, thank you for visiting us\n\n";
    while (start){
        cout << "If you want to add a new medicine type 0\n";
        cout << "If you want to sell medicine type 1\n";
        cout << "If you want to find medicine in pharmacy type 2\n";
        cout << "If you want to update medicine qount type 3\n";
        cout << "For closing the program type -1\n";
        int answer;
        cin >> answer;
        switch (answer)
        {
            case 0:{
                double price;
                string name;
                int count;
                cout << "Type name\n";
                cin >> name;
                cout << "Type price\n";
                cin >> price;
                cout << "Type count\n";
                cin >> count;
                mypharmacy.addNewMedicine(name, price, count);
                break;
            }
            case 1:{
                string name;
                int count;
                cout << "Type name\n";
                cin >> name;
                cout << "Type count\n";
                cin >> count;
                mypharmacy.sealeMedicine(name, count);
                break;
            }
            case 2:{
                string name;
                cout << "Type name\n";
                cin >> name;
                mypharmacy.findMedicine(name);
                break;
            }
            case 3:{
                string name;
                int count;
                cout << "Type name\n";
                cin >> name;
                cout << "Type count\n";
                cin >> count;
                mypharmacy.addMedicine(name, count);
                break;
            }
            case -1:
                start = false;
                break;
            default:
                cout << "Please type correct valid op_code\n";
        }
    }
    
}
