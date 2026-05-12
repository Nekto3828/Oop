''' cmd


mdaaa

#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

int main() {
    int Q;
    cin >> Q;
    
    vector<bool> ochered;  
    
    for (int i = 0; i < Q; ++i) {
        string op;
        cin >> op;
        
        if (op == "ARRIVE") {
            int k;
            cin >> k;
            if (k > 0) {
                ochered.insert(ochered.end(), k, false);//не пуш бэк потому что можно //без цикла обойтись
            } else {
                //удаляем пакеты с конца
                int antiminus = -k;
                ochered.resize(ochered.size() - antiminus);
            }
        }
        else if (op == "PRIORITY") {
            int i;
            cin >> i;
            ochered[i] = true;
        }
        else if (op == "NORMAL") {
            int i;
            cin >> i;
            ochered[i] = false;
        }
        else if (op == "PRIORITY_COUNT") {
            int cnt = count(ochered.begin(), ochered.end(), true);
            cout << cnt << endl;
        }
    }
    
    return 0;
}
'''
