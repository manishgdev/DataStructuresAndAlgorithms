# Bit Manipulation
## Check if nth Bit is set in a given number X or not
#### 1. X & (1 << n) > 0
```python
def is_nth_bit_set(num, n):
    # Right shift the number by n positions
    shifted_num = num >> n
    # Perform bitwise AND with 1
    result = shifted_num & 1
    # If result is 1, nth bit is set
    return result == 1

# Example usage:
num = 17  # Binary representation: 10001
n = 4
print("Is the", n, "th bit set in", num, "?", is_nth_bit_set(num, n))
```

#### 2. (X>>n) && 1 == 1
```python
def is_nth_bit_set(num, n):
    # Right shift the number by n positions
    shifted_num = num >> n
    # Perform bitwise AND with 1
    result = shifted_num & 1
    # If result is 1, nth bit is set
    return result == 1

# Example usage:
num = 17  # Binary representation: 10001
n = 4
print("Is the", n, "th bit set in", num, "?", is_nth_bit_set(num, n))
```

## Setting the nth bit in a number
#### Use bitwise OR (`|`) operator

```python
def set_nth_bit(num, n):
    # Create a mask with only the nth bit set
    mask = 1 << n
    # Perform bitwise OR with the mask
    result = num | mask
    return result

# Example usage:
num = 17  # Binary representation: 10001
n = 2
new_num = set_nth_bit(num, n)
print("Number after setting the", n, "th bit:", new_num)
```
In above code
<li>The function set_nth_bit takes two arguments: num (the original number) and n (the position of the bit you want to set).</li>
<li>It creates a mask by left shifting 1 by n positions, which effectively sets only the nth bit in the mask.</li>
<li>Then, it performs a bitwise OR operation between the original number num and the mask to set the nth bit.</li>
The result is returned.
In the provided example, we're setting the 2nd bit (indexing starts from 0) in the number 17. The result will be 21 because the binary representation of 17 is 10001, and after setting the 2nd bit, it becomes 10101, which is equivalent to 21 in decimal.

## Clearing the nth bit in a number
### Using bitwise AND (`&`) and NOT (`~`)

```python
def clear_nth_bit(num, n):
    # Create a mask with only the nth bit set
    mask = ~(1 << n)
    # Perform bitwise AND with the mask
    result = num & mask
    return result

# Example usage:
num = 21  # Binary representation: 10101
n = 2
new_num = clear_nth_bit(num, n)
print("Number after clearing the", n, "th bit:", new_num)
```

In above code 
<ul>
<li>The function clear_nth_bit takes two arguments: num (the original number) and n (the position of the bit you want to clear).</li>
<li>It creates a mask by left shifting 1 by n positions and then complementing it, which effectively unsets only the nth bit in the mask.</li>
<li>Then, it performs a bitwise AND operation between the original number num and the mask to clear the nth bit.</li>

</ul>
In the provided example, we're clearing the 2nd bit (indexing starts from 0) in the number 21. The result will be 17 because the binary representation of 21 is `10101`, and after clearing the 2nd bit, it becomes `10001`, which is equivalent to 17 in decimal.

## Toggle the ith bit in number
**Using XOR (`^`) operator**
```python
def toggle_ith_bit(num, i):
    # Create a mask with only the ith bit set
    mask = 1 << i
    # Perform bitwise XOR with the mask
    result = num ^ mask
    return result

# Example usage:
num = 12  # Binary representation: 1100
i = 2
new_num = toggle_ith_bit(num, i)
print("Number after toggling the", i, "th bit:", new_num)

```
In the provided example, we're toggling the 2nd bit (indexing starts from 0) in the number 12, which has a binary representation of `1100`. After toggling the 2nd bit, the resulting number will be `8`, which corresponds to the binary representation `1000`.


## Clearing right most set bit in a number
### n & (n-1)
Example : Let's take 24, Binary of 24 is `110001` and binary of 23 (n-1) is `10111`, so 24 `&` 23 = 16 (`10000`)
```
def clear_rightmost_set_bit(num):
    # To clear the rightmost set bit, subtract 1 from the number and perform bitwise AND with the original number
    return num & (num - 1)

# Example usage:
num = 23  # Binary representation: 10111
result = clear_rightmost_set_bit(num)
print("Number after clearing the rightmost set bit:", result)
```

