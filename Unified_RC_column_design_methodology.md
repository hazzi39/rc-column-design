# Unified Reinforced Concrete Column Design Methodology

This document combines the methodology for **rectangular** and **circular** reinforced concrete columns into a single calculation procedure.

It is based on:

- the rectangular short- and slender-column worked procedures in the attached course notes, and
- the attached circular-section ultimate strength procedure.

It is intended for use in engineering calculations for reinforced concrete columns subjected to combined axial compression and bending.

## 1. Purpose

To assess the adequacy of a reinforced concrete column by:

1. defining section geometry, materials, and reinforcement,
2. determining axial force and bending strength,
3. constructing or using the appropriate interaction diagram,
4. checking whether the column is short or slender,
5. including slenderness effects where required, and
6. confirming transverse reinforcement detailing is adequate.

## 2. Required Inputs

Obtain the following:

- section shape: rectangular or circular,
- section dimensions,
- clear column height `L_u`,
- concrete strength `f'c`,
- steel yield strength `f_sy`,
- steel elastic modulus `E_s`,
- concrete cover,
- longitudinal bar size, number, and layout,
- design axial force `N*`,
- design bending moment `M*`,
- frame / bracing condition,
- stiffness information for effective-length assessment,
- strength reduction factor `phi` from the governing code.

## 3. General Design Assumptions

Use the following ultimate strength assumptions:

- linear strain distribution,
- extreme concrete compression strain `epsilon_cu = 0.003`,
- steel yield strain `epsilon_sy = f_sy / E_s`,
- steel stress limited to `+/- f_sy`,
- compression taken as positive,
- design adequacy checked using a section interaction diagram.

For all sections:

- the column is adequate when the applied action point lies within the design interaction capacity,
- slender columns require moment magnification before the final interaction check.

## 4. Overall Design Workflow

Use the following sequence for any reinforced concrete column:

1. define geometry, reinforcement, and material properties,
2. identify the bending axis under consideration,
3. determine section properties and bar locations,
4. generate the section interaction curve,
5. check the applied load point for the short-column case,
6. determine effective length and slenderness,
7. if slender, calculate moment magnification,
8. re-check the design point using the amplified moment,
9. check tie / transverse reinforcement detailing,
10. conclude adequacy.

## 5. Section Geometry and Reinforcement

### 5.1 Rectangular sections

Determine:

- width `b`,
- overall depth `D`,
- gross area `A_g = bD`,
- compression steel area `A_sc`,
- tension steel area `A_st`,
- effective depth to tension steel `d`,
- depth to compression steel `d_sc`.

### 5.2 Circular sections

Determine:

- diameter `D`,
- radius `r = D/2`,
- gross area `A_g = pi D^2 / 4`,
- total steel area `A_s`,
- area of each bar `A_si`,
- position of each bar relative to the extreme compression fibre for the bending direction considered.

## 6. Strength Analysis for Rectangular Sections

For rectangular sections, the notes use a four-point interaction-curve construction based on strain compatibility and the equivalent rectangular stress block.

### 6.1 Define the four key points

Construct the interaction diagram using:

- Point `D`: uniform compression, `M_u = 0`,
- Point `C`: decompression point, `k_u = 1.0`,
- Point `B`: balanced failure,
- Point `A`: pure bending, `N_u = 0`.

### 6.2 Point D: uniform compression

At Point `D`, the whole section is in compression:

`N_uo = alpha_1 f'c A_g + f_sy A_s`

Coordinates:

- `D = (0, N_uo)`

### 6.3 Point C: decompression point

At Point `C`, the neutral axis passes through the tension steel layer:

- `k_u = 1.0`,
- tension steel force is zero.

Procedure:

1. calculate concrete and compression-steel forces,
2. sum forces to obtain `N_uc`,
3. take moments about the tension steel level,
4. determine eccentricity `e`,
5. calculate `M_uc = N_uc e`.

Coordinates:

- `C = (M_uc, N_uc)`

### 6.4 Point B: balanced failure

At Point `B`:

- concrete reaches `epsilon_cu = 0.003`,
- tension steel reaches `epsilon_sy`.

Procedure:

1. calculate:

   `k_ub = epsilon_cu / (epsilon_cu + epsilon_sy)`

2. determine neutral-axis depth:

   `d_n = k_ub d`

3. calculate compression-steel strain and stress,
4. sum internal forces to obtain `N_ub`,
5. take moments to obtain `M_ub`.

Coordinates:

- `B = (M_ub, N_ub)`

### 6.5 Point A: pure bending

At Point `A`:

- `N_u = 0`

Procedure:

1. write axial equilibrium:

   `0 = C_c + C_s - T`

2. relate compression-steel strain to neutral-axis depth using similar triangles,
3. solve for `k_u`,
4. calculate internal moment:

   `M_u = C_c z_c + C_s z_s`

Coordinates:

- `A = (M_u, 0)`

### 6.6 Draw the rectangular interaction curve

1. plot `A`, `B`, `C`, and `D`,
2. join the points smoothly,
3. plot the design action point,
4. confirm the design point lies within the permissible interaction boundary.

