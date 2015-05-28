---
layout: post
title: N Queen && Sudoku Solver
categories: [C++, Algorithm]
tags: [backtracking, recursion, Constraint Programming]
description: notes about n queen and sudoku solver
fullview: false
---

##N Queen && Suduku

###these two problems are in Leetcode

[n queen](https://leetcode.com/problems/n-queens/)

[sudoku solver](https://leetcode.com/problems/sudoku-solver/)

we can use backtracking and recursion to solve these two problems. Actually they belong to [Constraint Programming (coursera course)](https://class.coursera.org/optimization-001/lecture). The idea of constraint programming is we search through all the possible solution space, proceed under the constraint enforced by the previous steps. If we come up to a situation where we can not proceed anymore, we will backtrack. We will continue this process until we get a solution to the problem.

###N Queen

{% highlight c++ %}
class Solution {
public:
    bool constraint(int i, int j, int n, vector<string> &slu) {
        for (int r = 0; r < n; ++r) {
        	if (slu[i][r] == 'Q')
    	    return false;
    	if (slu[r][j] == 'Q')
    	    return false;
        }
        int c = i; int r = j;
        while (c < n && r < n) {
            if (slu[c++][r++] == 'Q')
    	    return false;
    	
        }
        c = i; r = j;
        while (c >= 0 && r >= 0) {
            if (slu[c--][r--] == 'Q') 
                return false;
        }
        c = i; r = j;
        while (c >= 0 && r < n) {
            if (slu[c--][r++] == 'Q') 
    	    return false;
        }
        c = i; r = j;
        while (c < n && r >= 0) {
            if (slu[c++][r--] == 'Q')
    	    return false;
        }
        return true;
    }

    void getNQueens(int n, int row, int start, vector<string> &slu, vector<vector<string> > &result) {
       row = row % n;
       if (row != start) {
            for (int j = 0; j < n; ++j) {
                if (slu[row][j] == '.' && constraint(row, j, n, slu)) {
                    slu[row][j] = 'Q';
                    getNQueens(n, row+1,start, slu, result);
    		        slu[row][j] = '.';
    	        }
    	    }
        }
        if (row % n == start) {
            result.push_back(slu);
        }
    }

    vector<vector<string> > solveNQueens(int n) {
        string temp;
        for (int i = 0; i < n; ++i) {
            temp.push_back('.');
        }

        //cout << temp << endl;
        vector<string> slu;
        for (int j = 0; j < n; ++j) {
    	    slu.push_back(temp);
        }
        
        vector<vector<string> > result;
        for (int i = 0; i < n; ++i) {
            slu[i][0] = 'Q';
            getNQueens(n, (i+1), i, slu, result);
    	    slu[i][0] = '.';
        }
        return result;
    }
    
};

{% endhighlight %}


###Sudoku Solver

{% highlight c++ %}
class Solution {
    set<char> dict1[9];  // for col
    set<char> dict2[9];   // for row
    set<char> dict3[3][3];
    bool find;
public:
 
    void p(vector<vector<char>>& board ) {
         cout << endl;
         for (int i = 0; i < 9; ++i) {
	    for(int j = 0; j < 9; ++j) {
	        cout << board[i][j] << " ";
	    }
            cout << endl;
	 } 
	 cout << endl;
    }

    void initdict(vector<vector<char>>& board) {
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                if (board[i][j] != '.') {
                    dict1[i].insert(board[i][j]);
                    dict2[j].insert(board[i][j]);
                    dict3[i/3][j/3].insert(board[i][j]);
                }
            }
        }
    }

    bool canput(char start, int i, int j, vector<vector<char>>& board) {
        if (dict1[i].find(start) != dict1[i].end()) {
            return false;
        } 
        
        if (dict2[j].find(start) != dict2[j].end()) {
            return false;
        } 
        
        if (dict3[i/3][j/3].find(start) != dict3[i/3][j/3].end()) {
            return false;
        } 
        
        dict1[i].insert(start);
        dict2[j].insert(start);
        dict3[i/3][j/3].insert(start);
        return true;
        
    }

    void erasefromdict(vector<vector<char>>& board, int i, int j, char s) {
        dict1[i].erase(s);
        dict2[j].erase(s);
        dict3[i/3][j/3].erase(s);
    }

    void solveSudoku(vector<vector<char>>& board, int i, int j) {
	
        if (board[i][j] == '.') {
            char start = '1';
            for (; start <= '9'; ++start) {
                if (canput(start, i, j, board)) {
                
                    board[i][j] = start; // put
                    if (i != 8 && j == 8) {
                        solveSudoku(board, i+1, 0);
                        if (find == true) {
                            return;
                        }
                        
                        // backtracking
                        board[i][j] = '.';
                        erasefromdict(board, i, j, start);
                    
                    } else if (i == 8 && j == 8) {
                        find = true;
                        return;
            
                    } else {
                        solveSudoku(board, i, j+1);
                        if (find == true) {
                            return;
                        }
                        
                        // backtracking
                        board[i][j] = '.';
                        erasefromdict(board, i, j, start);
                    
                    }
                }
                
            }

        } else {
            if (i != 8 && j == 8) {
                solveSudoku(board, i+1, 0);

            } else if (i == 8 && j == 8) {
                find = true;
                return;

            } else {
                solveSudoku(board, i, j+1);
            }
            
            if (find == true) {
                return;
            }
        }
        
        
    }

    void solveSudoku(vector<vector<char>>& board) {
        find = false;
        initdict(board);
        solveSudoku(board, 0, 0);
    }
};

{% endhighlight %}
