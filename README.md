# Bifrost_dhCurves

Collection of of bifrost compounds to work with curves inside of Bifrost. bSplines should match Maya NURBS curves for the most part.
![bSpline_nodes](https://github.com/domrab/Bifrost_dhCurves/assets/58582379/66c73fe1-0ea7-46be-91ad-c5317272ee11)

---

# construct_bSpline
Construct a bSpline object from its control points, the degree, and optionally a knot vector.

### Inputs

<b>control_points [in]</b>\
The input control points for bSpline.

<b>degree [in]</b>\
The degree.

<b>knots [in]</b>\ (optional)`
The knot vector. This is optional. If nothing is provided, a default knot vector gets assigned.

<b>remap_range [in]</b>\
If no knot vector is supplied, the default range is 0 to spans. If custom range is true, the `min` and `max` input values get used.

<b>min [in]</b>\
Default start value for generated knot vector if its not supplied.

<b>max [in]</b>\
Default end value for generated knot vector if its not supplied.

### Outputs

<b>bSpline [out]</b>\
The resulting bSpline object.

---

# knot_vector
Construct a knot vector with the proper multiplicity.

### Inputs

<b>cv_count [in]</b>\
The number of cvs for which this knot vector will be used.

<b>degree [in]</b>\
The degree of the bSpline (determines the multiplicity).

<b>remap_range [in]</b>\
The default range is 0 to spans. If custom range is true, the `min` and `max` input values get used.

<b>min [in]</b>\
Default start value for generated knot vector if its not supplied.

<b>max [in]</b>\
Default end value for generated knot vector if its not supplied.

### Outputs

<b>knots [out]</b>\
The output knot vector

---

# parameter_array
Similar to the native `sequence_array` node but instead of a start and step size, this takes creates `size` samples between `start` and `end` inclusive.

### Inputs

<b>size [in]</b>\
The number of parameters.

<b>start [in]</b>\
The first value in the parameter array.

<b>end [in]</b>\
The last value in the parameter array.

### Outputs

<b>parameters [out]</b>\
The parameter array.

---

# bSpline_scope
An easy visualization compound for bSplines.

### Inputs

<b>bSpline [in]</b>\
The bSpline to visualize.

<b>steps_per_span [in]</b>\
The number of sample steps per span. Maya's nurbs equivalent of this is 4 or 16 depending if subdivision preview is turned on.

<b>color [in]</b>\
The visualization color.

<b>shape [in]</b>\
The shape, this corresponds to the shape on the strand shape.

<b>thickness [in]</b>\
The thickness of the shape, only applicable when `shape` is `tube`.

<b>screen_aligned [in]</b>\
If the shape is screen aligned, only applicable when `shape` is `tube`.

### Outputs

<b>strands [out]</b>\
The strands created from the bSpline for visualization purposes.

---

# get_d1_bSpline_length (internal)
Calculate the accurate length of a degree 1 bSpline curve

### Inputs

<b>bSpline [in]</b>\
The bSpline to get the length from.

<b>custom_range [in]</b>\
If true, the length is calculated on a subsection of the curve.

<b>min [in]</b>\
The start parameter of the sub curve.

<b>max [in]</b>\
The end parameter of the sub curve.

### Outputs

<b>length [out]</b>\
The accurate length.

<b>sample_positions [out]</b>\
The sampled positions used to calculate the length.

---

# get_dN_bSpline_length (internal)
Calculate the approximate length of a bSpline of any degree.

### Inputs

<b>bSpline [in]</b>\
The bSpline to get the length from.

<b>steps [in]</b>\
The total number of substeps used to estimate the length.

<b>custom_range [in]</b>\
If true, the length is calculated on a subsection of the curve.

<b>min [in]</b>\
The start parameter of the sub curve.

<b>max [in]</b>\
The end parameter of the sub curve.

### Outputs

<b>length [out]</b>\
The approximate length.

<b>sample_positions [out]</b>\
The sampled positions used to calculate the length.

---

# get_bSpline_length
Get the length of a given (sub) bSpline. The result will be accurate for a degree 1 spline but always smaller than the real length for any bSpline of degree greater than 1. 

### Inputs

<b>bSpline [in]</b>\
The bSpline to get the length from.

<b>custom_range [in]</b>\
If true, the length is calculated on a subsection of the curve.

<b>min [in]</b>\
The start parameter of the sub curve.

<b>max [in]</b>\
The end parameter of the sub curve.

<b>steps [in]</b>\
The total number of substeps used to estimate the length.

<b>color [in]</b>\
The visualization color.

<b>shape [in]</b>\
The shape, this corresponds to the shape on the strand shape.

<b>thickness [in]</b>\
The thickness of the shape, only applicable when `shape` is `tube`.

<b>screen_aligned [in]</b>\
If the shape is screen aligned, only applicable when `shape` is `tube`.

### Outputs

<b>length [out]</b>\
The approximate length.

<b>strands [out]</b>\
The strands created from the bSpline for visualization purposes.

---

# deconstruct_bSpline
Deconstruct a bSpline into its components.

### Inputs

<b>bSpline [in]</b>\
The bSpline to query.

### Outputs

<b>cvs [out]</b>\
The control points.

<b>cv_count [out]</b>\
The control point count.

<b>degree [out]</b>\
The degree.

<b>knots [out]</b>\
The knot vector.

<b>min [out]</b>\
The minimum value in the knot vector.

<b>max [out]</b>\
The maximum value in the knot vector.

---

# get_bSpline_cvs
Get control point info from a bSpline.

### Inputs

<b>bSpline [in]</b>\
The bSpline to query.

### Outputs

<b>cvs [out]</b>\
The control points.

<b>cv_count [out]</b>\
The control point count.

---

# get_bSpline_degree
Get the degree info from a bSpline.

### Inputs

<b>bSpline [in]</b>\
The bSpline to query.

### Outputs

<b>degree [out]</b>\
The degree.

---

# get_bSpline_knots
Get the knot vector info from a bSpline.

### Inputs

<b>bSpline [in]</b>\
The bSpline to query.

### Outputs

<b>knots [out]</b>\
The knot vector.

<b>min [out]</b>\
The minimum value in the knot vector.

<b>max [out]</b>\
The maximum value in the knot vector.

---

# deBoor (internal)
Simple deBoor implementation to sample a bSpline. While slower than the matrix representation of bSplines, I found this to produce an output matching maya nurbs curves.

### Inputs

<b>c__cvs [in]</b>\
The control point array.

<b>p__degree [in]</b>\
The degree of the curve.

<b>t__knots [in]</b>\
The knot vector.

<b>x__parameter [in]</b>\
The parameter to query at.

<b>k__span [in]</b>\
The span in which the parameter lies.

### Outputs

<b>position [out]</b>\
The calculated output position.

---

# find_span (internal)
Find the span for the deBoor algorith from a given parameter and the knot vector.

### Inputs

<b>parameter [in]</b>\
The parameter to find the span for.

<b>knots [in]</b>\

### Outputs

<b>parameter_clamped [out]</b>\
The parameter clamped in the valid knot vector range.

<b>span [out]</b>\
The span in which the parameter lies.

---

# sample_bSpline
Sample a bSpline at a given parameter

### Inputs

<b>bSpline [in]</b>\
The bSpline to query.

<b>parameter [in]</b>\
The parameter to sample the bSpline at.

### Outputs

<b>position [out]</b>\
The sampled position.

---

# sample_bSpline_per_span
Sample a bSpline several times at each span at equally spaced parameter intervalls.

### Inputs

<b>bSpline [in]</b>\
The bSpline to query.

<b>steps [in]</b>\
The number of parameter steps per span.

### Outputs

<b>positions [out]</b>\
The sampled positions.

<b>parameters [out]</b>\
The parameters at which the positions got sampled.