<ul>
<li>The function clear_rightmost_set_bit takes a number num as input.</li>
<li>Inside the function, we subtract 1 from the number, which effectively turns off the rightmost set bit and all bits to its right.</li>
<li>We then perform a bitwise AND operation between the original number and the result of num - 1, which effectively clears the rightmost set bit in the original number.</li>
<li>The resulting number is returned.</li>
</ul>

## Swap two numbers
<ul>
    <li>Using temp variable</li>
    <li>a = a+b, b = a - b, a = a -b</li>
    <li>usnig xor operator</li>
</ul>
#### Using XOR (`^`) operator

```python
def swap_numbers(a, b):
    print("Before swapping:")
    print("a =", a)
    print("b =", b)
    
    # Perform swapping using XOR operator
    a = a ^ b
    b = a ^ b
    a = a ^ b
    
    print("\nAfter swapping:")
    print("a =", a)
    print("b =", b)

# Example usage:
a = 5
b = 9
swap_numbers(a, b)
```

<ol>
<li>a=a^b</li>
<li>b=a^b => (a^b)^b => a</li>
<li>a=a^b => (a^b)^a => b</li>
</ol>

## Count Number of set bits in a number
<ol>
    <li>Divide the number by 2 recursively and store the quotient in a string and keep diving the remainders until the number is divisible by zero or remainder is 1</li>
    <li>Repeatedly right-shifting the number and checking the least significant bit (LSB) until the number becomes zero</li>
    <li>Repeatedly clearing the rightmost set bit, number of iterations taken to make number zero will be number of set bits</li>
</ol>

### Using Right Shift Operator
```python
def count_set_bits(num):
    count = 0
    while num:
        # Increment count if LSB is set
        count += num & 1
        # Right shift the number to check the next bit
        num >>= 1
    return count

# Example usage:
num = 23  # Binary representation: 10111
print("Number of set bits in", num, ":", count_set_bits(num))

```

### Repeatedly flipping the rightmost set bit to zero
```python
def count_set_bits(num):
    count = 0
    while num:
        # Flip the rightmost set bit to zero
        num &= (num - 1)
        # Increment the count
        count += 1
    return count

# Example usage:
num = 23  # Binary representation: 10111
print("Number of set bits in", num, ":", count_set_bits(num))

```

## Check if number is power of two
**`(num & (num - 1)) == 0`**

```python
def is_power_of_two(num):
    # A number is a power of 2 if and only if it has only one bit set
    # So, we can check if num & (num - 1) is equal to 0
    return num != 0 and (num & (num - 1)) == 0

# Example usage:
num = 16
print("Is", num, "a power of 2?", is_power_of_two(num))

```
## Find Single number in an array where other numbers are repeated three times
### traversing all the bits in number
```
def single_number(nums):
    # Initialize variables to store the count of set bits for each bit position
    result = 0
    # Traverse all the bits of an integer
    for i in range(32):
        # Initialize a variable to store the count of set bits at the ith position
        count = 0
        # Traverse all the numbers in the array
        for num in nums:
            # Increment count if the ith bit is set in the current number
            if num & (1 << i):
                count += 1
        # Reconstruct the single number by setting the ith bit if count is not divisible by 3
        if count % 3 != 0:
            # Use bitwise OR to set the ith bit in the result
            result |= (1 << i)
    return result

# Example usage:
nums = [3, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, 6, 7]
print("Number that appears only once:", single_number(nums))

```
<ul>
<li>We traverse all the bits of an integer (typically 32 bits for integers in Python).</li>
<li>For each bit position, we initialize a count variable to store the count of set bits at that position.</li>
<li>We then traverse all the numbers in the array and increment the count if the current number has the bit set at the current position.</li>
<li>After traversing all the numbers, we reconstruct the single number by setting the bit at the current position in the result if the count is not divisible by 3.</li>
<li>Finally, we return the result, which is the single number that appears only once in the array.</li>
</ul>
This approach has a time complexity of `O(n * 32) = O(n)` and a space complexity of O(1), where n is the number of elements in the array.

### Creating buckets ones, twos, three etc.

