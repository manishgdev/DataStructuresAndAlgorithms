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


