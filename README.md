<center>
  <h1>The student manage system</h1>
</center>
<p>
  上传到github上是为了学习一下git的使用方法
  本人学艺不精代码有问题还请多多见谅
</p>

下面是源代码：
```c
/*
1、录入学生成绩信息 方法名：void in();
2、查找学生成绩信息 方法名：void search();
3、删除学生成绩信息 方法名：void del();
4、修改学生成绩信息 方法名：void modify();
5、插入学生成绩信息 方法名：void insert();
6、按总分排序并保存到文件中 方法名：void order();
7、查询学生总人数 方法名：void searchNum();
请从上述功能中，选择5种功能进行实现，重要代码部分需要写注释。可参考给出的方法名进行功能实现，也可自定义方法名称。
学生类的结构体定义如下：
*/

#include <stdio.h>
#include <stdlib.h>

// 定义结构体储存学生信息
struct student
{
    int num;       /*学号*/
    char name[15]; /*姓名*/
    double elec;   /*选修课*/
    double expe;   /*实验课*/
    double requ;   /*必修课*/
    double sum;    /*总分*/
} stu[100];        // 定义结构体数组

// 定义全局变量
int n = 0; /*学生人数*/

// 录入学生成绩信息
// 把录入的成绩存到结构体数组中
void in()
{
    printf("输入学生人数:");
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        printf("请输入第%d个学生的学号：", i + 1);
        scanf("%d", &stu[i].num); // 读取学生的学号
        printf("请输入学生的姓名：");
        scanf("%s", stu[i].name); // 读取学生的姓名
        printf("请输入学生的选修课成绩：");
        scanf("%lf", &stu[i].elec); // 读取学生的选修课成绩
        printf("请输入学生的实验课成绩：");
        scanf("%lf", &stu[i].expe); // 读取学生的实验课成绩
        printf("请输入学生的必修课成绩：");
        scanf("%lf", &stu[i].requ);                           // 读取学生的必修课成绩
        stu[i].sum = stu[i].elec + stu[i].expe + stu[i].requ; // 计算总分
    }
}

// 查找学生成绩信息
void search()
{
    int xuehao; // 用于接收用户输入的学号
    printf("请输入要查找的学生的学号：");
    scanf("%d", &xuehao);
    for (int i = 0; i < n; i++) // 遍历结构体数组
    {
        if (stu[i].num == xuehao) // 找到对应的学号，如果学号相同则输出该学生的信息
        {
            // 输出学生信息
            printf("学号：%d\n", stu[i].num);
            printf("姓名：%s\n", stu[i].name);
            printf("选修课成绩：%.2lf\n", stu[i].elec);
            printf("实验课成绩：%.2lf\n", stu[i].expe);
            printf("必修课成绩：%.2lf\n", stu[i].requ);
            printf("总分：%.2lf\n", stu[i].sum);
            return;
        }
    }
    printf("没有找到该学生的信息\n");
}

// 删除学生成绩信息

void del()
{
    int xuehao; // 用于接收用户输入的学号
    printf("请输入要删除的学生的学号：");
    scanf("%d", &xuehao);
    // 遍历结构体数组找到要删除的学生的学号
    for (int i = 0; i < n; i++)
    {
        // 找到对应的学号
        if (stu[i].num == xuehao)
        {
            // 把后面的学生信息往前移动，覆盖掉要删除的学生信息
            for (int j = i; j < n; j++)
            {
                // 把后面一项的信息覆盖前面一项的信息
                stu[j] = stu[j + 1];
            }
            n--; // 再一次初始化学生人数
            printf("删除成功\n");
            return;
        }
    }
}

// 修改学生成绩信息
void modify()
{
    int xuehao;
    printf("请输入要修改的学生的学号：");
    scanf("%d", &xuehao);
    for (int i = 0; i < n; i++)
    {
        // 找到对应的学号
        // 重新录入学生的成绩
        if (stu[i].num == xuehao)
        {
            printf("请输入学生的选修课成绩：");
            scanf("%lf", &stu[i].elec); // 读取学生的选修课成绩
            printf("请输入学生的实验课成绩：");
            scanf("%lf", &stu[i].expe); // 读取学生的实验课成绩
            printf("请输入学生的必修课成绩：");
            scanf("%lf", &stu[i].requ);                           // 读取学生的必修课成绩
            stu[i].sum = stu[i].elec + stu[i].expe + stu[i].requ; // 计算总分数
            printf("修改成功\n");
            return;
        }
    }
}

// 插入学生成绩信息
void insert()
{
    // 在数组的最后一项插入学生信息
    printf("请输入第%d个学生的学号：", n + 1);
    scanf("%d", &stu[n].num); // 读取学生的学号
    printf("请输入学生的姓名：");
    scanf("%s", stu[n].name); // 读取学生的姓名
    printf("请输入学生的选修课成绩：");
    scanf("%lf", &stu[n].elec); // 读取学生的选修课成绩
    printf("请输入学生的实验课成绩：");
    scanf("%lf", &stu[n].expe); // 读取学生的实验课成绩
    printf("请输入学生的必修课成绩：");
    scanf("%lf", &stu[n].requ);                           // 读取学生的必修课成绩
    stu[n].sum = stu[n].elec + stu[n].expe + stu[n].requ; // 计算总分
    n++;                                                  // 再一次初始化学生人数
    printf("插入成功\n");
}

// 按总分排序并保存到文件中
void order()
{

    for (int i = 0; i <= n; i++)
    {
        // 遍历结构体数组，默认第一个为最大的，向后对比
        // 遇到后面比前面大的就交换
        if (stu[i].sum < stu[i + 1].sum)
        {
            // 定义个临时变量来存储交换的数据
            struct student tamp = stu[i];
            stu[i] = stu[i + 1];
            stu[i + 1] = tamp;
        }
    }

    // 把排序好的学生信息保存到文件中
    /*
    FILE是一个结构体，定义在stdio.h中，用于文件的读写操作
    FILE *fp; // 定义一个文件指针
    把指针指向文件
    fopen是一个函数用于打开文件
    fopen("文件名", "打开方式");
    w代表写入，如果文件不存在就创建一个文件
     */
    FILE *fp = fopen("student.txt", "w");
    for (int i = 0; i < n; i++)
    {
        // 把学生信息写入文件中
        fprintf(fp, "学号：%d\n", stu[i].num);
        fprintf(fp, "姓名：%s\n", stu[i].name);
        fprintf(fp, "选修课成绩：%.2lf\n", stu[i].elec);
        fprintf(fp, "实验课成绩：%.2lf\n", stu[i].expe);
        fprintf(fp, "必修课成绩：%.2lf\n", stu[i].requ);
        fprintf(fp, "总分：%.2lf\n", stu[i].sum);
    }
}

// 查询学生总人数
void searchNum()
{
    printf("学生总人数为：%d\n", n);
}

int main()
{
    int xuanze; // 用于接收用户输入的数字
    // 死循环监听用户
    while (1)
    {
        printf("**********************************\n");
        printf("欢迎使用学生管理系统\n");
        printf("1、录入学生成绩信息\n");
        printf("2、查找学生成绩信息\n");
        printf("3、删除学生成绩信息\n");
        printf("4、修改学生成绩信息\n");
        printf("5、插入学生成绩信息\n");
        printf("6、按总分排序并保存到文件中\n");
        printf("7、查询学生总人数\n");
        printf("8、退出\n");
        printf("**********************************\n");
        printf("请输入你的选择：");
        scanf("%d", &xuanze);
        switch (xuanze)
        {
        case 1:
            // 录入学生成绩
            in();
            break;
        case 2:
            // 查找学生成绩
            search();
            break;
        case 3:
            // 删除学生成绩
            del();
            break;
        case 4:
            // 修改学生成绩
            modify();
            break;
        case 5:
            // 插入学生成绩
            insert();
            break;
        case 6:
            // 按总分排序并保存到文件中
            order();
        //     break;
        case 7:
            // 查询学生总人数
            searchNum();
            break;
        case 8:
            // 退出
            exit(0);
        }
    }

    return 0;
}
