# Reinforced Concrete Column Design Methodology

This methodology is based on the worked examples in:

- `Week 9 short column.pdf`
- `Week 10 slender column.pdf`

It is written as a reusable calculation procedure for reinforced concrete column design using the same interaction-curve approach shown in the notes.

## 1. Purpose

To assess the capacity of a reinforced concrete column subjected to combined axial compression and bending by:

1. defining the section and material properties,
2. constructing a column strength interaction diagram,
3. checking whether the column is short or slender,
4. applying slenderness magnification where required, and
5. confirming reinforcement and tie spacing satisfy design requirements.

## 2. Required Inputs

Obtain the following before starting:

- column dimensions `b` and `D`,
- clear height `L_u`,
- reinforcement layout and bar size,
- concrete cover,
- concrete strength `f'c`,
- steel yield strength `f_sy`,
- design axial force `N*`,
- design moment `M*`,
- frame/bracing condition,
- beam and column stiffness data for effective-length assessment.

Also determine:

- gross area `A_g`,
- compression steel area `A_sc`,
- tension steel area `A_st`,
- effective depth to tension steel `d`,
- depth to compression steel `d_sc`,
- distance from centroidal axis to section face if needed for eccentricity calculations.

## 3. Governing Design Model

Use strain compatibility and equivalent rectangular concrete stress block assumptions from the course notes / AS 3600 approach:

- concrete ultimate strain at extreme compression fibre: `epsilon_cu = 0.003`,
- steel yield strain: `epsilon_sy = f_sy / E_s`,
- stress-block factors `alpha` and `gamma` from the relevant code expressions for the selected `f'c`.

The interaction diagram is developed using four key points:

- Point `D`: uniform compression, `M_u = 0`,
- Point `C`: decompression point, `k_u = 1.0`,
- Point `B`: balanced failure point,
- Point `A`: pure bending, `N_u = 0`.

## 4. Short Column Interaction Diagram Procedure

### 4.1 Section idealisation

1. Sketch the cross-section and the bending axis.
2. Identify which reinforcement layer is in compression and which is in tension for the chosen bending direction.
3. Calculate `A_sc`, `A_st`, `d`, and `d_sc`.

### 4.2 Point D: Uniform compression capacity

At Point `D`, there is no bending and the whole section is in compression.

Use:

`N_uo = alpha_1 f'c A_g + f_sy A_s`

where `A_s` is the total longitudinal steel area.

Coordinates:

- `D = (0, N_uo)`

### 4.3 Point C: Decompression point

At Point `C`, the neutral axis passes through the tension steel layer, so:

- `k_u = 1.0`,
- tension steel force is zero,
- compression steel is typically assumed yielded if strain exceeds yield.

Procedure:

1. Compute axial force:

   `N_uc = alpha_2 gamma f'c b (k_u d) + C_s`

2. Take moments about the tension steel level to obtain the internal lever arm `h`.
3. Determine eccentricity:

   `e = h - (d - d_g)`

   where `d_g` is the distance from the section centroid to the tension-steel reference level used in the notes.

4. Compute moment:

   `M_uc = N_uc e`

Coordinates:

- `C = (M_uc, N_uc)`

### 4.4 Point B: Balanced failure point

At Point `B`:

- extreme concrete strain reaches `0.003`,
- tension steel just yields, so `epsilon_st = epsilon_sy`,
- therefore `k_u = k_ub` from strain compatibility.

Procedure:

1. Determine:

   `k_ub = epsilon_cu / (epsilon_cu + epsilon_sy)`

2. Find neutral-axis depth:

   `d_n = k_ub d`

3. Calculate compression-steel strain:

   `epsilon_sc = epsilon_cu (d_n - d_sc) / d_n`

4. Convert to compression-steel stress:

   `sigma_sc = min(E_s epsilon_sc, f_sy)`

5. Determine axial force:

   `N_ub = alpha_2 gamma f'c b d_n + sigma_sc A_sc - f_sy A_st`

6. Take moments about the tension-steel level to obtain `h`.
7. Determine eccentricity `e`.
8. Compute:

   `M_ub = N_ub e`

Coordinates:

- `B = (M_ub, N_ub)`

### 4.5 Point A: Pure bending

At Point `A`, axial force is zero:

- `N_u = 0`

Unknowns are usually `k_u` and compression-steel strain `epsilon_sc`.

Procedure:

1. Write axial equilibrium:

   `0 = C_c + C_s - T`

