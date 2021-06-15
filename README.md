# Prims-algorithm-code-in-c++-to-find-minimum-cost

#include <iostream>
#include <cstring>
using namespace std;

int prims_algo()
{
    int n;
    cout<<"\nEnter the total number of offices in all cities :- "<<endl;          //Accept the cost matrix
    cin>>n;
    int cost_mat[n][n];
    cout<<"\nEnter the cost of telephone lines between specified cities.\n\n( If there is no line, please enter 999 as the cost. )"<<endl;
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            cout<<"\nCost between "<<i<<" and "<<j<<" is :- "<<endl;
            cin>>cost_mat[i][j];
        }
    }

    cout<<"\nThe cost matrix is:- "<<endl;                                         //display the cost matrix
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++)
        {
            cout<<"\t"<<cost_mat[i][j];
        }
        cout<<"\n"<<endl;
    }

    int st,nv;
    int t[n-1][3];                                                             //t array to store visited nodes in the mst
    int nearest[n];                                                           //nearest array to store previous node of all nodes
    cout<<"\nEnter the starting city ID (IDs from 0 to n-1) :- "<<endl;
    cin>>st;                                                                   //starting node in st
    nearest[st] = -1;
    cout<<"\nThe most efficient path is :- "<<endl;
    int r=0;
    int cost=0;
    for(int i=0;i<n;i++)                                                      //initially, nearest of each vertex = starting vertex (except for starting vertex itself)
    {
        if(i!=st)
            nearest[i]=st;
    }
    for(int i=0;i<n;i++)             //i loop for selecting the source vertex                                              //nested loop to calculate the minimum path to next node
    {
        int mini = 999;
        for(int j=0;j<n;j++)        //j loop to select destination vertex
        {
            int l=nearest[j];
            if(l != -1 && cost_mat[j][l] < mini)
            {
                mini = cost_mat[j][l];
                nv = j;
            }
        }
        t[r][0]=nearest[nv];                                               //store current and previous node and cost in t array
        t[r][1]=nv;
        t[r][2]=cost;
        if(t[r][0]!=-1)
            cout<<t[r][0]<<" ----> "<<t[r][1]<<endl;                       //print the visited minimum path
        r++;
        nearest[nv] = -1;
        if(mini!=999)
            cost=cost+mini;                                               //calculate minimum cost
        for(int k=0;k<n;k++)                                                                                   //loop to select next node to be visited (considering the least cost each time)
        {
            if(nearest[k]!=-1 && cost_mat[k][nv] < cost_mat[k][nearest[k]])       
            {
                nearest[k]=nv;
            }
        }
    }
    return cost;
}

int main()
{
    int ch;
    do
    {
        cout<<"\n************** MENU **************"<<endl;
        cout<<"\n1. Display Route for minimum cost (Minimum cost Spanning Tree).\n2. Calculate Minimum Cost.\n3. Exit"<<endl;
        cout<<"\n******************************"<<endl;
        cout<<"\nEnter Your Choice :- "<<endl;
        cin>>ch;
        switch(ch)
        {
        case 1:
            int min_cost;
            min_cost=prims_algo();
            break;
        case 2:
            cout<<"\nMinimum cost for telephone lines installation = "<<min_cost<<endl;
            break;
        case 3:
            break;
        default:
            cout<<"\nWrong choice."<<endl;
        }
    }while(ch!=3);

}
