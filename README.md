# C-
课设
#include <stdio.h>
#include <windows.h>
#include <stdlib.h>
#define N 100
int i=0;
	struct wage//教师工资信息 
	{
		int month;
		int salary;
		int allowance;
		int depuct;
	};
	struct teacherdata//教师基本信息 
	{
		char name[20];
		char number[20];
		char academy[20];
		char profession[20];
		struct wage sal;
	}tea[N];
void yan(char *c);//延时输出字符串 
void save1();//保存基本信息
void save2();//保存工资信息
void input();//输入信息 
void input1();//输入基本信息 
void input2();//输入工资信息 
void change();//修改或删除信息 
void change2();//根据工号或姓名修改数据
void deletedata();//删除教师信息
void output1();//显示教师基本信息 
void output2();//根据月份显示教师工资信息 
void output3();//根据工号姓名输出
void output4();//输出所有教师的基本信息和工资信息 
void search();//查询信息 
void putsch();//某月份不同学院所有教师工资信息
void putpro();//某月份不同职称所有教师工资信息 
void introduction()
{
	system("cls");
	printf("\n\n");
	printf("\t**本系统用于保存和查询教师基本信息和工资信息,以下是使用系统时应注意的问题**\n\n");
	printf("\t\t1.未录入教师数据信息前，查询，修改，删除或分析等操作都是无效的！！\n\n");
	 printf("\t\t2.录入信息时必须先录入基本信息才能录入工资信息!!!\n\n");
	 system("pause");
}
void save1(struct teacherdata*c)//保存教师基本信息 
{
	FILE *fp;
	if((fp=fopen("salary","rb+"))==NULL)
	{
		printf("无法打开");
		exit(0); 
	}
	if(fwrite(c,sizeof(struct teacherdata),1,fp)==1){
		printf("录入成功！！\n\n");
	}
	else 
		printf("录入失败！！\n\n");
		fclose(fp); 
	}
void save2(struct wage*c)//保存教师工资信息 
	{
		FILE *fp;
		if((fp=fopen("salary","rb+"))==0)
		{


			printf("文件无法打开\n");
			exit(0); 
		}
		if(fwrite(c,sizeof(struct wage),1,fp)==1)
			puts("输入成功！！！\n");
		else puts("输入失败\n");
		fclose(fp);
	}
void input()
{
	
do{
	system("cls");
	int i; 
	printf("1.录入教师的基本信息\n2.录入教师的工资信息\n3.返回上一级菜单\n请选择你的操作命令（数字）：");
	 scanf("%d",&i);
	 switch(i)
	 {
	 	case 1:input1();break;
	 	case 2: input2();break;
	 	case 3:return;break;
	 }
}while(i!=3);
}	

void input1()//输入教师基本信息 
{
	system("cls");
	FILE *fp;
	int a,flag;
	char num[20];
	if((fp=fopen("teacherdat","w"))==NULL)
	{
		printf("data error!!");
		exit(0);
	}
	printf("请输入教师工号");
	scanf("%s",num) ;
	for(a=0,flag=0;a<i;a++)
	{
		if(strcmp(num,tea[a].number)==0)
		flag=1;
	}
	if(flag==1)
	{
		printf("该教师信息已存在\n");
		system("pause");
			return;
	}	
	strcpy(tea[i].number,num); 
	printf("请输入教师姓名：\n");
	scanf("%s",&tea[i].name);
	printf("1.信息学院\n2.生命学院\n3.人文学院\n请选择教师所在学院(数字)：");
	scanf ("%d",&a);
	switch(a)
	{
		case 1:strcpy(tea[i].academy,"信息学院" );break;
		case 2:strcpy(tea[i].academy,"生命学院");break;
		case 3:strcpy(tea[i].academy,"人文学院");break;
		default:printf("重新输入！！"); break;
	}
	printf("1.教授\n2.副教授\n3.讲师\n4.助教\n请选择教师职称："); 
	scanf("%d",&a);
	switch(a)
	{
		case 1:strcpy(tea[i].profession,"教授");break;
		case 2:strcpy(tea[i].profession,"副教授");break;
		case 3:strcpy(tea[i].profession,"讲师");break;
		case 4:strcpy(tea[i].profession,"助教"); break;
		default:printf("重新输入！！");break; 
		 
		 
	}
	save1(&tea[i]);
	system("pause");
	i++;
}
	