```python
def single_number(nums):
    # Initialize variables to store the count of set bits for each bit position
    ones = 0
    twos = 0

    for num in nums:
        # Update the 'twos' variable by performing a bitwise OR between 'twos' and the common bits in 'ones' and 'num'
        twos |= (ones & num)
        
        # Update the 'ones' variable by performing a bitwise XOR between 'ones' and 'num'
        ones ^= num
        
        # Calculate the common bits (bits that are set in both 'ones' and 'twos')
        common_bits = ones & twos
        
        # Clear the common bits from 'ones' and 'twos' by performing a bitwise NOT followed by AND operation
        ones &= ~common_bits
        twos &= ~common_bits
    
    # At the end, 'ones' will contain the number that appears only once
    return ones

# Example usage:
nums = [3, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, 6, 7]
print("Number that appears only once:", single_number(nums))

```
Short Implementation
```
ones = 0
twos = 0
for num in nums:
    # ones - number is ones but not in twos
    ones = ones ^ num & ~twos
    # twos - number is in twos then delete from ones
    twos = twos ^ num & ~ones
```

In this implementation:

We iterate through the array nums.
For each number num in the array:
<ul>
<li>We update the twos variable by performing a bitwise OR between twos and the common bits in ones and num. This operation effectively marks the bits that have appeared twice.</li>
<li>We update the ones variable by performing a bitwise XOR between ones and num. This operation effectively marks the bits that have appeared once.</li>
<li>We calculate the common bits (bits that are set in both ones and twos).</li>
<li>We clear the common bits from ones and twos by performing a bitwise NOT followed by AND operation.</li>
<li>At the end, the ones variable will contain the number that appears only once.</li>
</ul>
In the provided example, the output will be the number that appears only once in the array [3, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, 6, 7], which is 7.

### Jumping 3 positions 
```
def single_number(nums):
    # Sort the array
    nums.sort()
    
    # Iterate through the array, moving 3 positions at a time
    i = 0
    while i < len(nums) - 1:
        if nums[i] != nums[i + 1]:
            # If the current number is not equal to the next number, it is the single number
            return nums[i]
        i += 3
    
    # If the single number is at the last position or the array has only one element
    return nums[-1]

# Example usage:
nums = [3, 3, 3, 4, 4, 4, 5, 5, 5, 6, 6, 6, 7]
print("Number that appears only once:", single_number(nums))

```
<ul>
<li>We first sort the array nums in ascending order.</li>
<li>We then iterate through the sorted array, moving 3 positions at a time.</li>
<li>Inside the loop, we check if the current number is not equal to the next number. If it's not, then the current number is the single number that appears only once, so we return it.</li>
<li>If we reach the end of the loop without finding the single number, it means that the single number is at the last position of the array or the array has only one element. In such cases, we return the last element of the array.</li>

</ul>

This approach has a time complexity of O(n log n) due to sorting, where n is the number of elements in the array. However, it does not require any additional space beyond the input array.

## Print all subsets of an array 
### Using Bit manipulation
```
def print_subsets(nums):
    n = len(nums)
    # Total number of subsets is 2^n
    total_subsets = 1 << n
    
    # Iterate through all possible subsets
    for i in range(total_subsets):
        subset = []
        # Check which elements to include in the current subset based on the binary representation of i
        for j in range(n):
            if i & (1 << j):
                subset.append(nums[j])
        print(subset)

# Example usage:
nums = [1, 2, 3]
print("All subsets of", nums, ":")
print_subsets(nums)

```
<ul>
<li>We first calculate the total number of subsets, which is 2^n, where n is the number of elements in the array nums.</li>
<li>We then iterate through all possible subsets using a loop from 0 to total_subsets - 1.</li>
<li>Inside the loop, for each subset represented by the binary number i, we iterate through the bits of i to determine which elements to include in the current subset.</li>
<li>If the j-th bit of i is set, we include the j-th element of nums in the current subset.</li>
<li>Finally, we print each subset.</li>

</ul>
For the input array [1, 2, 3], the output will be:
```
[]
[1]
[2]
[1, 2]
[3]
[1, 3]
[2, 3]
[1, 2, 3]
```

## XOR of numbers in a given range (L, R)

<ol>
<li>Compute the XOR of numbers from 0 to R.</li>
<li>Compute the XOR of numbers from 0 to L-1.</li>
<li>Compute the XOR of the two results obtained above.</li>
</ol>
This will give you the XOR of numbers in the range [L, R].

