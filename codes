#include <iostream>
#include<string>
#include<cmath>
#include<algorithm>
using namespace std;
//明文最大值
#define charNUM 10000
/**    维吉尼亚加密(循环加密)
    输入一个明文和密钥得到密文
*/
void Virginia()
{
    //     密文字符串
    string unciphertext;
    //     密钥
    string secretKey;
    //     转换后的密文
    string ciphertext ;
    //     密钥长度
    int skSize;
        //    当前密钥指针位置
    int skIndex=-1;
    //    指针位置对应的密钥字符
    char cipChar;

    cout<<"欢迎使用维吉尼亚密码加密，请输入明文"<<endl;
    cin>>unciphertext;
    cout<<"请输入密钥"<<endl;
    cin>>secretKey;
    skSize=secretKey.size();
    //    超大的明文长度


    for(long long unsigned i=0; i<unciphertext.size(); i++)
    {
    //    密钥指针循环移动
        skIndex++;
        skIndex=skIndex%skSize;
    //    当前所使用的密钥字符
        cipChar=secretKey[skIndex];
    //    字符转换
        ciphertext+=(unciphertext[i]-'a'+(cipChar-'a'))%26+'a';

    }
    cout<<"维吉尼亚加密后的密文为："<<endl;
    cout<<ciphertext;
}
/**
    e、d知一求一
    核心：（e*d-1）%product
           ed=k*product+c
           d=pro/e+(pro%e*k+c)/e
           形式一致，使用递归
           递归终止条件为：pro%e*k等于e-c或1
*/
int RSAbranch(int e,int product,int c)
{
    int d,k;
    //ed=k*product+c
    //d=pro/e+(pro%e*k+c)/e
    if(product%e==e-c)
    {
        k=1;
        d=(k*product+c)/e;
        return d;
    }
    else if(product%e==1)
    {
        k=e-c;
        d=(k*product+c)/e;
        return d;
    }
    //k=(et-c)/(pro%e)
    //k=e/(pro%e)+(e%(pro%e)*t-c)/(pro%e)
    k=RSAbranch(product%e,e,-c);
    d=(k*product+c)/e;
    return d;

}
/**
    大数取模
    求a^k%b的值
    其实可以更快，但那个算法实现上出现了一点问题就先用这个循环的代替了
    慢是慢了一点，但还是足够用
*/
int modPlus(int a,int k,int b)
{
    int ans=1;
    for(int i=0; i<k; i++)
    {
        ans=ans*a%b;
    }
    return ans;
}
//一种看起里似乎可行的大数取模的算法，但是return有问题，暂时没找到解决方法
//int RSAans(int a,int k,int b){
////求a^k%b a^k巨大无比
//    if(pow(a,k)<1e9){
//        a=pow(a,k);
//            cout<<a<<" "<<k<<" "<<a%b<<endl;
//        return a%b;
//
//    }
//    else if(a>b){
//    cout<<a<<" "<<k<<endl;
//            return RSAans(a%b,k,b);
//    }
//    else if(k%2){
//    cout<<a<<" "<<k<<endl;
//        return RSAans(a*a,k/2,b);
//    }else{
//            cout<<a<<" "<<k<<endl;
//        return (a*RSAans(a*a,k/2,b))%b;
//    }
//}
/**
    RSA算法
    输入明文序列和p、q、e、d（e,d）e和d输入一个即可，另一个输入0
    输出密文序列和其对应的ascii字符
*/
void RSA()
{
    //     明文字符串
    int unciphertext[charNUM];
    //      实际明文长度
    int charnum;
    //      用于输出结果的中间变量
    int ans;
    //      乘积 product=(p-1)*(q-1)
    int product;
    //      RSA相关参数，n=p*q
    int p,q,d,e,n;
    //      暂存e和d，方便后续交换
    int tempE,tempD;
    cout<<"欢迎使用RSA加密,请输入明文字符数"<<endl;
    cin>>charnum;
    cout<<"请输入明文序列"<<endl;
    for(int i=0; i<charnum; i++)
    {
        cin>>unciphertext[i];
    }
    cout<<"请输入p,q,d,e(d或e输入一个另一个输入0)"<<endl;
    cin>>p>>q>>d>>e;

    //     tempE为e和d中不为0的那个
    tempE=e!=0?e:d;
    //     模数，公钥即为（e，n）
    n=p*q;
    product=(p-1)*(q-1);
    //      (ed-1)%product==0
    //      ed=k*product+1 求k与d，辗转法
    tempD=RSAbranch(tempE,product,1);
    if(tempD>n){
        // 如果是知d求e,e要小于n
        cout<<"未找到公钥";
        return;
    }
    //     让tempE等于实际的e
    if(e==0){swap(tempD,tempE);}

    cout<<"公钥为：（"<<tempE<<","<<n<<")"<<endl;
    cout<<"私钥为：（"<<tempD<<","<<n<<")"<<endl;
    cout<<"密文为：";
    for(int i=0; i<charnum; i++)
    {
        ans=modPlus(unciphertext[i],tempE,n);
        printf("%d ",ans);
    }cout<<endl;
    cout<<"对应的字符为";
    for(int i=0; i<charnum; i++)
    {
        ans=modPlus(unciphertext[i],tempE,n);
        printf("%c ",ans);
    }


}


int main()
{
    //Virginia();
    RSA();
    return 0;
}