void input2( )//输入教师工资信息 
{
	system("cls");
	FILE *fp;
	if((fp=fopen("teacherdat","w"))==NULL)
		printf("data error"); 
	char d[20];
	int num=0,flag=0,month=0;
	system("cls");
	printf("请输入要录入工资信息的教师工号：");
	scanf("%s",d);
	for(;num<=i;num++)
	{
		if(strcmp(tea[num].number,d)==0)
		{ 
			flag=1;
			break;
		} 
	}
	if(flag==0)
	{ 
		printf("该教师信息不存在！！\n");
		system("pause");
		return;
	} 
	while(month<1||month>12) 
	{
		printf("请输入该教师工资月份：");
		scanf("%d",&month);
		tea[num].sal.month=month;
	}
	printf("请输入该教师该月份基本工资：");
		scanf("%d",&tea[num].sal.salary);
	printf("请输入该月份业绩津贴：");
		scanf("%d",&tea[num].sal.allowance) ;
	printf("请输入该月份扣除费用：");
		scanf("%d",&tea[num].sal.depuct) ;
	save2(&tea[num].sal);
	system("pause");	 
	}
	
void deletedata()
{
	system("cls"); 
	int g,flag=0;
	char k[20],c;
	printf("请输入要删除教师信息的工号：");
	scanf("%s",k);
	for(g=0;g<i;g++)
		if(strcmp(tea[g].number,k)==0)
		{
			flag=1;
			break;
		}
			
	if(flag==0)
	{
		printf("该教师信息不存在！！\n\n");
		system("pause");
		return;
	}		
	printf("您确定删除该工号所有信息吗（y/n):"); 
		while(c!='n'&&c!='y')
		{
			//printf("输入错误！！请重新输入\n");
			//system("pause");
			scanf("%c",&c);
		}
	if(c=='n')
		return;
	else{
	for(;g<i;g++)
		tea[g]=tea[g+1];
		i--;
		printf("删除成功\n");
	}
	system("pause");
}
	
