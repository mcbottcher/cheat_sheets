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

## Selected Signal Assignment

- Different from conditional assignment since it is only dependent on one expression

```
with <choose_expression> select
    target <= <expression> when <choices>,
              <expression> when <choices>;
```

```
begin
    with SEL select
        MX_OUT <= D3 when "11",
                D2 when "10",
                D1 when "01",
                D0 when "00",
                '0' when others;
end mux4t1_2;
```

## Process Statement

```
-- this is my first process
my_label: process(sensitivity_list) is
    <item_declaration>
begin
    <sequential_statements>
end process my_label;
```

- Every time there is a change in the signals in the process sensitivity list, all the sequential statements in the process are re-evaluated.

```
-- library declaration
library IEEE;
use IEEE.std_logic_1164.all;
-- entity
entity my_xor is
port ( A,B : in std_logic;
       F   : out std_logic);
end my_xor;
-- architecture
architecture behav of my_xor is
begin
    xor_proc: process(A,B) is
    begin
        F <= A XOR B;
    end process xor_proc;
end behav;
```

## Sequential if Statements

```
architecture mux_8to1_ce_arch of mux_8to1_ce is
    begin
    my_mux: process (Data_in,SEL,CE)
    begin
        if (CE = '0') then
        F_CTRL <= '0';
        else
            if
            (SEL = "111") then F_CTRL <= Data_in(7);
            elsif (SEL = "110") then F_CTRL <= Data_in(6);
            elsif (SEL = "101") then F_CTRL <= Data_in(5);
            elsif (SEL = "100") then F_CTRL <= Data_in(4);
            elsif (SEL = "011") then F_CTRL <= Data_in(3);
            elsif (SEL = "010") then F_CTRL <= Data_in(2);
            elsif (SEL = "001") then F_CTRL <= Data_in(1);
            elsif (SEL = "000") then F_CTRL <= Data_in(0);
            else F_CTRL <= '0';
            end if;
        end if;
    end process my_mux;
end mux_8to1_ce_arch;
```

## case Statement

```
case (expression) is
    when choices =>
        <sequential statements>
    when choices =>
        <sequential statements>
    when others =>
        <sequential statements>
end case;
```

## VHDL Operators

- Logical: `and or nand nor xor xnor`
- Relational: `= /= < <= > >=`, `/=` means not equal...
- Shift: `sll srl sla sra rol ror`
    - Shift Logical Left: Shift left and pad with zeros
    - Shift Logical Right: Shift right and pad with zeros
    - Shift left arithmetic: Shift left and pad with least significant bit
    - Shift right arithmetic: Shift right and pad with most significant bit
    - Rotate left: Roate left (most significant bit goes to least and rest are shifted)
    - Rotate right: Roate right (least significant bit goes to most and rest are shifted)
- Adding: `+ - &`
    - Often used with numeric types
    - `&` is the concatination operator: `C_val <= '1' & B_val & '0';`
- Sign: `+ -`
- Multiplying: `* / mod rem`
- Miscellaneous: `** abs not`

## Using VHDL for sequential circuits

- e.g. D-type flip-flop

```
entity d_ff is
    port ( D, CLK : in std_logic;
           Q : out std_logic);
end d_ff;
-- architecture
architecture my_d_ff of d_ff is
begin
    dff: process(CLK)
    begin
        if (rising_edge(CLK)) then
--or    if (CLK'event and CLK='1') then
            Q <= D;
        end if;
    end process dff;
end my_d_ff;
```

## Finite State Machine

