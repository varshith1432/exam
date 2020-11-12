# exam


<!DOCTYPE html>
<html>
<body>
<pre>
1.merge
#include<stdio.h>
#include<time.h>
#include<unistd.h>
void msort(int[],int,int);
void merge(int [],int,int,int);
void main(){
	int a[100],i,n,low,high;
	double time=0.0;
	printf("enter the number\n");
	scanf("%d",&n);
	for(i=0;i<n;i++){
		scanf("%d",&a[i]);	
	}
	for(i=0;i<n;i++){
		printf("%d",a[i]);
	}
	low=0;high=n-1;
	clock_t begin=clock();
	msort(a,low,high);
	clock_t end=clock();
	printf("after sorting");
	for(i=0;i<n;i++){
		printf("%3d",a[i]);
	}
	time+=(double)(end-begin)/CLOCKS_PER_SEC;
	printf("time spent is %f seconds",time);
}
void msort(int a[],int low,int high){
	int mid;
	if(low<high){
		mid=(low+high)/2;
		msort(a,low,mid);
		msort(a,mid+1,high);
		merge(a,low,mid,high);
	}
}
void merge(int a[],int low,int mid,int high){
	int i,j,h,b[20],k;
	h=low;i=low;j=mid+1;
	while(h<=mid && j<=high){
		if(a[h]<a[j]){
			b[i]=a[h++];
		}
		else{
			b[i]=a[j++];
		}
		i=i+1;
	}
	if(h>mid){
		for(k=j;k<=high;k++){
			b[i++]=a[k];
		}
	}	
	else{
		for(k=h;k<=mid;k++){
			b[i++]=a[k];
		}
	}
	for(k=0;k<=high;k++){
		a[k]=b[k];
	}
}

2.quick
#include<stdio.h>
#include<time.h>
#include<unistd.h>
void qsort(int [],int,int);
int partition(int [],int,int);
void main()
{
	int a[20],i,n,first,last;
	double time=0.0;
	printf("enter the size of the array\n");
	scanf("%d",&n);
	printf("enter the elements\n");
	for(i=0;i<n;i++)
	  scanf("%d",&a[i]);
	first=0;last=n-1;
	clock_t begin=clock();
	qsort(a,first,last);
	clock_t end=clock();
	time+=(double)(end-begin)/CLOCKS_PER_SEC;
	printf("time taken is: %lf\n",time);
	printf("sorted elements of the array are\n");
	for(i=0;i<n;i++)
	  printf("%3d",a[i]);
	printf("\n");    
}
void qsort(int a[],int first,int last)
{
	int loc;
	if(first<last)
	{
		loc=partition(a,first,last);
	//	printf("array is divided at %d location\n",a[loc]);
		qsort(a,first,loc-1);
		qsort(a,loc+1,last);
	}
}
int partition(int a[],int first,int last)
{
	int i,j,k,pivot,temp;
	i=first;j=last;pivot=a[first];
	do
	{
		do
		{
			i++;
		}while(a[i]<pivot);
		while(a[j]>pivot)
		  j--;
		if(i<j)
		{
			temp=a[i];
			a[i]=a[j];
			a[j]=temp;
		}
		/*printf("elements are\n");
		for(k=first;k<=last;k++)
		  printf("%3d",a[k]);
		printf("\n");*/  
	}while(i<j);
	a[first]=a[j];
	a[j]=pivot;
	return j;  
}

3.minmax
#include<stdio.h>
#include<stdio.h>
#include<time.h>
#include<unistd.h>
int max, min;
int a[100];
void maxmin(int i, int j)
{
 int max1, min1, mid;
 
 if(i==j)
 {
  max = min = a[i];
 }
 else
 {
  if(i == j-1)
  {
   if(a[i] <a[j])
   {
    max = a[j];
    min = a[i];
   }
   else
   {
    max = a[i];
    min = a[j];
   }
  }
  else
  {
   mid = (i+j)/2;
   maxmin(i, mid);
   max1 = max; min1 = min;
   maxmin(mid+1, j);
   if(max <max1)
    max = max1;
   if(min > min1)
    min = min1;
  }
 }
}
int main ()
{
 int i, num;
 double time_spent=0.0;
 printf ("\nEnter the total number of numbers : ");
 scanf ("%d",&num);
 printf ("Enter the numbers : \n");
 for (i=1;i<=num;i++)
  scanf ("%d",&a[i]);

 max = a[0];
 min = a[0];
 clock_t begin=clock();
 maxmin(1,num);
 clock_t end=clock();
 //time = (double)(end-begin)/CLOCKS_PER_SEC;
 time_spent+=(double)(end-begin)/CLOCKS_PER_SEC;
 printf("TIME ELAPSE IS %f sec \n", time_spent);
 printf ("Minimum element in an array : %d\n", min);
 printf ("Maximum element in an array : %d\n", max);
 return 0;
}

