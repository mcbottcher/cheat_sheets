# VHDL

## VHDL Invariants

- VHDL is NOT case sensitive
- VHDL is NOT sensitive to whitespace
- Comments in VHDL begin with the `--`. No block commenting available
- VHDL statements are terminated by the `;`
- `if, case, loop`:
    - Every `if` statement has a corresponding `then`
    - Every `if` is terminated with an `end if;`
    - To do an else if, use `elsif`
    - `case` statement should be terminated by `end case;`
    - Each `loop` statement has a corresponding `end loop;`

## VHDL design units

- VHDL uses "Black Box" design
- The black box is referred to as an `entity`
- The stuff inside the black box is the `architecture`

## Entity

```
entity my_entity is
port (
    port_name_1: in std_logic;
    port_name_2: out std_logic;
    port_name_3: out std_logic );
end my_entity;
```

- Direction of signal can be `in, out, inout`
- `std_logic` is a VHDL data type
- Can also specify buses using the `to, downto` keywords:

```
entity my_entity is
port (
    port_name_1: in std_logic;
    port_name_2: out std_logic_vector(0 to 7);
    port_name_3: out std_logic_vector(7 downto 0) );
end my_entity;
```

- Alternatively to the `std_logic` datatype, which has 9 different states, you can use the `bit` data type which only has two states: `0` and `1`

## VHDL Standard Libraries

- Two main library packages:

```
library IEEE;
use IEEE.std_logic_1164.all;
use IEEE.numeric_std.all;
```

## Signal and variable assignment

- Several frequently used object types: `signal, variable, constant`
    - `signal`: Software representation of a wire
        - To assign a value to a `signal` type use the `<=` operator
        - A `signal`changes its value "some time" after the signal assignment expression is evaluated
    - `variable`: Used to store local information
        - To assign a value to a `variable` type, use the `:=` operator
        - A `variable` changes its value soon after the variable assignment is executed
    - `constant`: Like a `variable`, but value cannot change

## Concurrency

- Hardware description languages are not like software. Parallelism is inherent with it.

```
-- entity
entity my_circuit is
    port ( A_1,A_2,B_1,B_2,D_1 : in std_logic;
    E_out: out std_logic);
end my_circuit;

-- architecture
architecture my_circuit_arc of my_circuit is
    signal A_out, B_out, C_out : std_logic;
begin
    -- All of these happen in parallel (at the same time)
    A_out <= A_1 and A_2;
    B_out <= B_1 or B_2;
    C_out <= (not D_1) and B_2;
    E_out <= A_out or B_out or C_out;
end my_circuit_arc;
```

## Signal Assignment operator <=

- `<=` is the signal assignment operator
- The signal on the left hand side of the operator is dependant upon the signals on the right-hand side of the operator.

## Logical operators

- Available logical operators:
    - `AND`
    - `OR`
    - `NAND`
    - `NOR`
    - `XOR`
    - `XNOR`
    - `NOT` (Unary operator: only operates on one thing. The others are binary operators)

## Conditional Signal Assignment

- Use the `when` `else` keywords
- The individual conditions are evaluated sequentially in the conditional signal assignment statement until the first condition evaluates as true. In this case, the associated expression is evaluated and assigned to the target. Only one assignment is applied per assignment statement.

```
architecture f3_3 of my_ckt_f3 is
begin
    F3 <= '1' when (L = '0' AND M = '0' AND N = '1') else
    '1' when (L = '1' AND M = '1') else
    '0'; -- Catch all expression
end f3_3;
```

- This uses realational operators:
    - `=` is "is equal to"
    - `\=` is "is not equal to"