void change()
{
	system("cls");
	int w;
	printf("1.根据工号或姓名修改教师基本信息和工资信息\n2.删除某一工号教师信息\n3.返回上级菜单：\n");
	printf("请选择你的操作命令：") ;
	 scanf("%d",&w);
	 switch(w)
	 {
	 	case 1:change2();break;
	 	case 2:deletedata();break;
	 	case 3:;break;
	 	default :printf("指令错误！！重新输入");break; 
	 }	
}
void change2()//修改教师基本信息和工资信息 
{
	system("cls");
	int f,j,a,flag=0;
	char e[20],c;
	system("cls");
	printf("请输入教师的工号或姓名：");
	scanf("%s",e);
	for(f=0;f<i;f++)
	{
		if(strcmp(tea[f].number,e)==0||strcmp(tea[f].name,e)==0)
		{
			flag=1;
			break;
		}
	}
		
	if(flag==0)
	{
		printf("该教师信息不存在\n");
		system("pause");
		return;
	}
	printf("您确定要修改该教师的信息吗（y/n):");
	scanf("%c",&c);
	if(c!='n'&&c!='y')
	{
		scanf("%c",&c);
	}
	if(c=='n')
			return;
	else
	{
	printf("您要修改的是(数字)\n1.基本信息\n2.工资信息\n");
	scanf("%d",&j);
	switch(j)
	{
		case 1:{
				printf("请重新输入工号：");
					scanf("%s",tea[f].number);
				printf("请重新输入姓名：");
					scanf("%s",tea[f].name);
				printf("请重新选择学院：\n");
				printf("\t\t1.信息学院\n\t\t2.生命学院\n\t\t3.人文学院\n请选择教师所在学院(数字)：");
				scanf ("%d",&a);
				switch(a)
			{
				case 1:strcpy(tea[f].academy,"信息学院" );break;
				case 2:strcpy(tea[f].academy,"生命学院");break;
				case 3:strcpy(tea[f].academy,"人文学院");break;
				default :printf("重新输入！！"); break;
			}
			printf("请重新选择教师职称：\n");
			printf("\t\t1.教授\n\t\t2.副教授\n\t\t3.讲师\n\t\t4.助教\n\t\t请选择教师职称：");
			scanf("%d",&a);
			switch(a)
			{
				case 1:strcpy(tea[f].profession,"教授");break;
				case 2:strcpy(tea[f].profession,"副教授");break;
				case 3:strcpy(tea[f].profession,"讲师");break;
				case 4:strcpy(tea[f].profession,"助教"); break;
				default :printf("重新输入！！");break; 
			}
			save1(&tea[f]);
		};break;
		case 2:{
			printf("请重新输入工资月份：");
				scanf("%d",&tea[f].sal.month);
			printf("请重新输入基本工资：");
				scanf("%d",&tea[f].sal.salary);
			printf("请重新输入业绩津贴：");
				scanf("%d",&tea[f].sal.allowance);
			printf("请重新输入扣除工资：");
				scanf("%d",&tea[f].sal.depuct) ;
				save2(&tea[f].sal);
		};break;
		default:printf("指令错误！！重新输入");break;
		}
	}
	system("pause");
}
void output4()//输出所有教师的基本信息和工资信息 
{
	int t,flag=0;
	if(i==0)
	{
		printf("尚无数据存在！！！");
		system("pause");
		return; 
	}
	for(t=0;t<i;t++)
	{
	//	if(strcmp(tea[t].number,cc)==0 || strcmp(tea[t].name,cc)==0)
		{
			printf("工号\t姓名\t学院\t\t职称\t月份\t基本工资\t业绩津贴\t扣除工资\n");
			printf("%s\t%s\t%s\t%s\t%d\t\t%d\t\t%d\t\t%d\n",tea[t].number,tea[t].name,tea[t].academy,tea[t].profession,tea[t].sal.month,tea[t].sal.salary,tea[t].sal.allowance,tea[t].sal.depuct);
			
		} 
	}
	system("pause"); 
}
void output3()//输出所有教师基本信息 
{
	int t;
	if(i==0)
	{
		printf("尚无教师数据存在\n");
		system("pause");
		return;
	}
	printf("工号\t姓名\t学院\t职称\n");
	for(t=0;t<i;t++)
		printf("%s\t%s\t %s  %s\n",tea[t].number,tea[t].name,tea[t].academy,tea[t].profession);
		system("pause");
}

