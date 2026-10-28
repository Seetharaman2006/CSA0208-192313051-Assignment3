# Grama Jyothi Smart Meter Electricity Billing System

## 1. Project Overview

Grama Jyothi is a rural electricity cooperative that provides electricity to thousands of households. This project implements a C-based smart meter billing system that calculates electricity charges using smart meter consumption data.

The system supports interval-based energy readings, configurable electricity tariffs, and peak-hour billing. It is designed to demonstrate how electricity billing can be adapted for smart meters that record energy consumption at regular intervals.

## 2. Objectives

* Calculate electricity bills from smart meter readings.
* Process energy consumption recorded in watt-hours (Wh).
* Apply configurable electricity tariff rates.
* Support peak-hour pricing.
* Calculate total, peak, and off-peak energy consumption.
* Read tariff settings and meter readings from external files.
* Support up to 35,040 readings per year, corresponding to 15-minute intervals.

## 3. Technologies Used

* **Programming Language:** C
* **Compiler:** GCC
* **Development Environment:** OnlineGDB or another C development environment
* **Input Format:** CSV
* **Configuration Format:** Plain-text configuration file

## 4. Project Structure

```text
Grama-Jyothi/
├── main.c
├── tariff.cfg
├── readings.csv
└── README.md
```

| File           | Description                                                              |
| -------------- | ------------------------------------------------------------------------ |
| `main.c`       | Contains the electricity billing program.                                |
| `tariff.cfg`   | Stores the fixed charge, tariff rates, peak multiplier, and slab limits. |
| `readings.csv` | Contains date, time, and interval energy consumption.                    |
| `README.md`    | Explains the project and how to run it.                                  |

## 5. Features

### Smart Meter Data Processing

Reads date, time, and energy consumption from a CSV file.

### Configurable Tariff

Loads billing parameters from `tariff.cfg`, allowing tariff values to be changed without modifying the main program.

### Slab-Based Billing

The example tariff uses:

* First 100 kWh: Free
* 101–200 kWh: ₹2.25 per kWh
* Above 200 kWh: ₹4.50 per kWh

### Peak-Hour Pricing

The program identifies readings between 6:00 PM and 9:59 PM and applies a peak multiplier of 1.20 (20% extra) to the calculated energy charge.

### Consumption Summary

Displays:

* Number of valid readings
* Total energy consumption
* Peak-hour consumption
* Off-peak consumption
* Fixed charge
* Energy charge
* Total electricity bill

## 6. Tariff Configuration

The `tariff.cfg` file contains:

```text
50.00 2.25 4.50 1.20 100 200
```

The values represent:

| Value   | Meaning                                   |
| ------- | ----------------------------------------- |
| `50.00` | Fixed charge in rupees                    |
| `2.25`  | First paid-slab rate in rupees per kWh    |
| `4.50`  | Second paid-slab rate in rupees per kWh   |
| `1.20`  | Peak-hour multiplier                      |
| `100`   | Upper limit of the free slab in kWh       |
| `200`   | Upper limit of the first paid slab in kWh |

These values are illustrative and can be changed according to the applicable electricity tariff.

## 7. Smart Meter Input Format

The `readings.csv` file contains one reading per line.

Example:

```csv
2026-10-01,08:00,500
2026-10-01,12:00,1000
2026-10-01,18:00,2000
2026-10-01,19:00,1500
2026-10-01,22:00,1000
```

Each row contains:

1. Date in `YYYY-MM-DD` format
2. Time in `HH:MM` format
3. Energy consumed during the interval, in watt-hours (Wh)

**Important:** The third column represents interval energy consumption, not a cumulative meter reading.

For example, `500` means that 500 Wh (0.5 kWh) was consumed during that interval.

## 8. Installation and Execution

### Step 1: Install a C Compiler

Install GCC or use an online C compiler such as OnlineGDB.

### Step 2: Prepare the Files

Place the following files in the same working directory:

* `main.c`
* `tariff.cfg`
* `readings.csv`

### Step 3: Compile the Program

Using GCC, execute:

```bash
gcc main.c -o grama_jyothi -std=c11 -Wall -Wextra
```

### Step 4: Run the Program

On Linux:

```bash
./grama_jyothi
```

On Windows:

```bash
grama_jyothi.exe
```

**OnlineGDB users:** Ensure that both input files are accessible in the program's working directory. If the environment does not support additional files directly, use its file-management or input-file facilities.

## 9. Sample Output

For the example input, the expected summary is approximately:

```text
====================================
   GRAMA JYOTHI SMART METER BILL
====================================
Number of readings : 5
Total consumption : 6.000 kWh
Peak consumption  : 3.500 kWh
Off-peak consumption: 2.500 kWh
Fixed charge      : Rs. 50.00
Energy charge     : Rs. 0.00
------------------------------------
TOTAL BILL        : Rs. 50.00
====================================
```

The total remains ₹50.00 because the example consumption is below the first 100 kWh free slab.

## 10. Error Handling

The program includes basic error handling for:

* Missing tariff configuration file
* Invalid tariff configuration
* Missing smart meter input file
* Invalid CSV rows
* Negative energy consumption
* Exceeding the maximum number of supported readings

## 11. Annual Smart Meter Capacity

A year contains:

* 24 hours per day
* 4 readings per hour
* 365 days per year

Therefore:

`24 × 4 × 365 = 35,040 readings per year`

The program defines a maximum capacity of 35,040 readings.

This capacity assumes a non-leap year and exactly one reading per 15-minute interval.

## 12. Limitations

* The tariff values are examples and are not official electricity rates.
* The program assumes that each CSV row contains interval energy consumption in Wh.
* The program applies the peak multiplier based on the timestamp of each reading.
* It does not fully validate chronological ordering, duplicate timestamps, or date validity.
* The implementation is a demonstration model and would require additional validation and testing before production use.

## 13. Future Enhancements

* Add household-specific billing records.
* Validate timestamps and missing intervals.
* Support leap years and multiple billing periods.
* Generate monthly bills and downloadable reports.
* Store customer data in a database.
* Add automatic detection of abnormal energy consumption.
* Integrate with IoT smart meters for real-time monitoring.

## 14. Conclusion

The Grama Jyothi Smart Meter Electricity Billing System demonstrates how C programming can be used to process interval-based energy consumption, apply configurable tariff slabs, and calculate peak and off-peak electricity charges.

Separating the tariff configuration and smart meter data from the source code makes the model easier to modify and test. The project provides a foundation for developing more advanced electricity billing systems for rural electricity cooperatives.
