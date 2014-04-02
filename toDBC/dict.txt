// ToDBC.cpp
// 全角转化为半角的函数
//
#include <stdio.h>
#include <iostream>
#include <fstream>
#include <string>
#include <map>
#include <sstream>
using namespace std;

// 转化函数
string ToDBC(string input);
// 在如转化字典
map<string,string> LoadDict();

int main()
{
    string str1 = "你好~github；Hello,word！";
    string str2;
    str2 = ToDBC(str1);
    std::cout << str2 << endl;
    return 0;
}

string ToDBC(string input)
{
    string line;
    string word;
    map<string,string> dict;
    int k = 0;
    for(int i = 0;i < input.length();i++)
    {
        if(input[i] < 128 && input[i]>0)
            line += input[i];
        else
        {
            k++;
            if(k==1)
                word = input[i];
            else
            {
                word = word + input[i];
                if(dict.count(word))
                {
                    line = line + word;
                }
                else
                    line = line + word;
                k = 0;
            }
        }
    }
    return line;
}

map<string,string> LoadDict()
{
    ifstream infile("dict.txt");
    map<string,string> wmap;
    if(!infile)
    {
        std::cout << "can not open dict.txt " << endl;
        _exit(1);
    }
    string line;

    while(getline(infile,line))
    {
        stringstream sin(line);
        string t1,t2;
        sin>>t2>>t1;
        wmap.insert(make_pair(t1,t2));
    }
    infile.close();
    return wmap;
}