void output2()//输出该月份所有教师工资信息 
{
	system("cls");
	int t=0,j,f;
	printf("请输入要查找的月份：");
		scanf("%d",&f);
			for(j=0;j<i;j++)
			{
				if(tea[j].sal.month==f)
				{
					printf("工号\t\t姓名\t\t基本工资\t\t业绩津贴\t\t扣除工资\n");
					printf("%s\t\t%s\t\t%d\t\t%d\t\t%d\n",tea[j].number,tea[j].name,tea[j].sal.salary,tea[j].sal.allowance,tea[j].sal.depuct);
					t=1;
				}
			}
			if(t==0)
			{
				printf("无该月份信息！！！\n");
				system("pause");
			}
}
void output1()//按工号或姓名输出教师基本信息和工资信息 
{
	system("cls");
	int t=0,flag=0;
	char cc[20];
	printf("请输入教师工号或姓名：");
		scanf("%s",cc);
	for(t=0;t<i;t++)
	{
		if(strcmp(tea[t].number,cc)==0 || strcmp(tea[t].name,cc)==0)
		{
			printf("工号\t姓名\t学院\t职称\t月份\t基本工资\t业绩津贴\t扣除工资\n");
			printf("%s\t%s\t%s%s\t%d\t%d\t%d\t%d\n",tea[t].number,tea[t].name,tea[t].academy,tea[t].profession,tea[t].sal.month,tea[t].sal.salary,tea[t].sal.allowance,tea[t].sal.depuct);
			flag=1;
			break;
		} 
	}
		if(flag==0)
		{
			printf("该教师信息不存在\n");
			system("pause");
		}
			
	
} 
void search()
{
	system("cls");
	int j;
	printf("1.显示所有教师基本信息\n2.显示所有教师的基本信息和工资信息\n3.显示该月份所有教师工资信息\n4.根据工号或姓名查询教师某一个月份的基本信息和工资信息\n");
	printf("请选择你的操作命令：");
	scanf("%d",&j);
	switch(j)
	{
		case 1:output3();break;
		case 2:output4();break;
		case 3:output2();break;
		case 4:output1();break; 
		default:printf("输入错误\n"),system("pause");break; 
	}
}
void putsch()//根据月份查看不同学校平均工资 
{
	system("cls");
	int flag=0,s,x=0,sh=0,r=0,sum1=0,sum2=0,sum3=0,m;
	printf("请输入想查询的月份：");
		scanf("%d",&m);
	for(s=0;s<i;s++)
	{
		if(m==tea[s].sal.month)
			{
				if(strcmp(tea[s].academy,"信息学院")==0)
					{
						sum1+=(tea[s].sal.salary-tea[s].sal.depuct+tea[s].sal.allowance );
						x++;
					}
				if(strcmp(tea[s].academy,"生命学院")==0)
					{
						sum2+=(tea[s].sal.salary+tea[s].sal.allowance-tea[s].sal.depuct);
						sh++;
					}
				if(strcmp(tea[s].academy,"人文学院")==0)
					{
						sum3+=(tea[s].sal.salary+tea[s].sal.allowance-tea[s].sal.depuct);
						r++;
					}
					flag=1;
				}
	}
	if(flag==0)
	{
		printf("无该月份数据！！！\n");
		system("pause");
		return;
	}
	    if(x==0)
			printf("\t信息学院该月份平均实发工资为：%d\n\n",sum1);
		else  		
			printf("\t信息学院该月份平均实发工资为：%d\n\n",sum1/x);
		if(sh==0)
			printf("\t生命学院该月份平均实发工资为：%d\n\n",sum2);
		else
			printf("\t生命学院该月份平均是发工资为：%d\n\n",sum2/sh);
		if(r==0)
			printf("\t人文学院该月份平均实发工资为：%d\n\n",sum3);
		else
			printf("\t人文学院该月份平均实发工资为：%d\n\n",sum3/r);
	}
	