```python
def compute_xor_range(L, R):
    # Function to compute XOR of numbers from 0 to n
    def compute_xor(n):
        if n % 4 == 0:
            return n
        elif n % 4 == 1:
            return 1
        elif n % 4 == 2:
            return n + 1
        else:
            return 0

    # Compute XOR of numbers from 0 to R
    xor_R = compute_xor(R)

    # Compute XOR of numbers from 0 to L-1
    xor_L_minus_1 = compute_xor(L - 1) if L > 0 else 0

    # Compute XOR of numbers in the range [L, R]
    xor_range = xor_R ^ xor_L_minus_1

    return xor_range

# Example usage:
L = 5
R = 10
print("XOR of numbers in the range [", L, ",", R, "]:", compute_xor_range(L, R))

```

```
1 - 1^0               = 1
2 - 1^2               = 3
3 - 1^2^3             = 0
4 - 1^2^3^4           = 4

5 - 1^2^3^4^5         = 1
6 - 1^2^3^4^5^6       = 7
7 - 1^2^3^4^5^6^7     = 0
8 - 1^2^3^4^5^6^7^8   = 8

9 - 1^2^3^4^5^6^7^8^9 = 1
```

## Perform Division with using a division operator
### repeated subtraction
```
def divide(dividend, divisor):
    # Sign of the result
    sign = -1 if (dividend < 0) ^ (divisor < 0) else 1

    # Take the absolute value of the dividend and divisor
    dividend = abs(dividend)
    divisor = abs(divisor)

    # Initialize quotient
    quotient = 0

    # Subtract divisor from dividend until dividend is less than divisor
    while dividend >= divisor:
        dividend -= divisor
        quotient += 1

    return sign * quotient

# Example usage:
dividend = 10
divisor = 3
print("Result of division:", divide(dividend, divisor))
```

### Using Bit Manipulation
```
def divide(dividend, divisor):
    # Sign of the result
    sign = -1 if (dividend < 0) ^ (divisor < 0) else 1

    # Take the absolute value of the dividend and divisor
    dividend = abs(dividend)
    divisor = abs(divisor)

    # Initialize quotient and result
    quotient = 0
    result = 0

    # Iterate from the maximum bit position to 0
    for i in range(31, -1, -1):
        if (result + (divisor << i)) <= dividend:
            result += (divisor << i)
            quotient |= (1 << i)

    return min(sign * quotient, 2**31 - 1)  # Ensure the result does not exceed 32-bit integer limit

# Example usage:
dividend = 10
divisor = 3
print("Result of division:", divide(dividend, divisor))

```
<ul>
<li>We determine the sign of the result similarly to before.</li>
<li>We take the absolute value of the dividend and divisor.</li>
<li>We initialize the quotient and result to 0.</li>
<li>We iterate from the maximum bit position (31) to 0.</li>
<li>In each iteration, we check if adding the shifted divisor to the result is less than or equal to the dividend. If it is, we update the result and set the corresponding bit in the quotient.</li>
<li>We return the quotient with the appropriate sign, ensuring it does not exceed the 32-bit integer limit.</li>

</ul>

## Count of repeated numbers in an array
```
def count_repeated_numbers(nums):
    # Initialize a bitmask to keep track of encountered elements
    bitmask = 0
    repeated_count = 0

    for num in nums:
        # Check if the current number is already encountered by checking the bitmask
        if bitmask & (1 << num):
            repeated_count += 1
        else:
            # If not encountered, mark the current number in the bitmask
            bitmask |= (1 << num)

    return repeated_count

# Example usage:
nums = [1, 2, 3, 4, 5, 2, 3, 4, 5, 6, 7, 8, 8]
print("Count of repeated numbers:", count_repeated_numbers(nums))

```
<ul>
<li>We initialize a bitmask variable to keep track of encountered elements. Initially, it is set to 0.</li>
<li>We iterate through the array nums.</li>
<li>For each element num in nums:</li>
<li>We check if the current number has been encountered before by checking if the corresponding bit is set in the bitmask using bitwise AND operation `(bitmask & (1 << num))`. If the bit is set, it means the number is repeated, so we increment the repeated_count.</li>
<li>If the number has not been encountered before, we mark it in the bitmask by setting the corresponding bit using bitwise OR operation `(bitmask |= (1 << num))`.</li>
<li>After iterating through all elements, we return the `repeated_count`, which represents the count of repeated numbers in the array.</li>
</ul>

