# Checking-BST
Checking function for binary tree is BST or not, C++#include <iostream>
using namespace std;
struct Node {
	int data;
	Node *left, *right;
};
Node* newNode(int data)
{
	Node* temp = new Node;
	temp->data = data;
	temp->left = temp->right = NULL;
	return temp;
}
void printInorder(struct Node* node)
{
	if (node == NULL)
		return;
	printInorder(node->left);
	cout << node->data << " ";
	printInorder(node->right);
}
/*
     10
    /  \
   8   11
 /  \    
7   9

    */

int isBST(struct Node*root){
	static struct Node* prev=NULL;
	if(root!=NULL){
	     if(!isBST(root->left)){// if conditon true return 0
		    return 0;
	     }// previous is pointing to the root node of tree
	     if(prev!=NULL && root->data<=prev->data){// we are standing on left root node and level 1
			return 0;
	    }
	prev=root;// previous = root of our tree, s
	return isBST(root->right);// same as check for left node data,  checking the ascending order of element
}
else{
	return 1;
}	
}
int main()
{
	//Root node
	struct Node* root = newNode(7);
	//level 1
	root->left = newNode(4);
	root->right = newNode(12);
	//level 2
	root->left->left = newNode(2);
	root->left->right = newNode(6);
	root->left->left->right = newNode(3);
	root->left->right->left = newNode(5);
    root->right->left = newNode(9);
	root->right->right = newNode(19);
	root->right->left->right = newNode(11);
	root->right->left->left = newNode(8);
	root->right->right->left = newNode(15);
	root->right->right->right = newNode(20);
	
	cout << "\nInorder traversal of binary tree  "<<endl;
	printInorder(root);
	
	if(isBST(root)){
		cout<<" \nThis tree is Binary Search Tree  "<<endl;	
	}else{
		cout<<" This tree is NOT Binary Search Tree  "<<endl;
	}
	return 0;
}

