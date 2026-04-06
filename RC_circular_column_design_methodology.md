# Reinforced Concrete Circular Column Design Methodology

This methodology adapts the reinforced concrete column design procedure to **circular sections** using the attached circular-section strength method.

It is intended for engineering calculations for a circular reinforced concrete column subjected to combined axial compression and bending.

## 1. Purpose

To determine the ultimate strength of a circular reinforced concrete column by:

1. defining geometry, materials, and reinforcement layout,
2. evaluating axial load and bending capacity for selected neutral-axis depths,
3. constructing a circular-section interaction diagram,
4. checking whether slenderness effects must be included, and
5. confirming the final design strength is adequate.

## 2. Required Inputs

Obtain the following:

- column diameter `D`,
- radius `r = D/2`,
- clear height `L_u`,
- concrete strength `f'c`,
- steel yield strength `f_sy`,
- steel elastic modulus `E_s`,
- design axial force `N*`,
- design moment `M*`,
- concrete cover,
- number, size, and position of longitudinal bars,
- bracing/frame condition for slenderness assessment.

Also determine:

- gross concrete area `A_g = pi D^2 / 4`,
- area of each bar `A_si`,
- total steel area `A_s`,
- location of each bar relative to the extreme compression fibre for the bending axis considered.

## 3. Governing Assumptions

Use the ultimate strength assumptions from the attached circular-section procedure:

- extreme concrete strain `epsilon_u = 0.003`,
- linear strain distribution,
- neutral axis at depth `d_n` from the extreme compression fibre,
- equivalent concrete compressive stress `0.85 f'c`,
- steel stress:
  - `f_si = E_s epsilon_si` if the bar has not yielded,
  - `f_si = +/- f_sy` if yield occurs.

Compression is taken as positive.

## 4. Circular Section Geometry of Compression Block

For a selected neutral-axis depth `d_n`, first determine the equivalent concrete compression segment.

Let:

- `y d_n` = depth of equivalent rectangular stress block,
- `b_o` = maximum width of compression segment,
- `alpha` = angle subtended at the circle centre by chord `b_o`.

Then:

`b_o = 2 sqrt(2 y d_n r - (y d_n)^2)`

`alpha = 4 tan^-1 (2 y d_n / b_o)`

`A'_c = 0.5 r^2 (alpha - sin alpha)`

where `A'_c` is the effective area of the concrete compression block.

## 5. Resultant Concrete Compression Force

The concrete compressive force is:

`C_c = 0.85 f'c A'_c`

This force acts at the centroid of the compression segment, at distance `d_c` from the extreme compression fibre:

`d_c = r [1 - (4/3) (sin^3(alpha/2) / (alpha - sin alpha))]`

## 6. Strain and Force in Reinforcing Bars

For each reinforcing bar `i`, located at distance `d_si` from the extreme compression fibre:

`epsilon_si = epsilon_u (d_n - d_si) / d_n`

Then determine the steel stress:

- `f_si = E_s epsilon_si` if `|E_s epsilon_si| < f_sy`
- `f_si = sign(epsilon_si) f_sy` if yielding occurs

The force in each bar is:

`F_si = A_si f_si`

Take:

- `F_si > 0` for compression,
- `F_si < 0` for tension.

## 7. Axial Capacity for a Trial Neutral Axis

For the chosen `d_n`, the ultimate axial force is obtained by summing concrete and steel forces:

`N_u = C_c + sum(F_si)`

This gives the axial capacity corresponding to that neutral-axis position.

## 8. Moment Capacity for a Trial Neutral Axis

Take moments about the plastic centroid of the circular section. The ultimate moment is:

`M_u = [C_c (r - d_c) + sum(F_si (r - d_si))]`

The associated eccentricity is:

`e = M_u / N_u`

This gives one point on the circular-column interaction curve for the selected `d_n`.

## 9. Interaction Diagram Procedure for a Circular Section

Because the concrete compression region is a circular segment, it is generally more convenient to generate the interaction diagram numerically rather than by the rectangular-section four-point shortcut.

### 9.1 Define bar coordinates

1. Sketch the circular section and mark the bending axis.
2. Locate each longitudinal bar around the circumference.
3. For the chosen bending direction, determine `d_si` for every bar measured from the extreme compression fibre.

### 9.2 Select trial neutral-axis depths

