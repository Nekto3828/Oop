#include <iostream>
#include <map>
#include <set>
#include <string>

using namespace std;

int main() {
    map<string, set<string>> components;

    int Q;
    cin >> Q;

    for (int i = 0; i < Q; ++i) {
        
        string cmd;
        cin >> cmd;

        if (cmd == "ADD") {
            string ip1, ip2;
            cin >> ip1 >> ip2;

            if (components.find(ip1) == components.end())//не нашли нужный ip в мэп, //делаем ему свое множество
                components[ip1] = {ip1};
            if (components.find(ip2) == components.end())
                components[ip2] = {ip2};

            //ссылки на множества
            set<string>& s1 = components[ip1];
            set<string>& s2 = components[ip2];

            if (s1 == s2) continue;

            set<string> podset = s1;
            podset.insert(s2.begin(), s2.end()); //пихаем их в одну подсеть

            for (const string& ip : podset) { //переписываем значение для каждого //адреса из созданной подсети
                components[ip] = podset;
            }
        }
        else if (cmd == "COUNT") {
            string ip;
            cin >> ip;
            if (components.find(ip) == components.end())
                cout << 1 << endl; 
            else
                cout << (components[ip].size() - 1)<< endl;
        }
        else if (cmd == "CHECK") {
            string ip1, ip2;
            cin >> ip1 >> ip2;
            if (components.find(ip1) == components.end() || components.find(ip2) == components.end()) //если адреса не встр. до этого, то они точно в //разных
                cout << "NO" << endl;
            else
                cout << (components[ip1].count(ip2) ? "YES" : "NO") << endl;
        }
    }

    return 0;
}
