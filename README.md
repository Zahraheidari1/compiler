# compiler
// C++ program to implement Symbol Table
#include <iostream>
using namespace std;

const int MAX = 100;

class Node {

	string symbol, scope, type;
	Node* next;

public:

	Node(string key, string value, string type, int lineNo)
	{
		this->symbol = key;      // for example  symbol   scope   type
		this->scope = value;     //              tow_3    inner   int
		this->type = type;       //              pro_one  global  proc

		next = NULL;
	}

	void print()
	{
		cout << "Identifier's Name:" << symbol
			<< "\nType:" << type
			<< "\nScope: " << scope
			<< endl;
	}
	friend class SymbolTable;
};

class SymbolTable {
	Node* head[MAX];

public:
	SymbolTable()
	{
		for (int i = 0; i < MAX; i++)
			head[i] = NULL;
	}

	int hash(string id); // hash function for length id =>id[]
	string find(string id);
	bool insert(string id, string scope,
		string Type, int lineno);
	bool deleteRecord(string id);

	bool modify(string id, string scope,
		string Type);
};

int SymbolTable::hash(string id)
{
	int Sum = 0;

	for (int i = 0; i < id.length(); i++) {
		Sum = Sum + id[i];
	}

	return (Sum);
}
// Function to modify an sym
bool SymbolTable::modify(string id, string s,
	string t)
{
	int index = hash(id);
	Node* start = head[index];

	if (start == NULL)
		return "-1";
	else
	while (start != NULL) {
		if (start->symbol== id) {
			start->scope = s;
			start->type = t;
			return true;
		}
		start = start->next;
	}

	return false; // id not found
}
bool SymbolTable::insert(string id, string scope,
	string Type, int lineno)
{
	int index = hash(id);
	Node* p = new Node(id, scope, Type, lineno);

	if (head[index] == NULL) {
		head[index] = p;
		cout << "\n"
			<< id << " inserted";

		return true;
	}

	else {
		Node* start = head[index];
		while (start->next != NULL)
			start = start->next;

		start->next = p;
		cout << "\n"
			<< id << " inserted";

		return true;
	}

	return false;
}
int main()
{
	SymbolTable s;
	
}
