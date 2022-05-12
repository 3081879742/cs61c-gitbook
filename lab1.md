# Lab 1: C & CGDB

## Exercise 1: Warm Up <a href="#exercise-1-warm-up" id="exercise-1-warm-up"></a>

### Part 1 <a href="#part-1" id="part-1"></a>

返回字母在字符串中出现的次数

### Part 2

用每个核苷酸出现的次数填充DNA_SEQ

解答:

`ex1.h`

```c
typedef struct DNA_sequence {
    char sequence [21];
    int A_count;
    int C_count;
    int G_count;
    int T_count;
} DNA_sequence;
```

`ex1.c`

```c
/* Returns the number of times LETTER appears in STR.
There are two different ways to iterate through a string.
1st way hint: strlen() may be useful
2nd way hint: all strings end in a null terminator */
int num_occurrences(char *str, char letter)
{
    /* TODO: implement num_occurances */
    int count = 0;
    while (*str)
    {
        if (*str == letter)
            count++;
        str++;
    }
    return count;
}

/* Populates DNA_SEQ with the number of times each nucleotide appears.
Each sequence will end with a NULL terminator and will have up to 20 nucleotides.
All letters will be upper case. */
void compute_nucleotide_occurrences(DNA_sequence *dna_seq)
{
    /* TODO: implement compute_nucleotide_occurances */
    dna_seq->A_count = num_occurrences(dna_seq->sequence, 'A');
    dna_seq->C_count = num_occurrences(dna_seq->sequence, 'C');
    dna_seq->G_count = num_occurrences(dna_seq->sequence, 'G');
    dna_seq->T_count = num_occurrences(dna_seq->sequence, 'T');
    return;
}

```

## Exercise 2

### Part 1: Compiler Warnings 编译器警告

了解编译器警告以及解决这些警告的重要性。本节将在此过程中解决一个或多个bug。在继续下一节之前，请确保修复了这些错误。

### Part 2: Assert Statements 断言语句

使用`assert`语句找出不能正常工作的函数

解答:

添加`assert`:

```c
/* Returns true if PASSWORD meets the conditions specified above */
bool check_password(const char *first_name, const char *last_name, const char *password)
{
    bool length, upper, lower, number, name;
    lower = check_lower(password);
    length = check_length(password);
    name = check_name(first_name, last_name, password);
    number = check_number(password);
    upper = check_upper(password);
    assert(lower);
    assert(length);
    assert(name);
    assert(number);
    assert(upper);
    return (lower && length && name && upper && number);
}
```
修改`check_length`:
```c
/* Returns true if the length of PASSWORD is at least 10, false otherwise */
bool check_length(const char *password)
{
    // int length = strlen(password);
    // bool meets_len_req = (length <= 10);
    // return meets_len_req;
    return strlen(password) >= 10;
}
```

修改`check_number`:

```c
/* Returns true if PASSWORD contains at least one number, false otherwise */
bool check_number(const char *password)
{
    while (*password != '\0')
    {
        // if (check_range(*password, 0, 9))
        if (check_range(*password, '0', '9'))
        {
            return true;
        }
        ++password;
    }
    return false;
}/* Returns true if the length of PASSWORD is at least 10, false otherwise */
bool check_length(const char *password)
{
    // int length = strlen(password);
    // bool meets_len_req = (length <= 10);
    // return meets_len_req;
    return strlen(password) >= 10;
}
```

修改`check_range`:

```c
/* Returns true if LETTER is in the range [LOWER, UPPER], false otherwise */
bool check_range(char letter, char lower, char upper)
{
    // bool is_in_range = (letter > lower && letter < upper);
    // return is_in_range;
    return letter >= lower && letter <= upper;
}
```

