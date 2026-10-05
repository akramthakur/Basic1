class Solution {
public:
    void rec(vector<string> & res,int n ,int l , int r, string s){
        if(s.size()== (2*n)){
            res.push_back(s);
            return;
        }
        if(l<n){
            rec(res,n,l+1,r,s+"(");
        }
        if(r<l){
             rec(res,n,l,r+1,s+")");
        }
    }
    vector<string> generateParenthesis(int n) {
        vector<string>res ;
      
        rec(res,n,0,0,"");
        return res;
    }
};
