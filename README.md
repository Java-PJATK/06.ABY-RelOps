# 6.ABY-RelOps
Listing 6 ABY-RelOps/RelOps.java Page 23

# Section 5. Instructions and operators

## 5.1 Operators

Operators are usually expressed by symbols (like `+`, `*`, etc.) and represent operations to be performed on their **operands** (arguments). Most operators are _binary_, i.e., they operate on two operands; some operators act on one operand only (they are called _unary_ operators). Finally, there is one _ternary_ operator.

### 5.1.1 Assignment operator

Assignment operator

`b = expr;`

evaluates the value of the right-hand side and stores the result in a variable appearing on the left-hand side. The type of the value of `expr` must be the same as the type of `b`, or be implicitly convertible to this type. It is important to remember that the whole expression `a=b` has a type and a value: the type of this expression is the type of the left-hand operand, and its value is equal to the value of the left-hand operand _after_ the assignment. Therefore, after

```java
int a, b = 1, c;
c = (a = b+1) + 1;
```

values of `a`, `b` and `c` will be 2, 1, 3.

Note that addition (subtraction, etc.) does _not_ modify values of operands — it just yields a new _temporary value_ and we have to do something with this value: print it, assign it to a variable, use it in an expression, etc. For example, after

```java
int a = 5, b = 1;
b = 2*(a + 1) + b;
```

the value of a is still 5; when calculating `a+1` we got a value (in this case 6) which is subsequently multiplied by 2 and added the current value of b, i.e., 1. We haven’t assigned any new value to `a`, so it remains as it was. However, the value of the whole expression on the right-hand side of the assignment (13) has been assigned to b (erasing its previous value), so `b` _is_ modified here.

There is a special form of assignment, the so called **compound** or **augmented** assignment operator. It has the form

`a @= b`

where `@` stands for any binary operator, like `+`, `*`, `%`, `>>`, etc. and is (almost) equivalent to

`a = a @ b`

For example `a += 5` would mean _increment_ `a` _by 5_, and `a /= 2` — _divide_ a _by 2_. Other examples:

```
    // shift operator
a <<= 2;
a = a << 2;

    // mod (remainder) operator
a %= 7;
a = a % 7;

    // bitwise ANDing
a &= 0xFF;
a = a & 0xFF;
```
Incrementing and decrementing integral values by 1 is so often used that it has a special syntax.

If a is a variable of an integral type, then ++a and a++ cause a to be incremented by 1 (with - instead of + — decremented). However, there is a difference between these two forms.

_Pre_incrementation or decrementation (`++a` or `--a`) are ‘immediate’. The value of a is incremented (decremented) and the value of the expression `++a` or `--a` will be equal to this already incremented or decremented value.

However, when a variable (say, a) is _post_incremented (or _post_decremented), the value of the variable a is also modified, but the value of the _expression_ `a++` (or `a--`) is equal to the ’old’, unmodified value of `a`.

For example, after

```
int a = 5, b = 1, c;
c = ++a + b--;
```

c will be 7, as on the right-hand side a has been incremented and the value of `++a` is equal to this incremented value (which is 6 in the example), while b is decremented, but the value of the expression `b--` is equal to the ’old’, not decremented, value of `b` (i.e., still 1). However, after

```
int a = 5, b = 1, c;
c = ++a + --b;
```

c will be 6, as values of `++a` and `--b` will reflect ’new’ values of these variables. In both cases, after the assignment to `c`, values of `a` and `b` are 6 and 0, respectively.

### 5.1.2 Arithmetic operators  

Well known examples of arithmetic operators include addition (a+b), multiplication (a*b), division (a/b), and subtraction (a-b). As we can see, binary operators (those,
that require two operands) are placed between operands they act upon.

Important: All binary arithmetic operations are always performed on
• two values of type int, or
• two values of type long, or
• two values of type float, or
• two values of type double,

and the result is the value of the same type as the type of operands.

In other cases, the values of one or both operands will be implicitly converted to match one of these cases. Therefore:

To format the provided content in GitHub Markdown without rephrasing:

```java
int i1 = 7;
char c1 = 'A', c2 = 'x';
short s1 = 3;
long l1 = 9;
double d1 = 3.5;

int r1 = i1 + s1;      // short -> int
long r2 = l1 + c1;     // char -> long
double r3 = l1 + d1;   // long -> double
int r4 = c1 + c2;      // char -> int (both operands)
int r5 = c1 + s1;      // char -> int, short -> int
```

Explanation and Notes:
- When adding values of different types:
  - Adding a `short` and an `int` results in an `int`.
  - Adding a `long` and a `char` results in a `long`.
  - Adding a `long` and a `double` results in a `double`.
  - Adding two `char` values results in an `int`.
  - Adding a `char` and a `short` results in an `int` (due to promotion to `int`).

For example, adding two `byte` values together gives an `int`, not a `byte`. Therefore, explicit casting would be required to store the result in a `byte` variable:

```java
byte a = 1, b = 2;
byte c = (byte)(a + b); // Now OK
```

Also remember that if two operands are of integral type, so is the result. Therefore,
1/2 is exactly 0, and 7/2 is exactly 3. When you divide two integers values, the result
is always truncated towards zero — for example, `7/3` and `-7/3` are `2` and `-2`, respectively.

