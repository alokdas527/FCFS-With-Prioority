import java.util.Scanner;
 
class TestClass{
public static void main(String args[]){
int burst_time[],arrival_time[],process[],waiting_time[],ct[],tat[],i,p,j,n,total=0,tot=0,pos,temp;
float wait_avg,TAT_avg;
Scanner s = new Scanner(System.in);
 
System.out.print("Enter number of process: ");
n = s.nextInt();
 
process = new int[n];
burst_time = new int[n];
arrival_time=new int[n];
waiting_time = new int[n];
tat = new int[n];
ct=new int[n];
System.out.println("\nEnter Arrival time:");
for(i=0;i<n;i++)
{
System.out.print("\nProcess["+(i+1)+"]: ");
arrival_time[i] = s.nextInt();;
process[i]=i+1; //Process Number
}

System.out.println("\n Burst time:");
for(i=0;i<n;i++)
{
System.out.print("\nProcess["+(i+1)+"]: ");
burst_time[i] = 2*arrival_time[i];;
process[i]=i+1; //Process Number
}
 
//Sorting
for(i=0;i<n;i++)
{
pos=i;

for(j=i+1;j<n;j++)
{

if(burst_time[j]>burst_time[pos])
pos=j;
}
 temp=arrival_time[i];
arrival_time[i]=arrival_time[pos];
arrival_time[pos]=temp;

temp=burst_time[i];
burst_time[i]=burst_time[pos];
burst_time[pos]=temp;
 
temp=process[i];
process[i]=process[pos];
process[pos]=temp;

}
 
 
 
//First process has 0 waiting time
waiting_time[0]=arrival_time[0];

 
//Calculating Average waiting time
System.out.println("\nProcess\t Arrival Time \t Burst Time \tWaiting Time\tTurnaround Time");
ct[0]=burst_time[0]+arrival_time[0];
for(i=1;i<n;i++)
{
for(j=0;j<i;j++)
{
ct[i]=ct[j]+burst_time[i]; //Calculating completion Time
}
}
for(i=0;i<n;i++)
{
tat[i]=ct[i]-arrival_time[i];
waiting_time[i]=tat[i]-burst_time[i];
tot+=waiting_time[i];
total+=tat[i];
System.out.println("\n p"+process[i]+"\t\t"+arrival_time[i]+"\t\t "+burst_time[i]+"\t\t "+waiting_time[i]+"\t\t "+tat[i]);
}
 
//Calculation of Average Turnaround Time
wait_avg=(float)tot/n;
TAT_avg=(float)total/n;
System.out.println("\n\nAverage Waiting Time: "+wait_avg);
System.out.println("\nAverage Turnaround Time: "+TAT_avg);
 
}
}
