#include <stdio.h>
#include <string.h>

#define MAX_SCHEDULE 100

typedef struct {
    char title[50];
    char date[20];
    char time[20];
    char description[200];
} Schedule;

Schedule schedules[MAX_SCHEDULE];
int count = 0;

// 일정 추가
void addSchedule() {
    if (count >= MAX_SCHEDULE) {
        printf("더 이상 일정을 추가할 수 없습니다.\n");
        return;
    }

    printf("제목 입력: ");
    scanf(" %[^\n]", schedules[count].title);

    printf("날짜 입력 (YYYY-MM-DD): ");
    scanf(" %[^\n]", schedules[count].date);

    printf("시간 입력 (HH:MM): ");
    scanf(" %[^\n]", schedules[count].time);

    printf("설명 입력: ");
    scanf(" %[^\n]", schedules[count].description);

    count++;
    printf("일정이 추가되었습니다.\n");
}

// 일정 조회
void viewSchedules() {
    if (count == 0) {
        printf("등록된 일정이 없습니다.\n");
        return;
    }

    for (int i = 0; i < count; i++) {
        printf("\n[%d]\n", i + 1);
        printf("제목: %s\n", schedules[i].title);
        printf("날짜: %s\n", schedules[i].date);
        printf("시간: %s\n", schedules[i].time);
        printf("설명: %s\n", schedules[i].description);
    }
}

// 일정 수정
void editSchedule() {
    int index;

    viewSchedules();
    if (count == 0) return;

    printf("\n수정할 일정 번호 입력: ");
    scanf("%d", &index);

    if (index < 1 || index > count) {
        printf("잘못된 번호입니다.\n");
        return;
    }

    index--;

    printf("새 제목: ");
    scanf(" %[^\n]", schedules[index].title);

    printf("새 날짜 (YYYY-MM-DD): ");
    scanf(" %[^\n]", schedules[index].date);

    printf("새 시간 (HH:MM): ");
    scanf(" %[^\n]", schedules[index].time);

    printf("새 설명: ");
    scanf(" %[^\n]", schedules[index].description);

    printf("일정이 수정되었습니다.\n");
}

// 일정 삭제
void deleteSchedule() {
    int index;

    viewSchedules();
    if (count == 0) return;

    printf("\n삭제할 일정 번호 입력: ");
    scanf("%d", &index);

    if (index < 1 || index > count) {
        printf("잘못된 번호입니다.\n");
        return;
    }

    index--;

    for (int i = index; i < count - 1; i++) {
        schedules[i] = schedules[i + 1];
    }

    count--;
    printf("일정이 삭제되었습니다.\n");
}

int main() {
    int choice;

    while (1) {
        printf("\n==== 일정 관리 프로그램 ====\n");
        printf("1. 일정 추가\n");
        printf("2. 일정 조회\n");
        printf("3. 일정 수정\n");
        printf("4. 일정 삭제\n");
        printf("5. 종료\n");
        printf("선택: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addSchedule();
                break;
            case 2:
                viewSchedules();
                break;
            case 3:
                editSchedule();
                break;
            case 4:
                deleteSchedule();
                break;
            case 5:
                printf("프로그램 종료\n");
                return 0;
            default:
                printf("잘못된 선택입니다.\n");
        }
    }
}
