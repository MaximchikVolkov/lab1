# lab1
Exercise 1.1
#include <stdio.h>
int j=0;
void printPoint(int a, int b);
void comparison(int a, int b);
void scanPointX(int a);
void scanPointY(int a);
float checkX(float a, float b);
float checkY(float a, float b);
int main()
{
    float k, b;
    float x1=0, y1=0, x2=0, y2=0, x3=0, y3=0, Y=0;
    x1=checkX(1, x1);
    y1=checkY(1, y1);
    x2=checkX(2, x2);
    y2=checkY(2, y2);
    x3=checkX(3, x3);
    y3=checkY(3, y3);
    printPoint(x1, y1);
    printPoint(x2, y2);
    printPoint(x3, y3);
    if(x1==x2)
    {
         if(y1!=y2)
         {
            if(x3==x1)
                 printf("On the straight line\n");
            if(x3<x1)
                 printf("Lefter than straight line\n");
            if(x3>x1)
                 printf("Righter than straight line\n");
          }
          if(y1==y2)
                printf("Syntaxix Error, Please correct your data\n");
    }
    if(x1<x2)
    {
        k=((y2-y1)/(x2-x1));
        b=y1-k*x1;
        Y=k*x3+b;
        comparison(y3, Y);
    }
    if(x1>x2)
    {
        k=((y1-y2)/(x1-x2));
        b=y1-k*x1;
        Y=k*x3+b;
        comparison(y3, Y);
    }
    return 0;
}
void printPoint(int a, int b)
{
    j++;
    printf("Point %d: x: %d y: %d\n",j, a, b);
}
void scanPointX(int a)
{
    printf("Point %d X: ", a);
}
void scanPointY(int a)
{
    printf("Point %d Y: ", a);
}
void comparison(int a, int b)
{
    if(a>b)
        printf("Over the straight line\n");
    if(a<b)
        printf("Under the straight line\n");
    if(a==b)
        printf("On the straight line\n");
}
float checkX(float a, float b)
{
    float s;
    do
    {
        scanPointX(a);
        fflush(stdin);
        s = scanf("%g", &b);
    }
    while (s < 1);
    return b;
}
float checkY(float a, float b)
{
    float s;
    do
    {
        scanPointY(a);
        fflush(stdin);
        s = scanf("%g", &b);
    }
    while (s < 1);
    return b;
}





