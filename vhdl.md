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

### Entity

```
entity my_entity is
port (
    port_name_1: in std_logic;
    port_name_2: out std_logic;
    port_name_3: out std_logic );
end my_entity;
```