void putpro()//根据月份显示不同职称平均实发工资					 
{
	system("cls");
	int s,m,x=0,sh=0,r=0,z=0,sum1=0,sum2=0,sum3=0,sum4=0;
	int flag=0;
	printf("请输入要查询月份：");
		scanf("%d",&m);
		for(s=0;s<=i;s++)
	{
		if(m==tea[s].sal.month)
			{
				if(strcmp(tea[s].profession,"教授")==0)
				{
					sum1+=(tea[s].sal.salary-tea[s].sal.depuct+tea[s].sal.allowance );
					x++;
				}
				if(strcmp(tea[s].profession,"副教授")==0)
					{
						sum2+=(tea[s].sal.salary+tea[s].sal.allowance-tea[s].sal.depuct);
						sh++;
					}
				if(strcmp(tea[s].profession,"讲师")==0)
					{
					sum3+=(tea[s].sal.salary+tea[s].sal.allowance-tea[s].sal.depuct);
					r++;
					}
				if(strcmp(tea[s].profession,"助教")==0)
				{
					sum4+= (tea[s].sal.salary+tea[s].sal.allowance-tea[s].sal.depuct);
					z++;
				}
				flag=1;
			}
		} 
		if(flag==0)
		{
			printf("该月份数据不存在！！！");
			system("pause");
			return;
		}
		if(x==0)
			printf("\t教授该月份平均实发工资为：%d\n\n",sum1);
		else  		
			printf("\t教授该月份平均实发工资为：%d\n\n",sum1/x);
		if(sh==0)
			printf("\t副教授该月份平均实发工资为：%d\n\n",sum2);
		else
			printf("\t副教授该月份平均是发工资为：%d\n\n",sum2/sh);
		if(r==0)
			printf("\t讲师该月份平均实发工资为：%d\n\n",sum3);
		else
			printf("\t讲师该月份平均实发工资为：%d\n\n",sum3/r);
		if(z==0)
			printf("\t助教该月份平均实发工资为：%d\n\n",sum4);
		else 	\
			printf("\t助教该月份平均实发工资为：%d\n",sum4/z); 	
} 

void analyze()
{
	system("cls");
	int h;
	printf("1.根据月份查询不同学院教师平均应发工资和实发工资信息\n2.根据月份查询不同职称教师平均应发工资和实发工资信息\n3.返回上级菜单\n");
	printf("请选择你的操作命令：");
	scanf("%d",&h);
	switch(h)
	{
		case 1:putsch();break;
		case 2:putpro();break;
		case 3:;break; 
	}
}
	
void yan(char *c)//延时输出 
{
		while(1){
			if(*c!='\0')
			{
			printf("%c",*c);
			c++;	
			}
		else break;
		Sleep(10);}
}
 
 int main()//主函数 
 {
 	FILE *fp;
 	int t=0,a;
	 if((fp=fopen("salary","wb+")) ==NULL)
	 {
	 	printf("读取文件数据失败");
	 	system("cls");
	//	exit(0);
	 }
 while(fscanf(fp,"%s%s%s%s%d%d%d%d",tea[t].number,tea[t].name,tea[t].academy,tea[t].profession,&tea[t].sal.month,&tea[t].sal.salary,&tea[t].sal.allowance,&tea[t].sal.depuct)!=EOF)
 {
	 t++;
	 i++;
 }//从已有文件读取数据
    fclose(fp);
 	system("color 06") ;
 	char hua[]={"$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$欢迎使用教师工资管理系统￥￥￥￥￥￥￥￥￥￥￥￥￥￥￥￥"};
	 yan(hua) ;
 	do{
	
		printf("\t\t\t\t\t\t\t\t\n");
		printf("\t\t\t-----------------$$$$ 教师工资管理系统 $$$$-----------------\n");
 		printf("\t\t\t\t\t 1.录入教师基本信息\t\t\t\t\t\n");
 		printf("\t\t\t\t\t 2.修改或删除教师信息\t\t\t\t\t\n");
 		printf("\t\t\t\t\t 3.查询教师信息\t\t\t\t\t\t\n");
 		//system("color 24");
 		printf("\t\t\t\t\t 4.统计并分析工资信息\t\t\t\t\t\n");
 		printf("\t\t\t\t\t 5.退出\t\t\t\t\t\n");
 		printf("\t\t\t\t\t 6.系统简介\t\t\t\t\t\n");
 		printf("请输入你的选择(数字)：");
		 scanf("%d",&a)	;
		 
		 switch(a)
		 {
		 case 1:input();break;
		 case 2:change();break;
		 case 3:search();break;
		 case 4:analyze();break;
		 case 5:printf("谢谢使用！再见！！\n");exit(0);
		 case 6:introduction();break;
		 default:printf("输入错误！！！请重新输入！！！");break;
		 }
		}while(a!=5);
	system("cls");
	return 0;	
}
 
