import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.util.*;
public class Sample {

	public static void main(String[] args) throws Exception {
		Scanner sc=new Scanner(System.in);
		String input="C:\\Users\\Prashwitha Sanil\\Desktop\\Coding Challenge\\input.txt";
		String output="C:\\Users\\Prashwitha Sanil\\Desktop\\Coding Challenge\\output.txt";
		FileReader file=new FileReader(input);
		BufferedReader br=new BufferedReader(file);
		int cost[]=new int[10];
		String goodies[]=new String[10];
		int count=0;
		
		for(int i=0;i<9;i++)
		{
			String st=br.readLine();
			if(st!=null)
			{
				String[] token = st.split(":", 5);
				goodies[count]=token[0];
				cost[count]=Integer.parseInt(token[1]);
				count++;
			}		
		}
		
		sorting(cost,goodies);
		
		System.out.println("Enter number of Employees:");
		int n=sc.nextInt();
		FileWriter out=new FileWriter(output,true);
		BufferedWriter bw=new BufferedWriter(out);
		int value=search(cost,n);
		bw.newLine();
		bw.write("\nEnter the number of Employees: "+n);
		bw.newLine();
		bw.write("The goodies that are selected for distribution are : \n");
		for(int j=value;j<value+n;j++)
		{
			bw.write(goodies[j]+" : ");
			String str1=Integer.toString(cost[j]);
			bw.write(str1);
			bw.newLine();	
		}
		int diff=cost[value+n-1]-cost[value];
		bw.write("The difference between the chosen goodie with highest price and the lowest price is "+diff+". \n");
		bw.close();
	}
	
	static void sorting(int[] cost, String[] goodies) 
	{
		int n=cost.length;
		for(int i=0;i<n;i++)
		{
			int min=i;
			for(int j=i+1;j<n;j++)
			  if(cost[j]<cost[min])
				  min=j;
			int temp=cost[min];
			cost[min]=cost[i];
			cost[i]=temp;
			String temp1=goodies[min];
			goodies[min]=goodies[i];
			goodies[i]=temp1;
		}
	}

	private static int search(int[] price,int n) 
	{	
		int a=Integer.MAX_VALUE;
		int pos=-1;
		for(int i=0;i<price.length-n-1;i++)
		{
			int n1=price[i+n-1]-price[i];
			if(a>n1)
			{
				pos=i;
				a=n1;
			}
		}
		return pos;
	}

	

}

