#include <stdio.h>
#include <string.h>

#define MAX 5   // maximum apps allowed in background

char stack[MAX][30];
int top = -1;

// Push = open application
void push(char app[]) {
    if (top == MAX - 1) {
        printf("\n Too many applications running in background!\n");
        return;
    }
    top++;
    strcpy(stack[top], app);
    printf("Opened: %s\n", app);
}

// Pop = close application
void pop() {
    if (top == -1) {
        printf("\n No applications are running!\n");
        return;
    }
    printf("Closed: %s\n", stack[top]);
    top--;
}

// Mobile OFF = clear all apps
void mobileOff() {
    printf("\n Mobile turned OFF.\nClosing all applications...\n");
    while (top != -1) {
        printf("Closed: %s\n", stack[top]);
        top--;
    }
    printf("All apps cleared.\n");
}

// Mobile ON = open default app automatically
void mobileOn() {
    printf("\n Mobile turned ON.\n");
    push("Home Screen (In-built App)");
}

void showRunningApps() {
    if (top == -1) {
        printf("\nNo applications are running.\n");
        return;
    }
    printf("\nCurrently Running Apps:\n");
    for (int i = top; i >= 0; i--) {
        printf(" - %s\n", stack[i]);
    }
}

int main() {
    int choice;
    char app[30];

    while (1) {
        printf("\n==== Mobile Application Manager ====\n");
        printf("1. Open Application (Push)\n");
        printf("2. Close Latest Application (Pop)\n");
        printf("3. Show Running Applications\n");
        printf("4. Mobile Turn OFF\n");
        printf("5. Mobile Turn ON\n");
        printf("6. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {

        case 1:
            printf("Enter application name to open: ");
            scanf("%s", app);
            push(app);
            break;

        case 2:
            pop();
            break;

        case 3:
            showRunningApps();
            break;

        case 4:
            mobileOff();
            break;

        case 5:
            mobileOn();
            break;

        case 6:
            return 0;

        default:
            printf("Invalid choice!\n");
        }
    }
    return 0;
}
