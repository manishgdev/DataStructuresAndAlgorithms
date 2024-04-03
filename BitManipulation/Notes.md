## Bit Manipulation
### Check if nth Bit is set in a given number X or not
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

### Setting the nth bit in a number
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

### Clearing the nth bit in a number
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



