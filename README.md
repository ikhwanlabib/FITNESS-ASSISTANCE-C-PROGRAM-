#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>
#include <windows.h>
#include <conio.h>

typedef struct User {
    int height;             // Height in cm
    int age;                // Age in years
    float weight;           // Current weight in kg
    float target_weight;    // Target weight in kg
    int training_days;      // Training days per week
} User;

void showWorkoutOptions();
void showEquipmentOptions(int workoutType);
void workoutPlan(User user, int workoutType, int selectedEquipment[], int equipmentCount);
const char* equipmentName(int workoutType, int equipmentNumber);
void printSlowly(char* Text);

void showWorkoutOptions() {
    printSlowly("Choose your workout type:\n");
    printSlowly("1. Cardio\n");
    printSlowly("2. Strength\n");
    printSlowly("3. Functional and Flexibility\n");
    printSlowly("4. Basic Calisthenics\n");
}

void showEquipmentOptions(int workoutType) {
    switch (workoutType) {
        case 1:
            printSlowly("Cardio Equipment:\n");
            printSlowly("1. Treadmill\n");
            printSlowly("2. Elliptical Trainer\n");
            printSlowly("3. Stationary Bike\n");
            printSlowly("4. Rowing Machine\n");
            printSlowly("5. Stair Climber\n");
            printSlowly("6. Spin Bike\n\n");
            break;
        case 2:
            printSlowly("Strength Equipment:\n");
            printSlowly("1. Dumbbells\n");
            printSlowly("2. Barbells and Plates\n");
            printSlowly("3. Bench Press\n");
            printSlowly("4. Squat Rack\n");
            printSlowly("5. Cable Machine\n");
            printSlowly("6. Leg Press Machine\n");
            printSlowly("7. Smith Machine\n");
            printSlowly("8. Kettlebells\n\n");
            break;
        case 3:
            printSlowly("Functional & Flexibility Equipment:\n");
            printSlowly("1. Medicine Ball\n");
            printSlowly("2. Stability Ball\n");
            printSlowly("3. Resistance Band\n");
            printSlowly("4. Foam Roller\n");
            printSlowly("5. Yoga Mat\n\n");
            break;
        case 4:
            printSlowly("Basic Calisthenics Equipment:\n");
            printSlowly("1. Pull-Up Bar\n");
            printSlowly("2. Parallel Bar\n");
            printSlowly("3. Push-Up Bar\n");
            printSlowly("4. Dip Station\n");
            printSlowly("5. Jump Box\n");
            printSlowly("6. Gymnastic Rings\n\n");
            break;
        default:
            printSlowly("Unknown workout type.\n");
    }
}

void workoutPlan(User user, int workoutType, int selectedEquipment[], int equipmentCount) {
    printf("Your Weekly Workout Plan:\n\n");
    int Duration, totalDuration = 0, i, j;

    for (i = 0; i < user.training_days; i++) {
        Sleep(1000);

        printf("\nDay %d\n", i + 1);
        for (j = 0; j < equipmentCount; j++) {
            Duration = (rand() % 6 + 1) * 5;
            printf("   %c %-20s - %2d minutes\n", 175, equipmentName(workoutType, selectedEquipment[j]), Duration);
            totalDuration += Duration;
        }
    }

    float caloriesPerMinute = 8.0;
    float totalCalories = caloriesPerMinute * totalDuration * user.training_days;
    printf("\n\nEstimated Total Calories Burned in a Week: %.2f calories\n", totalCalories);
    printf("~~~~~~~~~~~~~~ KEEP IT UP & THANK YOU! ~~~~~~~~~~~~~~");
}

