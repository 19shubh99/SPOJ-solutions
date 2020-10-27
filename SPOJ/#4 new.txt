#include<bits/stdc++.h>
using namespace std;
int pre(char c){
    if(c=='^')
       return 3;
    else if(c=='*'||c=='/')
        return 2;
    else if(c=='+'||c=='-')
        return 1;
    else 
        return -1;
}
string RPN(stack<char>s,string infix){
    int n=infix.length();
    string postfix;
    for(int i=0;i<n;i++){
        if(infix[i]>='a'&&infix[i]<='z'){
            postfix+=infix[i];
        }
        else if(infix[i]=='('){
            s.push(infix[i]);
        }
        else if(infix[i]==')'){
            while((s.top()!='(')&&(!s.empty())){
                postfix+=s.top();
                s.pop();
            }
            if(s.top()=='('){
                s.pop();
            }
        }
        else{
            if(s.empty()){
                s.push(infix[i]);
            }
            else{
                if(pre(infix[i])>pre(s.top())){
                    s.push(infix[i]);
                }
                else if(pre(infix[i])==pre(s.top())&&(infix[i]=='^')){
                    s.push(infix[i]);
                }
                else{
                    while((!s.empty())&&pre(infix[i])<=pre(s.top())){
                        postfix+=s.top();
                        s.pop();
                    }
                    s.push(infix[i]);
                }
            }
        }
    }
    while(!s.empty()){
        postfix+=s.top();
        s.pop();
    }
    return postfix;
}
int main(){
    int t;
    cin>>t;
    while(t--){
    string i,e;
    cin>>i;
    stack<char>s;
    e=RPN(s,i);
    cout<<e<<endl;
}}