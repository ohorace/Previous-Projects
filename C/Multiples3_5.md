```c
#include <stdio.h>



int main(){
     

int myarray[1000];

     int count = 0;

     int size = 0;
     
int sum = 0;

     

for(int i = 0; i < 1000; i = i +1)
{
	
	if (i % 3 == 0 || i % 5 == 0){
		
		myarray[count] = i;
		
		size = size + 1;
		
		count = count+1; 

	}

     }



     for(int i = 0; i <= size; i = i + 1)
{
	
	sum = sum + myarray[i];

     }



     printf("Sum: %d\n", sum);


     return 0;

 }

```