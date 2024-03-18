# 7thDevelop a menu driven Program in C for the following operations on Singly Linked List (SLL) of
Student Data with the fields: USN, Name, Programme, Sem, PhNo
a. Create a SLL of N Students Data by using front insertion.
b. Display the status of SLL and count the number of nodes in it
c. Perform Insertion / Deletion at End of SLL
d. Perform Insertion / Deletion at Front of SLL(Demonstration of stack)
e. Exit


#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to represent student data
struct Student {
    char USN[20];
    char Name[50];
    char Programme[50];
    int Sem;
    long long int PhNo;
    struct Student *next;
};

// Function prototypes
struct Student* createNode();
void frontInsert(struct Student **head);
void displayList(struct Student *head);
int countNodes(struct Student *head);
void endInsert(struct Student **head);
void frontDelete(struct Student **head);
void endDelete(struct Student **head);

int main() {
    struct Student *head = NULL;
    char choice;

    do {
        printf("\nSingly Linked List Operations Menu:\n");
        printf("a. Create a SLL of N Students Data by using front insertion\n");
        printf("b. Display the status of SLL and count the number of nodes in it\n");
        printf("c. Perform Insertion at End of SLL\n");
        printf("d. Perform Deletion at Front of SLL (Demonstration of stack)\n");
        printf("e. Exit\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);

        switch (choice) {
            case 'a':
                frontInsert(&head);
                break;

            case 'b':
                displayList(head);
                printf("Number of nodes: %d\n", countNodes(head));
                break;

            case 'c':
                endInsert(&head);
                break;

            case 'd':
                frontDelete(&head);
                break;

            case 'e':
                printf("Exiting program.\n");
                break;

            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    } while (choice != 'e');

    // Free memory allocated for nodes before exiting
    struct Student *temp;
    while (head != NULL) {
        temp = head;
        head = head->next;
        free(temp);
    }

    return 0;
}

// Function to create a new node
struct Student* createNode() {
    struct Student *newNode = (struct Student*)malloc(sizeof(struct Student));
    if (newNode == NULL) {
        printf("Memory allocation failed.\n");
        exit(1);
    }
    newNode->next = NULL;
    return newNode;
}

// Function to insert a node at the front of the linked list
void frontInsert(struct Student **head) {
    struct Student *newNode = createNode();
    printf("Enter USN: ");
    scanf("%s", newNode->USN);
    printf("Enter Name: ");
    scanf(" %[^\n]", newNode->Name);
    printf("Enter Programme: ");
    scanf(" %[^\n]", newNode->Programme);
    printf("Enter Semester: ");
    scanf("%d", &newNode->Sem);
    printf("Enter Phone Number: ");
    scanf("%lld", &newNode->PhNo);

    newNode->next = *head;
    *head = newNode;

    printf("Student data inserted at the front of the list.\n");
}

// Function to display the linked list
void displayList(struct Student *head) {
    if (head == NULL) {
        printf("Singly Linked List is empty.\n");
        return;
    }

    struct Student *current = head;
    printf("Singly Linked List Status:\n");
    while (current != NULL) {
        printf("USN: %s, Name: %s, Programme: %s, Semester: %d, Phone Number: %lld\n", current->USN, current->Name, current->Programme, current->Sem, current->PhNo);
        current = current->next;
    }
}

// Function to count the number of nodes in the linked list
int countNodes(struct Student *head) {
    int count = 0;
    struct Student *current = head;
    while (current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}

// Function to insert a node at the end of the linked list
void endInsert(struct Student **head) {
    struct Student *newNode = createNode();
    printf("Enter USN: ");
    scanf("%s", newNode->USN);
    printf("Enter Name: ");
    scanf(" %[^\n]", newNode->Name);
    printf("Enter Programme: ");
    scanf(" %[^\n]", newNode->Programme);
    printf("Enter Semester: ");
    scanf("%d", &newNode->Sem);
    printf("Enter Phone Number: ");
    scanf("%lld", &newNode->PhNo);

    if (*head == NULL) {
        *head = newNode;
    } else {
        struct Student *current = *head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
    }

    printf("Student data inserted at the end of the list.\n");
}

// Function to delete a node from the front of the linked list
void frontDelete(struct Student **head) {
    if (*head == NULL) {
        printf("Singly Linked List is empty. Cannot delete.\n");
        return;
    }

    struct Student *temp = *head;
    *head = (*head)->next;
    printf("Deleted student data: USN: %s, Name: %s, Programme: %s, Semester: %d, Phone Number: %lld\n", temp->USN, temp->Name, temp->Programme, temp->Sem, temp->PhNo);
    free(temp);
}

// Function to delete a node from the end of the linked list
void endDelete(struct Student **head) {
    if (*head == NULL) {
        printf("Singly Linked List is empty. Cannot delete.\n");
        return;
    }

    if ((*head)->next == NULL) {
        printf("Deleted student data: USN: %s, Name: %s, Programme: %s, Semester: %d, Phone Number: %lld\n", (*head)->USN, (*head)->Name, (*head)->Programme, (*head)->Sem, (*head)->PhNo);
        free(*head);
        *head = NULL;
        return;
    }

    struct Student *current = *head;
    while (current->next->next != NULL) {
        current = current->next;
    }
    struct Student *temp = current->next;
    current->next = NULL;
    printf("Deleted student data: USN: %s, Name: %s, Programme: %s, Semester: %d, Phone Number: %lld\n", temp->USN, temp->Name, temp->Programme, temp->Sem, temp->PhNo);
    free(temp);
}
