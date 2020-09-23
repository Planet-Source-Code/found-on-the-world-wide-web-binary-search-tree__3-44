<div align="center">

## Binary Search Tree


</div>

### Description

This program implements a doubly linked list as a binary search tree and includes functions to: traverse inorder, preorder & postorder, insert and delete a node, search for a node, and count the height of a given leaf.
 
### More Info
 
The following letters are the contents of the data file btree.dat:

MFTCIPWADGKORVYBEHJLNQSUXZ

Just create a file called btree.dat and put these letters inside.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Found on the World Wide Web](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/found-on-the-world-wide-web.md)
**Level**          |Unknown
**User Rating**    |3.5 (28 globes from 8 users)
**Compatibility**  |C, C\+\+ \(general\)
**Category**       |[Data Structures](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/data-structures__3-8.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/found-on-the-world-wide-web-binary-search-tree__3-44/archive/master.zip)





### Source Code

```
#include <stdio.h>
#include <stdlib.h>
/* Binary Tree Structure Template */
typedef struct binary_tree
{
 char letter;
  struct binary_tree *left;
  struct binary_tree *right;
} TREE;
/* Function declarations */
TREE *fillTree(TREE *);
void insert(char, TREE **);
void menu(TREE *);
void displayInfo();
void inorder(TREE *);
void preorder(TREE *);
void postorder(TREE *);
int search(TREE *, char, int);
void freeTree(TREE *);
int deleteNode(TREE *, char);
/* Begin main function */
void main()
{
  TREE *root=NULL;            /* Create the root pointer */
 root=fillTree(root);          /* Fill the tree */
  menu(root);              /* Pass menu root, and enjoy */
}
/* Begin fillTree function */
TREE *fillTree(TREE *root)
{
  FILE *fin=fopen("btree.dat","r");   /* Open data file & create FILE ptr */
  char letter;
  while(fscanf(fin,"%c",&letter)!=EOF)  /* Fill tree letter by letter */
  insert(letter, &root);
  return root;
}
/* Begin insert function */
void insert(char newLetter, TREE **root)
{
 TREE *process;
  if(*root == NULL){
  process = (TREE *)malloc(sizeof(TREE));
   if(process!= NULL){
    process->letter = newLetter;
     process->left = NULL;
     process->right = NULL;
     *root = process;
   }
   else
    printf("Out of memory, can't insert letter.\n");
 }
  else{
  if(newLetter < (*root)->letter) insert(newLetter, &((*root)->left));
   else insert(newLetter, &((*root)->right));
  }
}
/* Begin menu function */
void menu(TREE *root)
{
 int choice, result, count;
  char target, process;
  displayInfo();
  while((scanf("%d",&choice)!=8)){
  switch(choice){
    case 1:         /* Traverse BST inorder */
      puts("");
     inorder(root);
      displayInfo();
      break;
     case 2:         /* Traverse BST in preorder */
      puts("");
     preorder(root);
      displayInfo();
      break;
     case 3:         /* Traverse BST in postorder */
      puts("");
     postorder(root);
      displayInfo();
      break;
     case 4:         /* Search BST for a node */
     count=0;
      puts("");
      printf("\nEnter target to search for: ");
    flushall();     /* Clear input buffer */
    scanf("%c",&target);
    result=search(root, target, count);
    if(result==-1) printf("\nTarget does not exist.");
    else
     printf("\nTarget %c found in %2d searches.\n", target, result);
    displayInfo();
    break;
   case 5:         /* Count height of a node */
    count=0;
    puts("");
    printf("\nEnter character to count height of: ");
    flushall();     /* Clear input buffer */
    scanf("%c",&target);
    result=search(root, target, count);
    if(result==-1) printf("\nTarget does not exist.");
    else
     printf("\nCharacter %c has a height of %2d.", target, result-1);
    displayInfo();
    break;
   case 6:         /* Insert node into BST */
    puts("");
    printf("\nEnter character to insert into binary search tree: ");
    flushall();     /* Clear input buffer */
    scanf("%c",&process);
    insert(process,&root);
    printf("\nThe character %c was inserted.", process);
    displayInfo();
    break;
     case 7:         /* Delete node from BST */
      puts("");
      printf("\nEnter character to delete from binary search tree: ");
    flushall();     /* Clear input buffer */
    scanf("%c",&process);
      result=deleteNode(root, process);
      if(result==0) printf("\nCharacter doesn't exist.");
    else printf("\nCharacter %c deleted.", process);
      displayInfo();
      break;
   case 8:         /* Au Revoir! */
    printf("\nHave a nice day. Goodbye.");
    freeTree(root);
    break;
   default:        /* Let user know they made an invalid choice */
    puts("");
    printf("Invalid selection\n\n");
    displayInfo();
    break;
  } /* End switch */
 }  /* End while */
}
/* Begin displayInfo function */
void displayInfo()
{
 printf("\n\n");
 puts("--------------------------------------------------");
 puts("     Binary Search Tree Menu Options     ");
 puts("--------------------------------------------------");
 printf("\n");
 printf("\t 1 Display inorder traversal\n");
 printf("\t 2 Display preorder traversal\n");
 printf("\t 3 Display postorder traversal\n");
 printf("\t 4 Search for a given node\n");
 printf("\t 5 Count the height of a given node\n");
 printf("\t 6 Insert a node onto the tree\n");
 printf("\t 7 Delete a node from the tree\n");
 printf("\t 8 Quit program\n");
 printf("\n");
 printf("Enter your selection: ");
}
/* Begin inorder function */
void inorder(TREE *root)
{
 if(root->left!=NULL) inorder(root->left);
 printf("%c",root->letter);
 if(root->right!=NULL) inorder(root->right);
}
/* Begin preorder function */
void preorder(TREE *root)
{
 printf("%c",root->letter);
 if(root->left!=NULL) preorder(root->left);
 if(root->right!=NULL) preorder(root->right);
}
/* Begin postorder function */
void postorder(TREE *root)
{
 if(root->left!=NULL) postorder(root->left);
 if(root->right!=NULL) postorder(root->right);
 printf("%c",root->letter);
}
/* Begin search function */
int search(TREE *root, char target, int count)
{
  if(root==NULL) return -1;         /* Target doesn't exist */
 count++;
 if(root->letter==target) return count;  /* Target found */
 if(target > root->letter)
  return search(root->right, target, count);
 if(target < root->letter)
  return search(root->left, target, count);
 return 007;                /* Bond, James Bond */
}
/* Begin freeTempTree function */
void freeTree(TREE *root)
{
 if(root!=NULL){        /* As long as root isn't null, recursively */
  freeTree(root->left);   /* travel tree in postorder freeing the   */
   freeTree(root->right);   /* nodes as you go.             */
   free(root);
  }
}
/* Begin deleteNode function */
int deleteNode(TREE *T_ptr, char target)
 {
  int  rt_child = 0, lft_child = 0;
  TREE *ptr = T_ptr, *parent = T_ptr, *S = T_ptr, *save = T_ptr;
 /*-----------------------------------------------+
  |        Find the node
  +-----------------------------------------------*/
  while (ptr != NULL && ptr->letter != target) {
   parent = ptr;
   if (target < ptr->letter) ptr = ptr->left;
   else ptr = ptr->right;
  }
  if (ptr == NULL) return 0;  /* Nothing to delete */
  else if (S->letter == target && (S->left == NULL || S->right == NULL))
   S = (S->left == NULL) ? S->right : S->left;
  else
   /*-----------------------------------------------+
   |   Delete a node without a left child
   +-----------------------------------------------*/
   if (ptr->left == NULL)
     if (target < parent->letter) parent->left = ptr->right;
     else parent->right = ptr->right;
   /*-----------------------------------------------+
   |   Delete a node without a right child
   +-----------------------------------------------*/
   else if (ptr->right == NULL)
     if (target < parent->letter) parent->left = ptr->left;
     else parent->right = ptr->left;
   /*--------------------------------------------------------------+
   |   Delete a node with both chidren--use RsmallestS subtree.
   +--------------------------------------------------------------*/
   else {
     save = ptr;
     parent = ptr;
     if ((ptr->left) >= (ptr->right)) {
      ptr = ptr->left;       /* Delete from left subtree.*/
      while (ptr->right != NULL) {
        rt_child = 1;
        parent = ptr;
        ptr = ptr->right;
      }
      save->letter = ptr->letter;
      if (rt_child) parent->right = ptr->left;
      else parent->left = ptr->left;
     }
     else {             /* Delete from right subtree.*/
      ptr = ptr->right;
      while (ptr->left != NULL) {
        lft_child = 1;
        parent = ptr;
        ptr = ptr->left;
      }
      save->letter = ptr->letter;
      if (lft_child) parent->left = ptr->right;
      else parent->right = ptr->right;
     }
   }
   free(ptr);
   return 1;         /* Indicates successful deletion */
  }
```

