# BirthdayListProg
 have successfully completed task 1 of  C developer internship under Inter Crowd  Task 1: BirthdayListProgram.    IDE used - Visual studio code .I would like to thank Intern Crowd te group.


#include <stdio.h>
#include <string.h>

#define MAX_NAME_LENGTH 50
#define MAX_BIRTHDAYS 10

typedef struct {
    char name[MAX_NAME_LENGTH];
    int day;
    int month;
} Birthday;

// Function to add a birthday to the list
void addBirthday(Birthday* birthdays, int* numBirthdays) {
    if (*numBirthdays >= MAX_BIRTHDAYS) {
        printf("Maximum number of birthdays reached.\n");
        return;
    }

    Birthday newBirthday;
    printf("Enter name: ");
    scanf("%s", newBirthday.name);
    printf("Enter day: ");
    scanf("%d", &newBirthday.day);
    printf("Enter month: ");
    scanf("%d", &newBirthday.month);

    birthdays[*numBirthdays] = newBirthday;
    (*numBirthdays)++;

    printf("Birthday added successfully.\n");
}

// Function to edit a birthday in the list
void editBirthday(Birthday* birthdays, int numBirthdays) {
    char name[MAX_NAME_LENGTH];
    printf("Enter the name of the person to edit: ");
    scanf("%s", name);

    int found = 0;
    for (int i = 0; i < numBirthdays; i++) {
        if (strcmp(birthdays[i].name, name) == 0) {
            printf("Enter new day: ");
            scanf("%d", &birthdays[i].day);
            printf("Enter new month: ");
            scanf("%d", &birthdays[i].month);
            found = 1;
            printf("Birthday edited successfully.\n");
            break;
        }
    }

    if (!found) {
        printf("Birthday not found.\n");
    }
}

// Function to search for a birthday by name
void searchBirthday(Birthday* birthdays, int numBirthdays) {
    char name[MAX_NAME_LENGTH];
    printf("Enter the name to search: ");
    scanf("%s", name);

    int found = 0;
    for (int i = 0; i < numBirthdays; i++) {
        if (strcmp(birthdays[i].name, name) == 0) {
            printf("Birthday found: %s - %d/%d\n", birthdays[i].name, birthdays[i].day, birthdays[i].month);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Birthday not found.\n");
    }
}

// Function to display all birthdays
void displayBirthdays(Birthday* birthdays, int numBirthdays) {
    printf("Birthday List:\n");
    for (int i = 0; i < numBirthdays; i++) {
        printf("%s - %d/%d\n", birthdays[i].name, birthdays[i].day, birthdays[i].month);
    }
}

// Function to display birthdays in a specific month
void displayBirthdaysByMonth(Birthday* birthdays, int numBirthdays, int month) {
    printf("Birthdays in month %d:\n", month);
    int found = 0;
    for (int i = 0; i < numBirthdays; i++) {
        if (birthdays[i].month == month) {
            printf("%s - %d/%d\n", birthdays[i].name, birthdays[i].day, birthdays[i].month);
            found = 1;
        }
    }

    if (!found) {
        printf("No birthdays found in month %d.\n", month);
    }
}

int main() {
    Birthday birthdays[MAX_BIRTHDAYS];
    int numBirthdays = 0;

    int choice;

    do {
        printf("Menu:\n");
        printf("1. Add a birthday\n");
        printf("2. Edit a birthday\n");
        printf("3. Search for a birthday\n");
        printf("4. Display all birthdays\n");
        printf("5. View birthdays by month\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addBirthday(birthdays, &numBirthdays);
                break;
            case 2:
                editBirthday(birthdays, numBirthdays);
                break;
            case 3:
                searchBirthday(birthdays, numBirthdays);
                break;
            case 4:
                displayBirthdays(birthdays, numBirthdays);
                break;
            case 5:
                {
                    int month;
                    printf("Enter the month to view birthdays: ");
                    scanf("%d", &month);
                    displayBirthdaysByMonth(birthdays, numBirthdays, month);
                    break;
                }
            case 6:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice.\n");
                break;
        }

        printf("\n");
    } while (choice != 6);

    return 0;
}
