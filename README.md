# Full-Custom CMOS Logic and 256-Bit SRAM Design

This project presents the transistor-level design, simulation, physical layout, and verification of CMOS logic and memory circuits developed in **Cadence Virtuoso**. The work progresses from reusable logic cells to a hierarchical **16 × 16 SRAM array with a total capacity of 256 bits**.

The complete portfolio, including schematics, layouts, transient waveforms, DRC results, and LVS results, is available here:

**[View the full design portfolio](Digital_IC_Design_Portfolio_Aibek_Bekbergen.pdf)**

## Project Highlights

| Result | Value |
|---|---:|
| SRAM organization | 16 rows × 16 columns |
| Total memory capacity | 256 bits |
| 6T SRAM static noise margin | 210.8107 mV |
| D flip-flop hold time | 7 ps |
| Nominal supply voltage used in the documented simulations | 1 V |

## Implemented Circuits

### CMOS Logic and Sequential Circuits

- CMOS inverter
- 2-input NAND gate
- 2-input XOR gate
- CMOS transmission gate
- D flip-flop
- 5-input NAND gate for row decoding

Each principal cell was developed through the following flow:

1. Transistor-level schematic design
2. Reusable symbol creation
3. DC or transient simulation
4. Custom physical layout
5. Design Rule Check (DRC)
6. Layout Versus Schematic (LVS) verification

### SRAM Bitcell

The memory core uses a conventional **6-transistor SRAM bitcell**. The cell was evaluated through:

- Static noise margin simulation
- Write-0 operation
- Read operation with precharged bit lines
- Data-retention behavior
- Custom layout
- DRC and LVS verification

The simulated static noise margin was **210.8107 mV**.

### SRAM Peripheral Circuits

The following peripheral blocks were designed to support row selection, writing, precharging, and differential readout:

- **4-to-16 row decoder:** constructed from inverters and 5-input NAND gates, with an enable input
- **Bit-line sense amplifier:** amplifies a small differential voltage between the complementary bit lines using positive feedback
- **Precharge circuit:** charges and equalizes the bit lines before read or write operations
- **Write driver:** actively drives the complementary bit lines according to the input data
- **SRAM column:** integrates bitcells with the precharge, write, and sensing circuitry

## 16 × 16 SRAM Architecture

The final system combines 16 word lines and 16 columns to form a **256-bit SRAM**. The hierarchy consists of:

```text
16 × 16 SRAM
├── 4-to-16 row decoder
├── 16 SRAM columns
│   ├── 16 6T SRAM bitcells
│   ├── Precharge circuit
│   ├── Write driver
│   └── Bit-line sense amplifier
└── Control and data interfaces
```

Top-level transient simulations demonstrate write and read operations for different selected rows, including `WL0` and `WL15`.

## Characterization

### D Flip-Flop Hold Time

The D flip-flop was characterized by first measuring the nominal clock-to-Q response and then sweeping the data-input delay around the rising clock edge. Under the documented simulation conditions, the measured hold time was **7 ps**.

### SRAM Write Sequence

The documented write operation uses four phases:

1. **Precharge:** `PRE = 0`, `WL = 0`, and `WRITE = 0`; both bit lines charge to the supply voltage.
2. **Float:** precharge is disabled and the bit lines temporarily retain their charge.
3. **Write:** the word line and write driver are enabled; the driver forces complementary values onto `BL` and `BLB`.
4. **Hold:** the word line and write driver are disabled, and the SRAM cell retains its new state.

### Differential Readout

The bit-line sense amplifier operates in two phases:

- During **precharge**, the internal nodes are initialized while the evaluation path is disabled.
- During **evaluation**, a small voltage difference between the bit lines is amplified by the cross-coupled structure to produce stable complementary outputs.

## Verification Status

DRC and LVS results are documented for the individual CMOS cells, the 6T SRAM bitcell, the decoder, the sense amplifier, the precharge circuit, and the write driver. Functional transient simulation is also included for the integrated SRAM column and the 16 × 16 array.

The portfolio does not claim completed top-level LVS verification for the full 16 × 16 SRAM array.

## Tools and Skills Demonstrated

- Cadence Virtuoso schematic capture and layout
- Cadence ADE circuit simulation
- Full-custom CMOS layout
- Hierarchical circuit and symbol design
- Static noise margin analysis
- Timing characterization
- DRC and LVS verification
- SRAM architecture and peripheral-circuit integration

## Repository Contents

| File | Description |
|---|---|
| `README.md` | Project overview, architecture, results, and verification summary |
| `Revised_Digital_IC_Design_Portfolio_Aibek_Bekbergen.docx` | Complete illustrated portfolio with schematics, layouts, simulations, DRC, and LVS evidence |

## Author

**Aibek Bekbergen**  
M.Sc. Student in Electrical Engineering, UNIST  
[GitHub](https://github.com/i2xbekbergen) · [LinkedIn](https://www.linkedin.com/in/aibek-bekbergen/)

