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