4.knapsack
# include<stdio.h>
 void knapsack(int n, float weight[], float profit[], float capacity)
{
   float x[20], tp = 0;
   int i, j, u;
   u = capacity;
   for (i = 0; i < n; i++)
      x[i] = 0.0;
   for (i = 0; i < n; i++) 
   {
      if (weight[i] > u)
         break;
      else 
	  {
         x[i] = 1.0;
         tp = tp + profit[i];
         u = u - weight[i];
         printf("object profit=%f, weight=%f, selected portion=%f  \n",profit[i],weight[i],x[i]);
      }
   }
   if (i < n)
   {
     x[i] = u / weight[i];
     printf("object profit=%f, weight=%f, selected portion=%f  \n",profit[i],weight[i],x[i]);
   }
   tp = tp + (x[i] * profit[i]);
  // printf("\nThe result vector is:- ");
  // for (i = 0; i < n; i++)
    //  printf("%f\t", x[i]); 
   printf("\nMaximum profit is:- %f", tp);
}
int main()
{
   float weight[20], profit[20], capacity;
   int num, i, j;
   float ratio[20], temp;
   printf("Enter the no. of objects:- \n");
   scanf("%d", &num);
   printf("Enter the wts and profits of each object:- \n");
   for (i = 0; i <num; i++)
   {
      scanf("%f %f", &weight[i], &profit[i]);
   }
   printf("Enter the capacityacity of knapsack:- \n");
   scanf("%f", &capacity);
   for (i = 0; i <num; i++)
   {
      ratio[i] = profit[i] / weight[i];
   }
   for (i = 0; i <num; i++)
   {
      for (j = i + 1; j <num; j++) 
	  {
         if (ratio[i] < ratio[j])
		  {
            temp = ratio[j];
            ratio[j] = ratio[i];
            ratio[i] = temp;
 
            temp = weight[j];
            weight[j] = weight[i];
            weight[i] = temp;
 
            temp = profit[j];
            profit[j] = profit[i];
            profit[i] = temp;
         }
      }
   }
   knapsack(num, weight, profit, capacity);
   return(0);
}

5.jobsequence
#include<stdio.h>
void opt(int d[],int p[],int n)
{
	int j[40],profit=0,k,r,q,i;
	j[0]=0;
	for(i=1;i<=n;i++)
	 j[i]=0;
	j[1]=1;
	k=1;
	for(i=2;i<=n;i++)
	{
		r=k;
		while((d[j[r]]>d[i]) && (d[r]!=r))
		{
			r--;
		}
		if((d[j[r]]<=d[i]) && (d[i]>r))
		{
			for(q=k;q>=r+1;q--)
			 j[q+1]=j[q];
			j[r+1]=i;
			k++;
		}
	}
	printf("job sequence is:\n");
	i=1;
	while(j[i]!=0)
	{
		printf("%3d",j[i]);
		profit+=p[j[i]];
		i++;
	}
	printf("\n profit is %d\n",profit);
}
int main()
{
	int d[40],p[40];
	int i,j,temp,n;
	printf("enter the no.of jobs\n");
	scanf("%d",&n);
	p[0]=d[0]=0;
	for(i=1;i<=n;i++)
	{
		printf("enter the profit\n");
		scanf("%d",&p[i]);
		printf("enter the job deadline\n");
		scanf("%d",&d[i]);
	}
	for(i=1;i<=n;i++)
	{
		for(j=i+1;j<=n;j++)
		{
			if(p[i]<p[j])
			{
				temp=p[i];
				p[i]=p[j];
				p[j]=temp;
				
				temp=d[i];
				d[i]=d[j];
				d[j]=temp;
			}
		}
	}
	opt(d,p,n);
	return 0;
}

6.ditch
#include<stdio.h>
#define infinity 999
void dij(int n,int v,int cost[10][10],int dist[100])
{
int i,u,count,w,flag[10],min;
for(i=1;i<=n;i++)
flag[i]=0,dist[i]=cost[v][i];
count=2;
while(count<=n)
{
min=99;
for(w=1;w<=n;w++)
if(dist[w]<min && !flag[w])
min=dist[w],u=w;
flag[u]=1;
count++;
for(w=1;w<=n;w++)
if((dist[u]+cost[u][w]<dist[w]) && !flag[w])
dist[w]=dist[u]+cost[u][w];
}
}
void main()
{
int n,v,i,j,cost[10][10],dist[10];
printf("\n Enter the number of nodes:");
scanf("%d",&n);
printf("\n Enter the cost matrix:\n");
for(i=1;i<=n;i++)
for(j=1;j<=n;j++)
{
scanf("%d",&cost[i][j]);
if(cost[i][j]==0)
cost[i][j]=infinity;
}
printf("\n Enter the source matrix:");
scanf("%d",&v);
dij(n,v,cost,dist);
printf("\n Shortest path:\n");
for(i=1;i<=n;i++)
if(i!=v)
printf("%d->%d,cost=%d\n",v,i,dist[i]);
}

7.all pairs
#include<stdio.h>
#define infinity 999
void main()
{
	int a[10][10],n,i,j,k;
	printf("enter the no.of nodes\n");
	scanf("%d",&n);
	printf("enter the cost matrix\n");
	for(i=1;i<=n;i++)
	 for(j=1;j<=n;j++)
	 {
	  scanf("%d",&a[i][j]);
	  if(a[i][j]==0 && i!=j)
	   a[i][j]=infinity;
     }
    for(k=1;k<=n;k++)
      for(i=1;i<=n;i++)
        for(j=1;j<=n;j++)
           if(a[i][j]>(a[i][k]+a[k][j]))
            a[i][j]=a[i][k]+a[k][j];
    printf("matrix representing all pairs shortest paths:\n");
    for(i=1;i<=n;i++)
    {
     for(j=1;j<=n;j++)
     	printf("%3d",a[i][j]);
     printf("\n");
    }
}

8.insertion sort
</pre>

</body>
</html>
