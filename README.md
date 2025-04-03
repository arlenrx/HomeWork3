#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

struct Candidate {
    char name[100];
    char dob[11];
    char gender;
    char email[100];
    char nationality[50];
    float bmi;
    char primarySkill[50];
    char secondarySkill[50];
    int koreanProficiency;
    char mbti[5];
    char introduction[200];
};

void calculateAge(const char *dob) {
    struct tm birthDate = {0};
    time_t currentTime;
    struct tm currentDate;
    
    sscanf(dob, "%4d/%2d/%2d", &birthDate.tm_year, &birthDate.tm_mon, &birthDate.tm_mday);
    birthDate.tm_year -= 1900;
    birthDate.tm_mon -= 1;
    
    time(&currentTime);
    currentDate = *localtime(&currentTime);
    
    int age = currentDate.tm_year - birthDate.tm_year;
    if (currentDate.tm_mon < birthDate.tm_mon || (currentDate.tm_mon == birthDate.tm_mon && currentDate.tm_mday < birthDate.tm_mday)) {
        age--;
    }

    printf("%d", age);
}

int main() {
    struct Candidate candidates[6];
    char groupName[50];
    int i;

    printf("Enter the audition group name: ");
    fgets(groupName, sizeof(groupName), stdin);
    groupName[strcspn(groupName, "\n")] = '\0';

    for (i = 0; i < 6; i++) {
        printf("\n####################################\n");
        printf("[%s] Audition Candidate Data Entry\n", groupName);
        printf("####################################\n");
        printf("Entering information for the %d candidate.\n", i + 1);
        printf("---------------------------------\n");
        
        printf("1. Name: ");
        fgets(candidates[i].name, sizeof(candidates[i].name), stdin);
        candidates[i].name[strcspn(candidates[i].name, "\n")] = '\0';

        printf("2. Date of Birth (YYYY/MM/DD format): ");
        fgets(candidates[i].dob, sizeof(candidates[i].dob), stdin);
        candidates[i].dob[strcspn(candidates[i].dob, "\n")] = '\0';

        printf("3. Gender (F for Female, M for Male): ");
        scanf(" %c", &candidates[i].gender);
        getchar();

        printf("4. Email: ");
        fgets(candidates[i].email, sizeof(candidates[i].email), stdin);
        candidates[i].email[strcspn(candidates[i].email, "\n")] = '\0';

        printf("5. Nationality: ");
        fgets(candidates[i].nationality, sizeof(candidates[i].nationality), stdin);
        candidates[i].nationality[strcspn(candidates[i].nationality, "\n")] = '\0';

        printf("6. BMI: ");
        scanf("%f", &candidates[i].bmi);
        getchar();

        printf("7. Primary Skill: ");
        fgets(candidates[i].primarySkill, sizeof(candidates[i].primarySkill), stdin);
        candidates[i].primarySkill[strcspn(candidates[i].primarySkill, "\n")] = '\0';

        printf("8. Secondary Skill: ");
        fgets(candidates[i].secondarySkill, sizeof(candidates[i].secondarySkill), stdin);
        candidates[i].secondarySkill[strcspn(candidates[i].secondarySkill, "\n")] = '\0';

        printf("9. Korean Proficiency Level (TOPIK): ");
        scanf("%d", &candidates[i].koreanProficiency);
        getchar();

        printf("10. MBTI: ");
        fgets(candidates[i].mbti, sizeof(candidates[i].mbti), stdin);
        candidates[i].mbti[strcspn(candidates[i].mbti, "\n")] = '\0';

        printf("11. Introduction: ");
        fgets(candidates[i].introduction, sizeof(candidates[i].introduction), stdin);
        candidates[i].introduction[strcspn(candidates[i].introduction, "\n")] = '\0';

        printf("=================================\n");
    }

    printf("\n####################################\n");
    printf("[%s] Audition Candidate Data Review\n", groupName);
    printf("####################################\n");
    printf("=============================================================================================\n");
    printf("Name          | DOB       | Gender | Email                 | Nationality | BMI  | Primary Skill | Secondary Skill | TOPIK | MBTI | \n");
    printf("=============================================================================================\n");

    for (i = 0; i < 6; i++) {
        printf("%-15s | %-9s | %-6c | %-20s | %-11s | %-4.1f | %-13s | %-15s | %-5d | %-4s |\n",
               candidates[i].name, candidates[i].dob, candidates[i].gender, candidates[i].email,
               candidates[i].nationality, candidates[i].bmi, candidates[i].primarySkill,
               candidates[i].secondarySkill, candidates[i].koreanProficiency, candidates[i].mbti);
        printf("---------------------------------------------------------------------------------------------\n");
        printf("%s\n", candidates[i].introduction);
        printf("---------------------------------------------------------------------------------------------\n");
    }

    return 0;
}
