#include <iostream>
#include <vector>

using namespace std;


void displayAdjacencyMatrix(const vector<vector<int>>& matrix); 
void displayAdjacencyList(const vector<vector<int>>& list);  
void dfsVisit(int u, int& time, const vector<vector<int>>& adjList, vector<string>& color, vector<int>& predecessor, vector<int>& firstTime, vector<int>& lastTime);
void printTrackingTable(const int& time, const vector<string>& color, const vector<int>& predecessor, const vector<int>& firstTime, const vector<int>& lastTime);


int main() {
		int numVertices, numEdges;
		cout << "Enter the number of vertices(nodes) and edges (with a space in between): ";
		cin >> numVertices >> numEdges;

		// Initializes adjacency matrix and list
		vector<vector<int>> adjMatrix(numVertices, vector<int>(numVertices, 0));
		vector<vector<int>> adjList(numVertices);

		// Takes in edges and populates matrix / list
		cout << "Note: This is a directed graph, so the first letter is the start and the second letter is where the arrow points to.\n";
		for (int i = 0; i < numEdges; ++i) {
				char uChar, vChar;
				cout << "Enter the vertices for edge " << i << " (example, A B): ";
				cin >> uChar >> vChar;
				int u = toupper(uChar) - 'A';   // In case user inputs lower case
				int v = toupper(vChar) - 'A';

				// Checks if the vertex is within the range of valid vertices characters
				if (u >= 0 && u < numVertices && v >= 0 && v < numVertices) {
						adjMatrix[u][v] = 1; // Directed graph. Edge is from u to v
						adjList[u].push_back(v);
				}
				else {
						cout << "Invalid vertex name. Please use letters A-" << char('A' + numVertices - 1) << endl;
						i--;
				}
		}

	displayAdjacencyMatrix(adjMatrix);
	displayAdjacencyList(adjList);

	cout << "Enter the starting vertex (example, A): ";
	char startVertexChar;
	cin >> startVertexChar;
	cout << endl;
	int startVertex = toupper(startVertexChar) - 'A'; // Finds the index based on user letter inpute

	// Checks if the start vertex is within the valid range
	if (startVertex < 0 || startVertex >= numVertices) {
			cout << "Invalid starting vertex. Please enter a letter from A to " << char('A' + numVertices - 1) << endl;
			cin >> startVertexChar;
			int startVertex = toupper(startVertexChar) - 'A';

			if (startVertex < 0 || startVertex >= numVertices) {
					cout << "Error: Second wrong input. Exiting program." << endl;
					return 1;
			}
	}

	// Initializes all vertices and starts DFS
	vector<string> color(numVertices, "white");
	vector<int> predecessor(numVertices, -1);
	vector<int> firstTime(numVertices, 0);
	vector<int> lastTime(numVertices, 0);
	int time = 0;

	printTrackingTable(time, color, predecessor, firstTime, lastTime);

	dfsVisit(startVertex, time, adjList, color, predecessor, firstTime, lastTime);

	// Continues DFS for any unconnected vertices
	for (int u = 0; u < numVertices; ++u) {
			if (color[u] == "white") {
					dfsVisit(u, time, adjList, color, predecessor, firstTime, lastTime);
			}
	}

	cout << "^^^Final Tracking Table^^^\n";

		return 0;
}

void dfsVisit(int u, int& time, const vector<vector<int>>& adjList, vector<string>& color, vector<int>& predecessor, vector<int>& firstTime, vector<int>& lastTime) {
		color[u] = "grey_";
		firstTime[u] = ++time;
		printTrackingTable(time, color, predecessor, firstTime, lastTime); 

		for (int v : adjList[u]) {
				if (color[v] == "white") {
						predecessor[v] = u;
						dfsVisit(v, time, adjList, color, predecessor, firstTime, lastTime);
				}
		}

		color[u] = "black";
		lastTime[u] = ++time;
		printTrackingTable(time, color, predecessor, firstTime, lastTime); 
}

void printTrackingTable(const int& time, const vector<string>& color, const vector<int>& predecessor, const vector<int>& firstTime, const vector<int>& lastTime) {
		cout << "Time: " << time << " Tracking Table:\n";
		cout << "Vertex | Color | Predecessor | First-Time | Last-Time\n";
		for (int u = 0; u < color.size(); ++u) {
				cout << char('A' + u) << "      | " << color[u] << "   | " << (predecessor[u] == -1 ? "^" : string(1, 'A' + predecessor[u])) << "         | " << firstTime[u] << "         | " << lastTime[u] << "\n";
		}
		cout << endl;
}

void displayAdjacencyMatrix(const vector<vector<int>>& matrix) {
		int numVertices = matrix.size();
		cout << "\nAdjacency Matrix:" << endl;

		// Prints the column header
		cout << "  ";
		for (int i = 0; i < numVertices; ++i) {
				cout << char('A' + i) << " ";
		}
		cout << endl;

		// Prints the matrix
		for (int i = 0; i < numVertices; ++i) {
				// Prints the row label
				cout << char('A' + i) << " ";
				for (int j = 0; j < numVertices; ++j) {
						// Prints each cell value
						cout << matrix[i][j] << " ";
				}
				cout << endl;
		}
}

void displayAdjacencyList(const vector<vector<int>>& list) {
		cout << "\nAdjacency List:" << endl;
		for (int i = 0; i < list.size(); ++i) {
				// Prints the current vertex
				cout << "Vertex " << char('A' + i) << ": ";

				// Prints all adjacent vertices
				for (int j : list[i]) {
						cout << char('A' + j) << " ";
				}
				cout << endl;
		}
}