Everybody knows addition, subtraction, multiplication, and division. Less known is the remainder (also called modulus operator) operator: `a % b`, yields the remainder after the division of `a` by `b`, so for example,

- `20 % 7` is `6` (as `20` is `2*7 + 6`)
- `19 % 6` is `1` (as `19` is `3*6 + 1`)

etc.

Note that in mathematics remainders are never negative. In most programming languages, however, the following is assumed to be always true:

```
(a/b) ∗ b + (a%b) ≡ a
```

This, combined with the convention that integer division always truncates towards 0, leads to the following rule:

taking the remainder yields remainder of absolute values of operands with the sign of the first operand

For example

```
System.out.println(" 7 /  2 = " + ( 7 / 2 ));
System.out.println(" 7 / -2 = " + ( 7 /-2 ));
System.out.println("-7 /  2 = " + (-7 / 2 ));
System.out.println("-7 / -2 = " + (-7 /-2 ));
System.out.println(" 7 %  2 = " + ( 7 % 2 ));
System.out.println(" 7 % -2 = " + ( 7 %-2 ));
System.out.println("-7 %  2 = " + (-7 % 2 ));
System.out.println("-7 % -2 = " + (-7 %-2 ));
```

Sure, here's your text formatted for GitHub Markdown:

---

### 5.1.3 Conditional and relational operators

Relational operators yield Boolean values. Comparing values (of various types) we get true or false, i.e., a Boolean value. For example:

- `a < b` // is a smaller than b ?
- `a > b` // is a bigger than b ?
- `a <= b` // is a smaller or equal to b ?
- `a >= b` // is a bigger or equal to b ?
- `a == b` // are a and b equal ?
- `a != b` // are a and b different ?

Logical values may be combined: the logical conjunction (AND) is denoted by `&&` and alternative (OR) by `||`. An exclamation mark denotes negation (NOT); for example:

- `a <= b && b <= c` // b belongs to the [a, c] interval
- `a < b || b > c` // b is outside this interval
- `!(a <= b && b <= c)` // negation of the first condition, equivalent to the second (de Morgan’s law)

**Short-circuiting:** `&&` and `||` operators are short-circuited (also known as McCarthy evaluation). If, after evaluation of the first term, the result is already known, the second term will not be evaluated. Therefore:

- For `expr1 && expr2`: if `expr1` is false, then `expr2` will not be evaluated.
- For `expr1 || expr2`: if `expr1` is true, then `expr2` will not be evaluated.

For example, in the expression `if (b != 0 && a/b > 5)`, division by zero will never occur because if `b` is zero, `b != 0` is false, making the entire condition false, and division by `b` will not be attempted.

**Caution:** Changing the order to `if (a/b > 5 && b != 0)` could result in a divide-by-zero error if `b` is zero!

In very rare situations, if we want both operands of an OR or AND operator to be evaluated regardless of the result of the evaluation of the first operand, we can use operators `|` and `&` (single, not doubled). Then both operands are always evaluated. Note that these symbols (`|` and `&`) stand for logical AND and OR only if their operands are boolean types. If operands are integer numbers, they denote bit-wise AND and bit-wise OR operators which result in integer values (see the next section).

There is also the so called ‘exclusive OR’ (XOR) operator, denoted by `ˆ`. If `expr1` and `expr2` have values of type `boolean`, then the expression

```
expr1 ^ expr2
```

is true if, and only if, the values of expr1 and expr2 are different, i.e., true and false or false and true. For example, if x is a double, after

```java
boolean b = (x >=2 && x <= 5) ^ (x >=3 && x <= 7);
```

b will be true if x ∈ [2, 5] ∪ [3, 7] but x /∈ [2, 5] ∩ [3, 7], i.e., when x belongs to the symmetric difference of the two intervals (their sum but without their intersection).

## Listing 6 ABY-RelOps/RelOps.java

```java
public class RelOps {
    public static void main (String[] args) {
        int a = 1, b = 8, d = 8;
        System.out.println(
                "Is d in [a,b]: " +
                ( a <= d && d <= b ));
        System.out.println(
                "Is d in (a,b): " +
                ( a <  d && d <  b ));
        System.out.println(
                "Is d outside (a,b): " +
                ( d <  a || d >  b ));
        System.out.println(
                "Is d outside (a,b): " +
                ( !(d >=  a || d <=  b) ));
        System.out.println(
                "Is d == b: " + (d == b));
        System.out.println(
                "Is d != b: " + (d != b));
    }
}
```

The **conditional expression** is the only ternary operator, i.e., an operator with three operands. 

It looks like this

```
cond ? expr1 : expr2
```

Here `cond` is an expression of type `boolean`. If it is `true`, then the value of `expr1` will become the value of the whole expression and `expr2` will not be evaluated; if `cond` is `false`, then the value of `expr2` becomes the value of the whole expression and `expr1` is not evaluated. The simplest example would be (`a` and `b` are `int`s):

```
int mx = a > b ? a : b;
```

which initializes `mx` with the bigger of `a` and `b` values. The ternary operator resembles the `if...else if` construct, but is not equivalent!

In particular, expression `b ? e1 : e2` has a value, while `if...else if` has not. 

For example,

```
a > b ? System.out.print("a") : System.out.print("b"); // NO!!!
```

doesn’t make sense, because `print` has no value.