const char* equipmentName(int workoutType, int equipmentNumber) {
    switch (workoutType) {
        case 1: // Cardio
            switch (equipmentNumber) {
                case 1: return "Treadmill";
                case 2: return "Elliptical Trainer";
                case 3: return "Stationary Bike";
                case 4: return "Rowing Machine";
                case 5: return "Stair Climber";
                case 6: return "Spin Bike";
                default: return "Unknown equipment";
            }
        case 2: // Strength
            switch (equipmentNumber) {
                case 1: return "Dumbbells";
                case 2: return "Barbells & Plates";
                case 3: return "Bench Press";
                case 4: return "Squat Rack";
                case 5: return "Cable Machine";
                case 6: return "Leg Press Machine";
                case 7: return "Smith Machine";
                case 8: return "Kettlebells";
                default: return "Unknown equipment";
            }
        case 3: // Functional and Flexibility
            switch (equipmentNumber) {
                case 1: return "Medicine Ball";
                case 2: return "Stability Ball";
                case 3: return "Resistance Band";
                case 4: return "Foam Roller";
                case 5: return "Yoga Mat";
                default: return "Unknown equipment";
            }
        case 4: // Calisthenics
            switch (equipmentNumber) {
                case 1: return "Pull-Up Bar";
                case 2: return "Parallel Bar";
                case 3: return "Push-Up Bar";
                case 4: return "Dip Station";
                case 5: return "Jump Box";
                case 6: return "Gymnastic Rings";
                default: return "Unknown equipment";
            }
        default:
            return "Unknown workout type";
    }
}

void printSlowly(char* Text) {
    int i;
    for (i = 0; i < strlen(Text); i++) {
        printf("%c", Text[i]);
        Sleep(10);
    }
}

int main() {
    User user;
    int workoutType, equipmentCount, maxEquipment, i;
    char Text[200];

    srand(time(0));

    printSlowly("~~~~~~ WELCOME TO FITHELPER PROGRAM ~~~~~~\n\n");

    sprintf(Text, "%c Enter your height (cm): ", 175);
    printSlowly(Text);
    scanf("%d", &user.height);

    sprintf(Text, "%c Enter your age (years): ", 175);
    printSlowly(Text);
    scanf("%d", &user.age);

    sprintf(Text, "%c Current weight (kg): ", 175);
    printSlowly(Text);
    scanf("%f", &user.weight);

    sprintf(Text, "%c Target weight (kg): ", 175);
    printSlowly(Text);
    scanf("%f", &user.target_weight);

    sprintf(Text, "\n%c How many days per week do you want to train (1-7): ", 175);
    do {
        printSlowly(Text);
        scanf("%d", &user.training_days);
    } while (user.training_days < 0 || user.training_days > 7);

    do {
        system("cls");
        showWorkoutOptions();
        sprintf(Text, "\n%c ", 175);
        printSlowly(Text);
        scanf("%d", &workoutType);
    } while (workoutType < 0 || workoutType > 4);

    sprintf(Text, "%c Enter number of equipment you want to use: ", 175);
    do {
        system("cls");
        showEquipmentOptions(workoutType);
        printSlowly(Text);
        scanf("%d", &equipmentCount);
    } while (equipmentCount < 1);

    switch (workoutType) {
        case 1: maxEquipment = 6; break;
        case 2: maxEquipment = 8; break;
        case 3: maxEquipment = 5; break;
        case 4: maxEquipment = 6; break;
        default: maxEquipment = 1; break;
    }

    if (equipmentCount > maxEquipment)
        equipmentCount = maxEquipment;

    int *selectedEquipment = (int *)malloc(equipmentCount * sizeof(int));

    for (i = 0; i < equipmentCount; i++) {
        do {
            printf("%c ", 174);
            scanf("%d", &selectedEquipment[i]);
        } while (selectedEquipment[i] < 0 || selectedEquipment[i] > maxEquipment);
    }

    system("cls");
    workoutPlan(user, workoutType, selectedEquipment, equipmentCount);

    free(selectedEquipment);
    printSlowly("\n\n\n>> Press any key to exit...");
    getch();
    system("cls");

    return 0;
}
# FITNESS-ASSISTANCE-C-PROGRAM-
