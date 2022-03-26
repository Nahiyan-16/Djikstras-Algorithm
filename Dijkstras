//NAHIYAN AHMED
#include<iostream>
#include<fstream>
#include<string>
#include<sstream>

using namespace std;

class DijkstraSSS{
private:
    int numNodes;
    int sourceNode;
    int minNode;
    int currentNode;
    int newCost;
    int **costMatrix;
    int *fatherAry;
    int *ToDoAry;
    int *BestAry;
public:
    DijkstraSSS(int n){
        numNodes = n;
        }
    void initializeAry(){
        costMatrix = new int*[numNodes+1];
        for(int i = 1; i <= numNodes;i++) costMatrix[i] = new int[numNodes+1];
        fatherAry = new int[numNodes + 1];
        ToDoAry = new int[numNodes + 1];
        BestAry = new int[numNodes + 1];
        }
    void allocateAry(){
        for(int i = 1; i <= numNodes; i++){
            for(int j = 1; j <= numNodes; j++){
                if(i == j){
                    costMatrix[i][j]=0;
                    }
                else{
                    costMatrix[i][j]=9999;
                    }
                }
            fatherAry[i] = 0;
            ToDoAry[i] = 1;
            BestAry[i] = 9999;
            }
        }
    void loadCostMatrix(ifstream &i){
        int firstNode, secondNode, cost;
        while (i>>firstNode && i>>secondNode && i>>cost){
            costMatrix[firstNode][secondNode] = cost;
            }
        }
    void setBestAry(int src){
        for(int i = 1; i <= numNodes; i++){
            for(int j = 1; j <= numNodes; j++){
                if(src == i){
                    BestAry[j]= costMatrix[i][j];
                    }
                }
            }
        }
    void setFatherAry(int src){
        for(int i = 1; i <= numNodes; i++){
            fatherAry[i] = src;
            }
        }
    void setToDoAry(int src){
        for(int i = 1; i <= numNodes; i++){
            if(src == i){
                ToDoAry[i] = 0;
            }
            else{
                ToDoAry[i] = 1;
                }
            }
        }
    bool checkToDoAry(){
        for(int i = 1; i <= numNodes; i++){
            if(ToDoAry[i] != 0){
                return false;
                }
            }
            return true;
        }
    void DijkstraMethod(ofstream &dFile, ofstream &SSSfile){
        SSSfile<<"========================================================================================="<<endl;
        SSSfile<<"There are "<<numNodes<<" nodes in the input graph. Below are all paris of shortest paths:"<<endl;
        SSSfile<<"========================================================================================="<<endl;
        sourceNode = 1;
        while(sourceNode <= numNodes){
        setBestAry(sourceNode);
        setFatherAry(sourceNode);
        setToDoAry(sourceNode);
        while(checkToDoAry()!=true){
        minNode = findMinNode();
        ToDoAry[minNode] = 0;
        debugPrint(dFile);
        int childNode = 1;
        while(childNode<=numNodes){
        if(ToDoAry[childNode] == 1){
            newCost = computeCost(minNode, childNode);
            if(newCost < BestAry[childNode]){
                BestAry[childNode] = newCost;
                fatherAry[childNode] = minNode;
                debugPrint(dFile);
                            }
                        }
            childNode++;
                    }
                }
        currentNode = 1;
        SSSfile<<"SOURCE NODE = "<<sourceNode<<endl;
        while(currentNode <= numNodes){
            printShortestPath(currentNode,sourceNode,SSSfile);
            currentNode++;
            }
        sourceNode++;
            }
        }
    void printShortestPath(int n, int src, ofstream &file){
            if(n == src){
                file<<"The path from "<<src<<" to "<<n<<": "<<n<<" <- "<<n<<": cost = 0"<<endl;
                }
            else if(fatherAry[n] == src){
                file<<"The path from "<<src<<" to "<<n<<": "<<n<<" <- "<<src<<": cost = "<<BestAry[n]<<endl;
                }
            else {
                file<<"The path from "<<src<<" to "<<n<<": "<<n<<" <- ";
                int father = n;
                while(fatherAry[father]!=src){
                    file<<fatherAry[father]<<" <- ";
                    father = fatherAry[father];
                    }
                file<<src<<": cost = "<<BestAry[n]<<endl;
                }
        }
    int computeCost(int m, int c){
        return BestAry[m] + costMatrix[m][c];
        }
    int findMinNode(){
        int minCost = 99999;
        minNode = 0;
        int index = 1;
        while(index <= numNodes){
            if(ToDoAry[index] == 1 && BestAry[index] < minCost){
                minCost = BestAry[index];
                minNode = index;
                }
            index++;
            }
        return minNode;
        }
    void debugPrint(ofstream &file){
        file<<"The sourceNode is: "<<sourceNode<<endl;
        
        file<<"The fatherAry is:[";
        for(int i = 1; i <= numNodes; i++){
            if(i == numNodes){
                file<<fatherAry[i];
                }
            else{
                file<<fatherAry[i]<<", ";
                }
            }
        file<<"]"<<endl;
        
        file<<"The bestCostAry is:[";
        for(int i = 1; i <= numNodes; i++){
            if(i == numNodes){
                file<<BestAry[i];
                }
            else{
                file<<BestAry[i]<<", ";
                }
            }
        file<<"]"<<endl;
        
        file<<"The ToDoAry is:[";
        for(int i = 1; i <= numNodes; i++){
            if(i == numNodes){
                file<<ToDoAry[i];
                }
            else{
                file<<ToDoAry[i]<<", ";
                }
            }
        file<<"]"<<endl;
        }
    };

int main(int argc, char *argv[])
{
    //argv[1] - Data 1
    //argv[2] - Data 2
	ifstream inFile;
    inFile.open(argv[2]);
    ofstream SSSfile;
    SSSfile.open(argv[3]);
    ofstream deBugFile;
    deBugFile.open(argv[4]);
    
    int numNodes;
    inFile>>numNodes;
    
    DijkstraSSS d(numNodes);
    d.initializeAry();
    d.allocateAry();
    
    d.loadCostMatrix(inFile);
    
    d.DijkstraMethod(deBugFile,SSSfile);
    
    inFile.close();
    SSSfile.close();
    deBugFile.close();
	return 0;
}