Choose a series of `d_n` values covering the full range from:

- very large `d_n` for near-uniform compression,
- through balanced and decompression conditions,
- to small `d_n` for low axial load / pure bending conditions.

### 9.3 For each trial `d_n`

1. Calculate compression-block depth `y d_n`.
2. Calculate `b_o`, `alpha`, and `A'_c`.
3. Calculate concrete force `C_c` and centroid depth `d_c`.
4. For each reinforcing bar, calculate `epsilon_si`, `f_si`, and `F_si`.
5. Sum forces to obtain `N_u`.
6. Sum moments to obtain `M_u`.
7. Record the point `(M_u, N_u)`.

### 9.4 Plot the curve

1. Plot all calculated points on `M-N` axes.
2. Join the points smoothly to form the circular-column interaction diagram.
3. Plot the design action point `(M*, N*)`, or `(M*/phi, N*/phi)` if checking against nominal strength.

The column is adequate if the design point lies within the acceptable interaction boundary.

## 10. Special Loading States

The following limiting cases are still useful for interpretation, even if the interaction curve is generated numerically.

### 10.1 Near uniform compression

When eccentricity is very small and the neutral axis is far outside the section, the whole section is predominantly in compression. This gives the upper end of the interaction diagram.

### 10.2 Balanced condition

Balanced failure occurs when:

- concrete at the extreme compression fibre reaches `epsilon_u = 0.003`, and
- the extreme tension steel reaches yield strain.

This point can be identified during the trial process and is often close to the peak-moment region of the interaction curve.

### 10.3 Pure bending

Pure bending occurs when:

- `N_u = 0`

This point is obtained by varying `d_n` until the summed internal axial force is zero.

## 11. Slenderness Check for Circular Columns

The same overall slenderness procedure used for rectangular columns can be applied to circular columns.

### 11.1 Effective length

1. Determine end restraint and frame bracing.
2. Obtain effective-length factor `k`.
3. Compute:

   `L_e = k L_u`

### 11.2 Radius of gyration

For a solid circular section:

`r_g = D / 4`

### 11.3 Slenderness ratio

Calculate:

`lambda = L_e / r_g`

Compare with the relevant code slenderness limit to determine whether second-order effects must be included.

## 12. Slender Column Strength Check

If the circular column is slender:

1. determine the critical buckling load using the applicable code expression,
2. calculate the moment magnifier,
3. amplify the first-order design moment,
4. re-check the design point against the circular-section interaction curve using the amplified moment.

Use the same code-based slenderness procedure as for rectangular columns, but use the **circular-section interaction curve** for the final strength check.

## 13. Tie / Helical Reinforcement Check

After longitudinal strength is verified, check transverse reinforcement requirements.

For circular columns, this may be:

- circular ties, or
- helical reinforcement,

depending on the detailing adopted.

Confirm:

- maximum pitch / spacing,
- bar restraint,
- cover,
- and all code detailing requirements for circular tied or spirally reinforced columns.

## 14. Suggested Calculation Sequence

Use the following order in an engineering calculation:

1. State design standard, material strengths, and reduction factor `phi`.
2. Show circular section geometry and bar arrangement.
3. Tabulate the bar positions and corresponding `d_si`.
4. Select a trial value of neutral-axis depth `d_n`.
5. Compute `b_o`, `alpha`, `A'_c`, `C_c`, and `d_c`.
6. Compute strain, stress, and force in each bar.
7. Sum forces to obtain `N_u`.
8. Sum moments to obtain `M_u`.
9. Repeat for enough `d_n` values to define the interaction curve.
10. Plot the interaction diagram.
11. Check the applied load point for the short-column case.
12. Determine `L_e`, radius of gyration, and slenderness ratio.
13. If slender, magnify the design moment and re-check the point on the interaction diagram.
14. Check transverse reinforcement detailing.
15. Conclude adequacy of the circular column.

## 15. Conclusion Statement Template

The circular reinforced concrete column is adequate if the factored axial load and bending moment, including any required slenderness magnification, lie within the design interaction capacity obtained from the circular-section strength analysis, and the transverse reinforcement satisfies code detailing requirements.

---

If you want, I can next merge this with the previous rectangular methodology into one combined document titled:

- `RC column design methodology for rectangular and circular sections`

or turn the circular method into a spreadsheet-style step table for calculations.
