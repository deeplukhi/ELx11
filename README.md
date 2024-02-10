#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define a structure to represent a book
struct Book {
    char title[100];
    char author[100];
    int availableCopies;
};

// Function to add a new book to the library
void addBook(struct Book library[], int *totalBooks) {
    printf("Enter book title: ");
    scanf(" %[^\n]s", library[*totalBooks].title); // Read until newline
    printf("Enter author: ");
    scanf(" %[^\n]s", library[*totalBooks].author);
    printf("Enter available copies: ");
    scanf("%d", &library[*totalBooks].availableCopies);

    (*totalBooks)++; // Increment the total number of books
    printf("Book added successfully!\n");
}

// Function to display details of all books in the library
void displayBooks(struct Book library[], int totalBooks) {
    if (totalBooks == 0) {
        printf("No books in the library.\n");
        return;
    }

    printf("\nLibrary Books:\n");
    for (int i = 0; i < totalBooks; i++) {
        printf("Title: %s\n", library[i].title);
        printf("Author: %s\n", library[i].author);
        printf("Available Copies: %d\n", library[i].availableCopies);
        printf("------------------------\n");
    }
}

// Function to borrow a book
void borrowBook(struct Book library[], int totalBooks) {
    char searchTitle[100];
    printf("Enter the title of the book you want to borrow: ");
    scanf(" %[^\n]s", searchTitle);

    for (int i = 0; i < totalBooks; i++) {
        if (strcmp(searchTitle, library[i].title) == 0) {
            if (library[i].availableCopies > 0) {
                library[i].availableCopies--;
                printf("Book '%s' borrowed successfully!\n", library[i].title);
            } else {
                printf("Sorry, no available copies of '%s'.\n", library[i].title);
            }
            return;
        }
    }

    printf("Book not found in the library.\n");
}

// Function to return a borrowed book
void returnBook(struct Book library[], int totalBooks) {
    char searchTitle[100];
    printf("Enter the title of the book you want to return: ");
    scanf(" %[^\n]s", searchTitle);

    for (int i = 0; i < totalBooks; i++) {
        if (strcmp(searchTitle, library[i].title) == 0) {
            library[i].availableCopies++;
            printf("Book '%s' returned successfully!\n", library[i].title);
            return;
        }
    }

    printf("Book not found in the library.\n");
}

int main() {
    struct Book library[100]; // Assuming a maximum of 100 books in the library
    int totalBooks = 0;
    int choice;

    do {
        printf("\nLibrary Management System\n");
        printf("1. Add a book\n");
        printf("2. Display all books\n");
        printf("3. Borrow a book\n");
        printf("4. Return a book\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addBook(library, &totalBooks);
                break;
            case 2:
                displayBooks(library, totalBooks);
                break;
            case 3:
                borrowBook(library, totalBooks);
                break;
            case 4:
                returnBook(library, totalBooks);
                break;
            case 5:
                printf("Exiting Library Management System. Goodbye!\n");
                break;
            default:
                printf("Invalid choice. Please enter a valid option.\n");
        }
    } while (choice != 5);

    return 0;
}
