# Result-management-system
My 1st trimester project practice

#include<stdio.h>
#include<string.h>
#include<stdlib.h>
struct students{
    char studentName[50];
    int Roll;
    char date[12];
    float ct;
    float mid;
    float finale;
    float assignment;
    float attendance;
    float totalmarks;
    float point;
    char grade[2];


}s;

FILE *fp;

int password = 1234;



int main(){
    int pass;
    printf("################################\n");
    printf("#                              #\n");
    printf("#     Enter your password:     #\n");
    printf("#                              #\n");
    printf("################################\n");


    printf("\nPassword: ");
    scanf("%d", &pass);
    if(pass==password){

        showmenu();
    }else{
        printf("Wrong password\n");
    }
    exit(0);

    return 0;
}

void showmenu(){
    int ch;

    while(1){
        system("cls");

        printf("##############################################\n");
        printf("#                                            #\n");
        printf("# ------->RESULT MANAGEMENT SYSTEM<--------- #\n");
        printf("#____________________________________________#\n");
        printf("#                                            #\n");
        printf("#                                            #\n");
        printf("#          Press 1 to add students           #\n");
        printf("#                                            #\n");
        printf("#        Press 2 to view students list       #\n");
        printf("#                                            #\n");
        printf("#          Press 3 to remove students        #\n");
        printf("#                                            #\n");
        printf("#               Press 0 to EXIT              #\n");
        printf("#                                            #\n");
        printf("##############################################\n");
        printf("\n");
        printf("Enter your choice: ");
        scanf("%d", &ch);


        switch(ch){
        case 0:
            exit(0);

        case 1:
            addstudent();
            break;

        case 2:
            studentList();
            break;

        case 3:
            del();
            break;

        default:
            printf("Invalid Choice...\n\n");

        }
        printf("Press Any Key To Continue...\n");
        getch();
    }
}


void addstudent(){
     system("cls");

     fp = fopen("students.txt", "ab");

     printf("Enter student Roll: ");
     fflush(stdin);
     scanf("%d", &s.Roll);

     printf("Enter student name: ");
     fflush(stdin);
     gets(s.studentName);

     printf("Enter student class test mark(out of 15): ");
     fflush(stdin);
     scanf("%f", &s.ct);

     printf("Enter student mid term mark(out of 30): ");
     fflush(stdin);
     scanf("%f", &s.mid);

     printf("Enter student final term mark(out of 40): ");
     fflush(stdin);
     scanf("%f", &s.finale);

     printf("Enter student assignment mark(out of 10): ");
     fflush(stdin);
     scanf("%f", &s.assignment);

     printf("Enter student attendance mark(out of 5): ");
     fflush(stdin);
     scanf("%f", &s.attendance);

     s.totalmarks = s.ct + s.mid + s.finale + s.assignment + s.attendance;

     if(s.totalmarks>=90 && s.totalmarks<=100){
        s.point = 4.00;
        strcpy(s.grade,"A");
     }else if(s.totalmarks>=86 && s.totalmarks<=89){
        s.point = 3.67;
        strcpy(s.grade,"A-");
     } else if(s.totalmarks>=82 && s.totalmarks<=85){
        s.point = 3.33;
        strcpy(s.grade,"B+");
     } else if(s.totalmarks>=78 && s.totalmarks<=81){
        s.point = 3.00;
        strcpy(s.grade,"B");
     } else if(s.totalmarks>=74 && s.totalmarks<=77){
        s.point = 2.67;
        strcpy(s.grade,"B-");
     } else if(s.totalmarks>=70 && s.totalmarks<=73){
        s.point = 2.33;
        strcpy(s.grade,"C+");
     } else if(s.totalmarks>=66 && s.totalmarks<=69){
        s.point = 2.00;
        strcpy(s.grade,"C");
     } else if(s.totalmarks>=62 && s.totalmarks<=65){
        s.point = 1.67;
        strcpy(s.grade,"C-");
     } else if(s.totalmarks>=58 && s.totalmarks<=61){
        s.point = 1.33;
        strcpy(s.grade,"D+");
     } else if(s.totalmarks>=55 && s.totalmarks<=57){
        s.point = 1.00;
        strcpy(s.grade,"D");
     } else if(s.totalmarks>=0 && s.totalmarks<=54){
        s.point = 0.00;
        strcpy(s.grade,"F");
     }
     /*
     if(s.totalmarks>=90 && s.totalmarks<=100){
        strcpy(s.grade,"A");
     }else if(s.totalmarks>=86 && s.totalmarks<=89){
        strcpy(s.grade,"A-");
     }else if(s.totalmarks>=78 && s.totalmarks<=81){
        strcpy(s.grade,"B+");
     }else if(s.totalmarks>=78 && s.totalmarks<=81){
        strcpy(s.grade,"B");
     }else if(s.totalmarks>=74 && s.totalmarks<=77){
        strcpy(s.grade,"B-");
     }else if(s.totalmarks>=70 && s.totalmarks<=73){
        strcpy(s.grade,"C+");
     }else if(s.totalmarks>=66 && s.totalmarks<=69){
        strcpy(s.grade,"C");
     }else if(s.totalmarks>=62 && s.totalmarks<=65){
        strcpy(s.grade,"C-");
     }else if(s.totalmarks>=58 && s.totalmarks<=61){
        strcpy(s.grade,"D+");
     }else if(s.totalmarks>=55 && s.totalmarks<=57){
        strcpy(s.grade,"D");
     }else if(s.totalmarks>=0 && s.totalmarks<=54){
        strcpy(s.grade,"F");
     }
     */

     printf("Student Added Successfully\n");

     fwrite(&s, sizeof(s),1,fp);
     fclose(fp);
}


void studentList() {
    system("cls");
    printf("<== students ==>\n\n");
    printf("%-10s %-20s %-10s %-10s %-15s %-15s %-10s %-15s %-10s %-10s \n\n", "Student", "Student Name", "Mid Term","Final","Attendance","Assignment", "CT", "Total marks", "point","Grade");

    fp = fopen("students.txt", "rb");
    if (fp == NULL) {
        printf("Error opening file.\n");
        return;
    }

    while (fread(&s, sizeof(s), 1, fp) == 1) {
        printf("%-10d %-20s %-10.2f %-10.2f %-15.2f %-15.2f %-10.2f %-15.2f %-10.2f %-10s \n", s.Roll, s.studentName, s.mid, s.finale, s.attendance, s.assignment, s.ct,s.totalmarks, s.point,s.grade);
    }

    fclose(fp);
}

void del(){
    int id, f=0;
    system("cls");
    printf("<== Remove student ==>\n\n");
    printf("Enter student roll to remove: ");
    scanf("%d", &id);

    FILE *ft;

    fp = fopen("students.txt", "rb");
    ft = fopen("temp.txt", "wb");

    while(fread(&s, sizeof(s), 1, fp) == 1){
        if(id == s.Roll){
            f=1;
        }else{
            fwrite(&s, sizeof(s), 1, ft);
        }
    }

    if(f==1){
        printf("\n\nDeleted Successfully.");
    }else{
        printf("\n\nRecord Not Found !");
    }

    fclose(fp);
    fclose(ft);

    remove("students.txt");
    rename("temp.txt", "students.txt");

}

