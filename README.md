//Lab11

// Project 2: Common Password Checker

#include<iostream>
using std::cout; using std::endl;
#include<string>
using std::string;
#include<vector>
using std::vector;
#include<algorithm>
using std::sort;
#include<iterator>
using std::ostream_iterator;
#include<utility>
using std::pair;
using std::make_pair;
#include<fstream>
using std::ifstream;
using std::fixed;
#include<numeric>
#include<cmath>
#include <cstdlib>
using std::abs;

auto diff_metric(std::string a, std::string b) {
    int differences = 0;
    if(a.length() < b.length()) {
        for(size_t i = 0; i < a.length(); i++) {
            if(a[i] != b[i]) {
                differences++;
            }
        }
        differences = differences + abs(static_cast<int>(a.length()) - static_cast<int>(b.length()));
    } else {
        for(size_t i = 0; i < b.length(); i++) {
            if(a[i] != b[i]) {
                differences++;
            }
        } 
        differences = differences + abs(static_cast<int>(a.length()) - static_cast<int>(b.length()));
    }
    return differences;
}

int main() {
    std::ifstream file("common_passwords.txt");

    std::string user_input;
    cout << "Give me a password: ";
    std::cin >> user_input;
    cout << "You provided a password of " << user_input << endl;
    cout << "The most similar passwords to " << user_input << " are:" << endl;

    std::string password;
    std::vector <std::pair<int, std::string>> pass_vect; //string is comparing to user_input, int is difference

    while(file >> password) {
        // cout << password << endl;               prints 123456
        // cout << " " << endl;
        pass_vect.push_back(std::make_pair(diff_metric(user_input, password),password));
    }
    std::sort(pass_vect.begin(), pass_vect.end());

    int min = pass_vect[0].first;
    for(std::vector<int>::size_type i = 0; i < pass_vect.size(); i++) {
        if(pass_vect[i].first == min) {
            cout << pass_vect[i].second << ", ";
        }
    }
    cout << "\n";
    cout << "All of which are " << min << " character(s) different." << endl;
}
