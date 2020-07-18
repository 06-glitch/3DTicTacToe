# 3DTicTacToe

#include <cstdlib>
#include <iostream>
#include <string>
#include <cstring>


using namespace std;

void DISPLAY (int *brd);
bool displayWINNER (int turn);
void resetARRAY ();
bool checkWINNER (int turn, int g, int r, int c);
int normalizeINPUT (string inp);

int turn, adj[6][6][6];


int main()
    {
         string inp;
         int g,r,c; 
         resetARRAY ();
         
    while (true) {
         turn++;
         DISPLAY (&adj[0][0][0]);
         if (turn%2==0) {cout<<"\nPlayer O, it's your turn!\n\n";}
             else {cout<<"\nPlayer X, it's your turn!\n\n";}
          cout<<"Enter grid number ('Q' to Quit) : ";
          getline (cin,inp);
          if ((inp[0]=='q')||(inp[0]=='Q')) break;
          g=normalizeINPUT(inp);
          if ((g<1)||(g>4)) {cout<<"\nInvalid selection.\n\n";            
                       system("PAUSE");turn--;continue;}
                       
          cout<<"Row number : ";
          getline (cin,inp);
          r=normalizeINPUT(inp);
          if ((r<1)||(r>4)) {cout<<"\nInvalid selection.\n\n";            
                       system("PAUSE");turn--;continue;}
                       
          cout<<"Column number : ";
          getline (cin,inp);
          c=normalizeINPUT(inp);
          if ((c<1)||(c>4)) {cout<<"\nInvalid selection.\n\n";            
                       system("PAUSE");turn--;continue;}
          if (adj[g][r][c]!=0) {cout<<"\nPlease select an unoccupied square!\n\n";
                       system("PAUSE");turn--;continue;}
          if (turn%2==0) {adj[g][r][c]=2;}
             else {adj[g][r][c]=1;}
          if (checkWINNER (turn,g,r,c)) {if(displayWINNER(turn)) break;}
         }
         cout<<"\n\n\n";
         return 0;
}


bool checkWINNER (int turn,int g,int r,int c) {
     int h=1;                   //sets 'h' to either
     if (turn%2==0) h=2;        //Xs or Os to check
     
     int x[4],y[4],z[4];        //variables to store winning coordinates
     x[0]=g;y[0]=r;z[0]=c;      //sets 0 of each to last move
     
     int ct;
     
     for (int a=1;a<14;a++){    //iterates through all possible directions
     
           ct=1;                      //each time resetting counter to one 
     
           int g2=g; int r2=r; int c2=c;
           
           for (int i=0;adj[g2][r2][c2]!=5;){

                 switch (a) {
                        case 1:g2--;break;                //////////////////////
                        case 2:g2--;r2--;c2--;break;      //  increments
                        case 3:g2--;r2--;break;           //  in each
                        case 4:g2--;r2--;c2++;break;      //  possible
                        case 5:g2--;c2--;break;           // direction
                        case 6:g2--;c2++;break;           //  until 
                        case 7:g2--;r2++;c2--;break;      // hitting
                        case 8:g2--;r2++;break;           //  a '5'
                        case 9:g2--;r2++;c2++;break;      //   
                        case 10:c2--;break;               //
                        case 11:r2--;c2--;break;          //   
                        case 12:r2--;break;               //  
                        case 13:r2--;c2++;break;          //////////////////////
                         }
                        
                 if (adj[g2][r2][c2]==h) {
                           x[ct]=g2;y[ct]=r2;z[ct]=c2;
                           ct++;}
                 
                 }
                 
                 
          g2=g;r2=r;c2=c;   //reset placeholder variables
         
         
          for (int i=0;adj[g2][r2][c2]!=5;) { 
              
              
                switch (a) {
                      case 1:g2++;break;                ///////////////////////
                      case 2:g2++;r2++;c2++;break;      //
                      case 3:g2++;r2++;break;           // and
                      case 4:g2++;r2++;c2--;break;      // then back
                      case 5:g2++;c2++;break;           //  in the
                      case 6:g2++;c2--;break;           //  opposite 
                      case 7:g2++;r2--;c2++;break;      //  direction
                      case 8:g2++;r2--;break;           //
                      case 9:g2++;r2--;c2--;break;      //
                      case 10:c2++;break;               //
                      case 11:r2++;c2++;break;          //
                      case 12:r2++;break;               //
                      case 13:r2++;c2--;break;          ///////////////////////
                      }
                                   
              if (adj[g2][r2][c2]==h) {
                      x[ct]=g2;y[ct]=r2;z[ct]=c2;
                      ct++;
                      }
               }
               if (ct>3) {for (int b=0;b<4;b++) {adj[x[b]][y[b]][z[b]]=4;} return 1;}
               }
     return 0;
}


     
int normalizeINPUT (string inp) {
    int i, q; 
    string n;
    for (int i=0;inp[i] != ' ';i++) n=n+inp[i];
    q=atoi(n.c_str());
    return q;
}

        
    

void DISPLAY(int *brd)
{
     system ("cls");
     cout <<"#1\t\t#2\t\t#3\t\t#4\n\n\n";
     int n;
     for (int y=1;y<5;y++) {
         for (int x=1;x<5;x++) {
             for (int z=1;z<5;z++) {
                 n=((x*36)+(y*6)+(z));
                 switch (*(brd+n)) {
                        case 0: cout<<" "; break;
                        case 1: cout<<"X"; break;
                        case 2: cout<<"O"; break;
                        case 4: cout<<(char)219;break;
                        }
                 if (z<4) cout<<(char)179;
                 }
             if (x<4) cout<<"\t\t";
             }
         if (y<4) {
                  cout<<"\n";
                  for (int m=1;m<32;m++) {
                       if (m%8==0) {cout<<"\t\t";}
                         else if (m%2==0) {cout<<(char)197;}
                           else cout<<(char)196;}
                            cout<<"\n";
                      }
                  
         }
     cout<<"\n\n\n\n";
     return;
     }
     
     
bool displayWINNER (int tn) {
     char yn[100];
     DISPLAY (&adj[0][0][0]);
     if (tn%2==0) {cout<<"\n\nO is the winner!!\n\n";}
        else cout<<"\n\nX is the winner!!\n\n";
     cout<<"Play again? (y/n) : ";
     cin>>yn;
     if (!strcmp(yn,"y")||!strcmp(yn,"Y")) {resetARRAY (); cin.ignore(1); turn=0; return 0;}
        else return 1;
}


void resetARRAY () {
     for (int x=0;x<6;x++) {
         for (int y=0;y<6;y++) {
             for (int z=0;z<6;z++) {
                 adj[x][y][z]=0;
                 }
             }
         }
     for (int i=0;i<6;i++) {
             for (int j=0;j<6;j++) {
                 adj[0][i][j]=5; adj[5][i][j]=5;
                 adj[i][j][0]=5; adj[i][j][5]=5;
                 adj[i][0][j]=5; adj[i][5][j]=5;}
                 }
         
     }
     
 
