```c
#include <stdio.h>


int main() {

     int sum = 1000;

     int product = 0;




     for(int i = 1; i <= 1000; i = i + 1){
	
		for(int j = 1; j <= 1000; j = j + 1){
		
			for(int k = 1; k <= 1000; k = k + 1){
			
				if((i*i) + (j*j) == (k*k) && (i + j + k  == sum)) {
			
					product = i * j * k;
			
				}
		
 			}
	
		}

   	 }


     printf("Product: %d\n", product);

     
return 0;

}

```