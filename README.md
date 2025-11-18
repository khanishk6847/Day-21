# Day-21
#include <stdio.h>
#include <stdlib.h>

void inputData(int id[], int sp[], int ln[], int n) {
    int i;
    for(i=0;i<n;i++) {
        scanf("%d", &id[i]);
        scanf("%d", &sp[i]);
        scanf("%d", &ln[i]);
    }
}

int countSpeedViolations(int sp[], int n) {
    int i, c=0;
    for(i=0;i<n;i++) {
        if(sp[i] > 80) c++;
    }
    return c;
}

int countLaneViolations(int id[], int ln[], int n) {
    int i, c=0;
    for(i=0;i<n;i++) {
        if(id[i] % 4 != ln[i]) c++;
    }
    return c;
}

int busiestLane(int ln[], int n) {
    int lc[4] = {0,0,0,0};
    int i, max=0, pos=0;
    for(i=0;i<n;i++) lc[ln[i]-1]++;
    for(i=0;i<4;i++) {
        if(lc[i] > max) {
            max = lc[i];
            pos = i;
        }
    }
    return pos+1;
}

int leastBusyLane(int ln[], int n) {
    int lc[4] = {0,0,0,0};
    int i, min=9999, pos=0;
    for(i=0;i<n;i++) lc[ln[i]-1]++;
    for(i=0;i<4;i++) {
        if(lc[i] < min) {
            min = lc[i];
            pos = i;
        }
    }
    return pos+1;
}

void displayReport(int id[], int sp[], int ln[], int n) {
    int i;
    printf("VehID\tSpeed\tLane\tSpeedV\tLaneV\n");
    for(i=0;i<n;i++) {
        int sv = (sp[i] > 80);
        int lv = (id[i] % 4 != ln[i]);
        printf("%d\t%d\t%d\t%d\t%d\n", id[i], sp[i], ln[i], sv, lv);
    }
}

int main() {
    int id[30], sp[30], ln[30];
    int n;
    
    scanf("%d", &n);
    
    inputData(id, sp, ln, n);
    
    int sv = countSpeedViolations(sp, n);
    int lv = countLaneViolations(id, ln, n);
    
    int b = busiestLane(ln, n);
    int l = leastBusyLane(ln, n);
    
    displayReport(id, sp, ln, n);
    
    printf("Speed Violations: %d\n", sv);
    printf("Lane Violations: %d\n", lv);
    printf("Busiest Lane: %d\n", b);
    printf("Least Busy Lane: %d\n", l);

    return 0;
}
