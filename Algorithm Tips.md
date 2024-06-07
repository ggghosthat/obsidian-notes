1) Faster reverse integer

	```csharp
	public bool IsPalindrome(int x) {
		if (x < 0)
		return false;
	
		int original = x;
		int reversed = 0;
	
		while(x != 0){
			int digit = x % 10;
			x /= 10;
	
			reversed = reversed * 10 + digit;
		}
		return original == reversed;
	}  
	```