Exercise 1.2
#include <stdio.h>
void printPoint(int a, int b);
void scanPointX(int a);
void scanPointY(int a);
void printError();
void pointOnPoint(int a);
void sideAndContinantion(double Y, double y, double x, double x1, double x2);
void printSector(int a);
double checkX(double a, double b);
double checkY(double a, double b);
int j=0;
int main()
{
    double x1=0, y1=0, x2=0, y2=0, x3=0, y3=0, x4=0, y4=0, l, Y12, Y13, Y23, masX[15], masY[15];
    x1=checkX(1, x1);
    y1=checkY(1, y1);
    x2=checkX(2, x2);
    y2=checkY(2, y2);
    x3=checkX(3, x3);
    y3=checkY(3, y3);
    x4=checkX(4, x4);
    y4=checkY(4, y4);
    printPoint(x1, y1);
    printPoint(x2, y2);
    printPoint(x3, y3);
    printPoint(x4, y4);
    //Анализируем тот случай, когда построение треугольника невозможно
    if((x1==x2 && y1==y2) || (x2==x3 && y2==y3) || (x1==x3 && y1==y3) || (x1==x2 && x1==x3) || (y1==y2 && y2==y3))
        printError();
    else
    {
        //Учитываем тот случай, когда искомая точка может являться вершиной треугольника
        if(x1==x4 && y1==y4)
            pointOnPoint(1);
        if(x2==x4 && y2==y4)
            pointOnPoint(2);
        if(x3==x4 && y3==y4)
            pointOnPoint(3);
        /*Рассматриваем разные вариации расположения всех вершин относительно друг друга
        и приводим все к тому, что справа налево вершины пронумерованы в порядке возрастания*/
        masX[0]=x1;
        masX[1]=x2;
        masX[2]=x3;
        masY[0]=y1;
        masY[1]=y2;
        masY[2]=y3;
        for(int i=0; i<3; i++)
        {
            for(int j=0; j<3; j++)
            {
                if(masX[i]>masX[j])
                {
                    l=masX[i];
                    masX[i]=masX[j];
                    masX[j]=l;
                    l=masY[i];
                    masY[i]=masY[j];
                    masY[j]=l;
                }
            }
        }
        x1=masX[0];
        x2=masX[1];
        x3=masX[2];
        y1=masY[0];
        y2=masY[1];
        y3=masY[2];
        if(x2==x3 && x1<x2)
        {
            if(y2>y3)
            {
                l=x2;
                x2=x1;
                x1=l;
                l=y2;
                y2=y1;
                y1=l;
            }
            if(y2<y3)
            {
                l=x2;
                x2=x1;
                x1=l;
                l=y3;
                y3=y1;
                y1=l;
            }
        }
        if(x2==x3 && x1>x2)
        {
            if(y2>y3)
            {
                l=x2;
                x2=x3;
                x3=l;
                l=y2;
                y2=y3;
                y3=l;
            }
        }
        if(x1==x2 && x3>x1)
        {
            if(y1>y2)
            {
                l=x1;
                x1=x3;
                x3=l;
                l=y1;
                y1=y3;
                y3=l;
            }
            if(y1<y2)
            {
                l=x3;
                x3=x1;
                x1=l;
                l=y3;
                y3=y2;
                y2=y1;
                y1=l;
            }
        }
        if(x1==x2 && x3<x1)
        {
            if(y2>y1)
            {
                l=y1;
                y1=y2;
                y2=l;
            }
        }
        if(x1==x3 && x2<x1)
        {
            if(y1>y3)
            {
                l=x2;
                x2=x3;
                x3=l;
                l=y2;
                y2=y3;
                y3=l;
            }
            if(y1<y3)
            {
                l=x3;
                x3=x2;
                x2=l;
                l=y3;
                y3=y2;
                y2=y1;
                y1=l;
            }
        }
        if(x1==x3 && x2>x1)
        {
            if(y1>y3)
            {
                l=x2;
                x2=x1;
                x1=l;
                l=y2;
                y2=y3;
                y3=y1;
                y1=l;
            }
            if(y1<y3)
            {
                l=x1;
                x1=x2;
                x2=l;
                l=y1;
                y1=y2;
                y2=l;
            }
        }
        Y12=((y1-y2)/(x1-x2)*(x4-x1)+y1);
        Y13=((y1-y3)/(x1-x3)*(x4-x3)+y3);
        Y23=((y2-y3)/(x2-x3)*(x4-x2)+y2);
        if(Y12==Y23 && Y23==Y13 && Y12==Y23)
            printError();
        else
        {
            sideAndContinantion(Y12, y4, x4, x1, x2);
            sideAndContinantion(Y23, y4, x4, x2, x3);
            sideAndContinantion(Y13, y4, x4, x1, x3);
            if(y2>y1 && y2>y3)
            {
                if(y4>Y12 && y4<Y13 && y4<Y23)
                   printSector(1);
                if(y4<Y12 && y4<Y13 && y4<Y23)
                   printSector(2);
                if(y4<Y12 && y4<Y13 && y4>Y23)
                   printSector(3);
                if(y4<Y12 && y4>Y13 && y4>Y23)
                   printSector(4);
                if(y4>Y12 && y4>Y13 && y4>Y23)
                   printSector(5);
                if(y4>Y12 && y4>Y13 && y4<Y23)
                   printSector(6);
                if(y4<Y12 && y4>Y13 && y4<Y23)
                   printSector(7);
            }
            else
            {
                if(y4<Y12 && y4>Y13 && y4>Y23)
                   printSector(1);
                if(y4<Y12 && y4<Y13 && y4>Y23)
                   printSector(2);
                if(y4<Y12 && y4<Y13 && y4<Y23)
                   printSector(3);
                if(y4>Y12 && y4<Y13 && y4<Y23)
                   printSector(4);
                if(y4>Y12 && y4>Y13 && y4<Y23)
                   printSector(5);
                if(y4>Y12 && y4>Y13 && y4>Y23)
                   printSector(6);
                if(y4>Y12 && y4<Y13 && y4>Y23)
                   printSector(7);
            }
        }
    }
    return 0;
}
void printPoint(int a, int b)
{
    j++;
    printf("Point %d: x: %d y: %d\n", j, a, b);
}
void scanPointX(int a)
{
    printf("Point %d X: ", a);
}
void scanPointY(int a)
{
    printf("Point %d Y: ", a);
}
void pointOnPoint(int a)
{
    printf("Point 4 on Point %d\n", a);
}
void sideAndContinantion(double Y, double y, double x, double x1, double x2)
{
    if(Y==y)
    {
        if(x2<x && x<x1)
            printf("Point 4 is located on the side of the triangle\n");
        if(x<x2 || x>x1)
            printf("Point 4 is located on the continuation of the side of the triangle\n");
    }
}
void printError()
{
    printf("Error System, Please correct your data\n");
}
void printSector(int a)
{
    printf("Point is located in %d sector", a);
}
double checkX(double a, double b)
{
    double s;
    do
    {
        scanPointX(a);
        fflush(stdin);
        s = scanf("%lf", &b);
    }
    while (s < 1);
    return b;
}
double checkY(double a, double b)
{
    double s;
    do
    {
        scanPointY(a);
        fflush(stdin);
        s = scanf("%lf", &b);
    }
    while (s < 1);
    return b;
}