## 7. Strength Analysis for Circular Sections

For circular sections, use the circular compression-segment method from the attached procedure.

### 7.1 Trial neutral-axis approach

For a selected neutral-axis depth `d_n`, determine concrete and steel forces, then compute the corresponding `(M_u, N_u)` point. Repeat for a range of `d_n` values to build the full interaction diagram.

### 7.2 Compression-segment geometry

Let:

- `y d_n` = equivalent compression-block depth,
- `b_o` = maximum width of compression segment,
- `alpha` = angle subtended at the centre.

Then:

`b_o = 2 sqrt(2 y d_n r - (y d_n)^2)`

`alpha = 4 tan^-1 (2 y d_n / b_o)`

`A'_c = 0.5 r^2 (alpha - sin alpha)`

where `A'_c` is the effective concrete compression area.

### 7.3 Concrete compression force

The resultant concrete compression force is:

`C_c = 0.85 f'c A'_c`

acting at a depth `d_c` from the extreme compression fibre:

`d_c = r [1 - (4/3) (sin^3(alpha/2) / (alpha - sin alpha))]`

### 7.4 Bar strains and forces

For each reinforcing bar `i`, at depth `d_si` from the extreme compression fibre:

`epsilon_si = epsilon_cu (d_n - d_si) / d_n`

Then:

- `f_si = E_s epsilon_si` if the bar is elastic,
- `f_si = sign(epsilon_si) f_sy` if the bar yields.

The force in each bar is:

`F_si = A_si f_si`

### 7.5 Axial and moment capacity for a trial `d_n`

Sum forces:

`N_u = C_c + sum(F_si)`

Take moments about the plastic centroid:

`M_u = [C_c (r - d_c) + sum(F_si (r - d_si))]`

Then:

`e = M_u / N_u`

This gives one interaction-curve point `(M_u, N_u)`.

### 7.6 Draw the circular interaction curve

1. repeat the trial process for a sufficient range of `d_n`,
2. record all `(M_u, N_u)` points,
3. plot the points and join them smoothly,
4. plot the design action point,
5. confirm the point lies within the permissible interaction boundary.

## 8. Short Column Strength Check

For either section shape, check the design actions against the interaction capacity by one of the following:

1. compare `(M*, N*)` directly with the `phi`-reduced interaction curve, or
2. convert the design actions to nominal demand and compare with nominal capacity:

   - `M_req = M* / phi`
   - `N_req = N* / phi`

The section is adequate if the demand point lies within the acceptable interaction boundary.

## 9. Slenderness Assessment

The same general slenderness procedure applies to both rectangular and circular columns.

### 9.1 Determine effective length

1. identify whether the frame is braced or unbraced,
2. determine end restraint,
3. obtain effective-length factor `k`,
4. calculate:

   `L_e = k L_u`

### 9.2 Radius of gyration

Use the appropriate radius of gyration:

- rectangular section: use the value required by the governing code or the simplified expression adopted in the notes,
- circular section: `r_g = D / 4` for a solid section.

### 9.3 Slenderness ratio

Calculate:

`lambda = L_e / r_g`

Compare with the relevant code limit to classify the column as short or slender.

## 10. Slender Column Design Check

If the column is slender:

1. calculate the critical buckling load `N_c` using the governing code expression,
2. calculate the moment magnifier,
3. amplify the first-order moment,
4. re-check the amplified load point on the section interaction diagram.

For the braced-column procedure used in the notes:

`delta_b = k_m / (1 - N* / N_c) >= 1.0`

and:

`M*_a = delta_b M*`

Then check:

- axial force `N*`,
- amplified moment `M*_a`

against the appropriate rectangular or circular interaction curve.

## 11. Transverse Reinforcement Check

After longitudinal strength is confirmed, check transverse reinforcement requirements.

### 11.1 Rectangular columns

Check stirrup or tie spacing against the code limits, including:

- least section dimension,
- bar-diameter-based spacing limit,
- adequate restraint of all longitudinal bars.

### 11.2 Circular columns

Check circular ties or helical reinforcement, including:

- maximum pitch / spacing,
- cover,
- restraint of longitudinal bars,
- compliance with code requirements for tied or spirally reinforced columns.

## 12. Unified Calculation Sequence

Use the following sequence in a formal engineering calculation:

1. state the design code, material strengths, and reduction factor `phi`,
2. show the column geometry, reinforcement layout, and bending axis,
3. calculate section properties and reinforcement locations,
4. generate the interaction curve using the method appropriate to the section shape,
5. plot and check the short-column design load point,
6. determine effective length `L_e`,
7. calculate slenderness ratio,
8. decide whether the column is short or slender,
9. if slender, calculate `N_c`, the moment magnifier, and the amplified design moment,
10. re-check the final design point on the interaction diagram,
11. check tie or helical reinforcement detailing,
12. conclude whether the column is adequate.

## 13. Conclusion Statement Template

The reinforced concrete column is adequate if the factored axial load and bending moment, including slenderness magnification where required, lie within the design interaction capacity for the relevant section shape, and the transverse reinforcement satisfies all code detailing requirements.
