#include <stdio.h>
#include <string.h>
#include <stdbool.h>
#define MAX_STUDENTS 10000
#define MAX_FACULTY 5000
#define MAX_COURSES 500
#define MAX_NAME_LENGTH 500
#define MAX_EMAIL_LENGTH 100
#define MAX_PASSWORD_LENGTH 20
typedef struct {
    char name[MAX_NAME_LENGTH];
    char email[MAX_EMAIL_LENGTH];
    char password[MAX_PASSWORD_LENGTH];
    char dob[11]; 
    int courses_enrolled[MAX_COURSES]; 
    int num_courses_enrolled;
} Student;
typedef struct {
    char name[MAX_NAME_LENGTH];
    char email[MAX_EMAIL_LENGTH];
    char password[MAX_PASSWORD_LENGTH];
} Faculty;
typedef struct {
    int course_code;
    char course_name[MAX_NAME_LENGTH];
    char faculty[MAX_NAME_LENGTH];
} Course;
Student students[MAX_STUDENTS];
Faculty faculty[MAX_FACULTY];
Course courses[MAX_COURSES];
int num_students = 0;
int num_faculty = 0;
int num_courses = 0;
void register_student() {
    if (num_students >= MAX_STUDENTS) {
        printf("Cannot register more students. Limit reached.\n");
        return;
    }
    printf("Enter name: ");
    scanf("%s", students[num_students].name);
    printf("Enter email: ");
    scanf("%s", students[num_students].email);
    printf("Enter password: ");
    scanf("%s", students[num_students].password);
    printf("Enter date of birth (YYYY-MM-DD): ");
    scanf("%s", students[num_students].dob);
    
    students[num_students].num_courses_enrolled = 0;
    num_students++;
    
    printf("Student registered successfully!\n");
}
void login_student() {
    char email[MAX_EMAIL_LENGTH];
    char password[MAX_PASSWORD_LENGTH];
    printf("Enter email: ");
    scanf("%s", email);
    printf("Enter password: ");
    scanf("%s", password);
    for (int i = 0; i < num_students; i++) {
        if (strcmp(students[i].email, email) == 0 && strcmp(students[i].password, password) == 0) {
            printf("Welcome back, %s!\n", students[i].name);
            return;
        }
    }
    printf("Invalid email or password.\n");
}
void register_faculty() {
    if (num_faculty >= MAX_FACULTY) {
        printf("Cannot register more faculty members. Limit reached.\n");
        return;
    }
    printf("Enter name: ");
    scanf("%s", faculty[num_faculty].name);
    printf("Enter email: ");
    scanf("%s", faculty[num_faculty].email);
    printf("Enter password: ");
    scanf("%s", faculty[num_faculty].password);
    num_faculty++;
    printf("Faculty registered successfully!\n");
}
void login_faculty() {
    char email[MAX_EMAIL_LENGTH];
    char password[MAX_PASSWORD_LENGTH];
    printf("Enter email: ");
    scanf("%s", email);
    printf("Enter password: ");
    scanf("%s", password);
    for (int i = 0; i < num_faculty; i++) {
        if (strcmp(faculty[i].email, email) == 0 && strcmp(faculty[i].password, password) == 0) {
            printf("Welcome back, %s!\n", faculty[i].name);
            return;
        }
    }
    printf("Invalid email or password.\n");
}
void add_course() {
    if (num_courses >= MAX_COURSES) {
        printf("Cannot add more courses. Limit reached.\n");
        return;
    }
    printf("Enter course code: ");
    scanf("%d", &courses[num_courses].course_code);
    printf("Enter course name: ");
    scanf("%s", courses[num_courses].course_name);
    printf("Enter faculty name: ");
    scanf("%s", courses[num_courses].faculty);
    num_courses++;
    printf("Course added successfully!\n");
}
int main() {
    int choice;
    do {
        printf("\nCollege Management System\n");
        printf("1. Register Student\n");
        printf("2. Login Student\n");
        printf("3. Register Faculty\n");
        printf("4. Login Faculty\n");
        printf("5. Add Course\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        
        switch(choice) {
            case 1:
                register_student();
                break;
            case 2:
                login_student();
                break;
            case 3:
                register_faculty();
                break;
            case 4:
                login_faculty();
                break;
            case 5:
                add_course();
                break;
            case 6:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while(choice != 6);

    return 0;
}