2. Use similar triangles in the strain diagram to relate `epsilon_sc` and `k_u`.
3. Substitute into the axial equilibrium equation and solve for `k_u`.
4. Calculate compression-steel stress from `epsilon_sc`.
5. Take moments about the tension-steel level:

   `M_u = C_c z_c + C_s z_s`

Coordinates:

- `A = (M_u, 0)`

### 4.6 Draw the interaction curve

1. Plot points `A`, `B`, `C`, and `D` on `M-N` axes.
2. Join the points smoothly to form the column interaction diagram.
3. If required, draw the line of constant eccentricity:

   `e = M / N`

4. A design point is satisfactory if it lies inside the strength curve, or inside the `phi`-reduced curve when design factors are applied directly.

## 5. Design Check for a Short Column

For a short column subjected to design actions `M*` and `N*`:

1. either compare `(M*, N*)` with the `phi`-reduced interaction diagram,
2. or convert to nominal demand and compare with the nominal interaction diagram:

   - `M_req = M* / phi`
   - `N_req = N* / phi`

The section is adequate when the demand point lies within the acceptable interaction boundary.

## 6. Slender Column Procedure

If the column may be slender, extend the short-column check as follows.

### 6.1 Determine effective length `L_e`

1. Identify whether the frame is braced or unbraced.
2. Evaluate end restraint from the connected beams/columns.
3. Determine the effective-length factor `k` from the code alignment charts / restraint expressions.
4. Compute:

   `L_e = k L_u`

5. Use the governing effective length permitted by the code clauses adopted in the notes.

### 6.2 Calculate slenderness ratio

Use:

`lambda = L_e / r`

For the rectangular example in the notes:

`r = 0.3 D`

### 6.3 Classify as short or slender

Compare `L_e / r` with the code limit used in the notes:

- if `L_e / r <= 25`, treat as short,
- if `L_e / r > 25`, treat as slender.

### 6.4 Determine critical buckling load `N_c`

For a slender column, calculate the critical buckling load using the code expression adopted in the worked example:

`N_c = (pi^2 / L_e^2) [182 d_o ((phi M_uc) / (1 + beta_d))]`

where:

- `d_o` is the effective depth term used in the notes,
- `M_uc` is taken from the balanced-point / interaction-curve capacity used in the example,
- `beta_d` is the load-duration factor or equivalent code parameter.

Use the exact code form required by your design standard and edition.

### 6.5 Determine the moment magnifier

For the braced-column example:

`delta_b = k_m / (1 - N* / N_c) >= 1.0`

with `k_m = 1.0` used in the notes.

### 6.6 Amplify design moment

Calculate the magnified moment:

`M*_a = delta_b M*`

Use `M*_a` instead of the original first-order moment in the final strength check.

### 6.7 Final strength check for slender column

Check the design pair:

- axial action `N*`,
- amplified moment `M*_a`

against the short-column interaction curve.

This may be done by:

1. comparing `(M*_a, N*)` with the `phi`-reduced curve, or
2. converting to nominal values `(M*_a / phi, N* / phi)` and checking against the nominal curve.

The column is adequate if the demand point remains within the acceptable interaction boundary.

## 7. Tie / Stirrup Design

After longitudinal strength is confirmed, check transverse reinforcement spacing.

From the worked example, tie spacing is taken as the lesser of:

- the least column dimension, and
- `15 d_b` for the longitudinal bar diameter,

subject to the relevant code clause for tied columns.

Adopt the smallest governing value and detail the tie arrangement so all longitudinal bars are laterally restrained.

## 8. Suggested Calculation Sequence for a Report

Use the following order in an engineering calculation:

1. State design standard, material strengths, and reduction factor `phi`.
2. Show section geometry and reinforcement layout.
3. Calculate `A_g`, `A_sc`, `A_st`, `d`, and `d_sc`.
4. Construct the interaction diagram using Points `D`, `C`, `B`, and `A`.
5. Plot the applied load point for the short-column check.
6. Determine frame restraint and effective length `L_e`.
7. Calculate slenderness ratio `L_e / r`.
8. Decide whether the column is short or slender.
9. If slender, calculate `N_c`, `delta_b`, and amplified moment `M*_a`.
10. Re-check the final design point on the interaction diagram.
11. Design and check stirrup spacing.
12. Conclude whether the column is adequate.

## 9. Conclusion Statement Template

The reinforced concrete column is adequate if the factored axial force and factored bending moment, including slenderness magnification where required, lie within the design interaction capacity and the transverse reinforcement spacing satisfies code limits.

---

If you want, I can also turn this into:

- a one-page handout for students,
- a formal calculation template with headings and equations,
- or a worked example sheet matching the exact dimensions from your notes.
