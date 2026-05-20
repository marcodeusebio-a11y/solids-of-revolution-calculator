# Solids of Revolution Calculator

A C++ command-line calculator for solids of revolution using cylindrical shells and disk/washer methods.

## Highlights

- Detects crossing and tangent/touching intersections.
- Supports side-boundary + intersection bounds for tangent-region problems.
- Supports implicit multiplication, such as `2x`, `3(x + 1)`, `2π`, `πx`, and `sin(x)cos(x)`.
- Accepts both `pi` and the Unicode symbol `π` in function expressions, such as `sin(π/2)` or `π*x^2`.
- Numeric prompts for bounds and axes also accept scalar expressions like `π`, `pi/2`, `2π`, and `sqrt(2)`.
- Uses Composite Simpson's Rule for volume and area estimates.
- Prints a refinement check by comparing the requested interval count with doubled intervals.
- Estimates the 2D area of the generating region before rotation.
- Warns when the disk/washer axis passes through the region and disks are created.
- Can export a labeled CSV sample table where every important number has a nearby explanation column.
- Includes an example labeled CSV export in `examples/labeled_washer_sample.csv`.
- Includes `--test` mode for quick self-checks.
- Includes a `Makefile` and `Doxyfile` for easier building and documentation.

## Command line build

```bash
make
```

Or without Make:

```bash
clang++ -std=c++17 -Wall -Wextra -pedantic main.cpp Solids_of_Revolution_Calculator.cpp -o solids_calc
```

## Run

```bash
./solids_calc
```

## Run self-checks

```bash
./solids_calc --test
```

Expected result:

```text
All self-checks passed.
```

## Xcode setup

Add these three files to the same Xcode command-line project target:

```text
main.cpp
Solids_of_Revolution_Calculator.cpp
Solids_of_Revolution_Calculator.h
```

Make sure `Solids_of_Revolution_Calculator.cpp` appears under:

```text
Target → Build Phases → Compile Sources
```

## Example: disk/washer volume around the x-axis

For the region bounded by `y = x`, `y = 0`, `x = 0`, and `x = 1`, rotated around `y = 0`:

```text
Choose task: 2
Enter number of slices/shells: 100
Disk/washer method option: 1
Top function in x: x
Bottom function in x: 0
Bounds method: 1
Left bound: 0
Right bound: 1
Axis of rotation y = 0
```

The volume should be approximately:

```text
1.04719755
```

which equals `pi / 3`, or `π / 3`.

## Example: tangent region with a side boundary

For the region bounded by `y = (x - 1)^2`, `y = 0`, `x = 0`, and tangent point `x = 1`, choose direct bounds or mixed bounds:

```text
Top function in x: (x - 1)^2
Bottom function in x: 0
Left bound: 0
Right bound: 1
Axis of rotation y = 0
```

The volume should be approximately:

```text
0.62831853
```

which equals `pi / 5`, or `π / 5`.


## Expression examples

You can now type pi either way:

```text
π
pi
2π
πx
sin(π/2)
π*x^2
```

For numeric prompts such as bounds or rotation axes, you can also enter scalar expressions:

```text
π
pi/2
2π
sqrt(2)
```

## Labeled CSV export

After a calculation, answer `y` to:

```text
Export a CSV sample table for this calculation? (y/n):
```

The export is still a CSV so it opens cleanly in Excel, Numbers, Google Sheets, or a text editor. It now includes label columns next to the numeric columns, so the user can tell what each number means. For example:

```text
input_label,input_value
"x sample input value",0.5

outer_radius_label,outer_radius_value
"outer radius = farther function distance from rotation axis",0.5

area_factor_label,area_factor_value
"washer cross-section area = pi*(outer_radius^2 - inner_radius^2); multiply by dx during integration",0.785398
```

The CSV includes the method, function orientation, bounds, axis of rotation, sample input values, function outputs, differences, shell radius/height, washer outer/inner radii, and the area factor used by the numerical integration. This is useful for debugging, explaining the method, or showing work in a portfolio.

## Notes

This is still a numerical calculator, not a full symbolic algebra system. It estimates intersections and integrals numerically, so difficult discontinuities or extremely narrow features may require a wider search interval, more slices/shells, or manual bounds.