```
-- architecture
architecture fsm1 of my_fsm1 is
    type state_type is (ST0,ST1);
    signal PS,NS : state_type;
begin
    sync_proc: process(CLK,NS,CLR)
    begin
        -- take care of the asynchronous input
        if (CLR = '1') then
            PS <= ST0;
        elsif (rising_edge(CLK)) then
            PS <= NS;
        end if;
    end process sync_proc;
        
    comb_proc: process(PS,TOG_EN)
    begin
        Z1 <= '0';
        -- pre-assign output
        case PS is
            when ST0 =>
                -- items regarding state ST0
                Z1 <= '0'; -- Moore output
                if (TOG_EN = '1') then NS <= ST1;
                else NS <= ST0;
                end if;
            when ST1 =>
                -- items regarding state ST1
                Z1 <= '1'; -- Moore output
                if (TOG_EN = '1') then NS <= ST0;
                else NS <= ST1;
                end if;
            when others => -- the catch-all condition
                Z1 <= '0'; -- arbitrary; it should never
                NS <= ST0; -- make it to these two statements
        end case;
end process comb_proc;

```

## One hot encoding

- This is how the states of the FSM are encoded.
- One hot encoding is when each state has its own output line
- e.g. 16 states = 16 output lines, with binary encoding only 4 are required.
- Often leads to smaller and faster FSM

- Changes needed to convert above example to one hot encoding

```
-- the approach for enumeration types
type state_type is (ST0,ST1,ST2,ST3);
signal PS,NS : state_type;
----------------------------------------------------------------------
-- the approach used for explicitly specifying state bit patterns
type state_type is (ST0,ST1,ST2,ST3);
attribute ENUM_ENCODING: STRING;
attribute ENUM_ENCODING of state_type: type is "1000 0100 0010 0001";
signal PS,NS : state_type;
```

## Structural modelling in VHDL

- Mapping ports of sub-level entities
```
-- library declaration
library IEEE;
use IEEE.std_logic_1164.all;
-- entity
entity my_compare is
    Port ( A_IN: in std_logic_vector(2 downto 0);
           B_IN: in std_logic_vector(2 downto 0);
           EQ_OUT : out std_logic);
end my_compare;
-- architecture
architecture ckt1 of my_compare is
    -- XNOR gate --------------------
    component big_xnor is
        Port ( A,B : in std_logic;
                F : out std_logic);
    end component;
    -- 3-input AND gate -------------
    component big_and3 is
        Port ( A,B,C : in std_logic;
               F : out std_logic);
    end component;
    -- intermediate signal declaration
    signal p1_out,p2_out,p3_out : std_logic;
begin
    x1: big_xnor port map (A => A_IN(2),
    B => B_IN(2),
    F => p1_out);

    x2: big_xnor port map (A => A_IN(1),
    B => B_IN(1),
    F => p2_out);

    x3: big_xnor port map (A => A_IN(0),
    B => B_IN(0),
    F => p3_out);

    a1: big_and3 port map (A => p1_out,
    B => p2_out,
    C => p3_out,
    F => EQ_OUT);
end ckt1;
```

## Creating generic components

- Use keyword `generic`
- Can use this to change the size/behaviour/other properties of a component that you make...

```
-- library declarations
library IEEE;
use IEEE.std_logic_1164.all;
-- entity
entity gen_parity_check is
generic ( n: positive);
port
( x: in std_logic_vector(n-1 downto 0);
y: out std_logic);
end gen_parity_check;
-- architecture
architecture arch of gen_parity_check is
begin
process(x)
variable temp: std_logic;
begin
temp:='0';
for i in x'range loop
temp := temp XOR x(i);
end loop;
y <= temp;
end process;
end arch;
```

```
-- library declaration
library IEEE;
use IEEE.std_logic_1164.all;
-- entity
entity my_parity_chk is
Port ( input
: in std_logic_vector(3 downto 0);
output : out std_logic);
end my_parity_chk;
-- architecture
architecture arch of my_parity_chk is
--------------- component declaration --------------------
component gen_parity_check is
generic ( N : positive);
port
( X : in std_logic_vector(N-1 downto 0);
Y : out std_logic);
end component;
begin
-------------- component instantiation -------------------
cp1: gen_parity_check generic map (4) port map (input, output);
end arch;
```