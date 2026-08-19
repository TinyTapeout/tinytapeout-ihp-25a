## How it works

The subtile factory test module is a simple module that can be used to test all the I/O available to a subtile on an ASIC.

Note: the bidirectional pins are unavailable to subtiles.

It has three modes of operation:

1. Mirroring the input pins to the output pins (when `rst_n` is low and `clk` is high).
2. Mirroring and inverting the input pins to the output pins (when `rst_n` is low and `clk` is low).
3. Outputting all zeros to the output pins (when `rst_n` is high, `clk` doesn't matter).

The following table summarizes the modes:

| `rst_n` | `clk` | Mode                  | uo_out value |
|---------|-------|-----------------------|--------------|
| 0       | 1     | Input mirror          | ui_in        |
| 0       | 0     | Inverted input mirror | uio_in       |
| 1       | X     | All zeros             | `8'b0`       |

This is implemented in Verilog as:

```verilog
assign uo_out  = rst_n ? (clk ? ui_in : ~ui_in) : 8'b0;
```

## How to test

1. Set `rst_n` low and `clk` high and observe that the input pins (`ui_in`) are output on the output pins (`uo_out`).
2. Set `rst_n` low and `clk` low and observe that the input pins (`ui_in`) are inverted and output on the output pins (`uo_out`).
2. Set `rst_n` high (and `clk` to anything) and observe that the output pins (`uo_out`) are all driven low.