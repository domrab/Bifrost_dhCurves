# Bifrost_dhCurves

Collection of Bifrost compounds to work with curves inside of Bifrost. bSplines should match Maya NURBS curves for the most part.\
To install, follow the instructions [here](https://help.autodesk.com/view/BIFROST/ENU/?guid=Bifrost_Common_install_compounds_and_graphs_html).

![bSpline_nodes](https://github.com/domrab/Bifrost_dhCurves/assets/58582379/66c73fe1-0ea7-46be-91ad-c5317272ee11)
Update 1:
![bSpline_nodes2](https://github.com/domrab/Bifrost_dhCurves/assets/58582379/3968e2f6-8989-4ddc-bfa7-3fc1226f4b2a)

---

# construct_bSpline
Construct a bSpline object from it's control points, the degree, and optionally a knot vector.

### Inputs

<b>`control_points [in]`</b>\
The input control points for bSpline.

<b>`degree [in]`</b>\
The degree.

<b>`knots [in] (optional)`</b>\
The knot vector. This is optional. If nothing is provided, a default knot vector gets assigned.

<b>`remap_range [in]`</b>\
If no knot vector is supplied, the default range is 0 to spans. If `remap_range` is true, the `min` and `max` input values get used.

<b>`min [in]`</b>\
Default start value for generated knot vector if it's not supplied.

<b>`max [in]`</b>\
Default end value for generated knot vector if it's not supplied.

### Outputs

<b>`bSpline [out]`</b>\
The resulting bSpline object.

---

# knot_vector
Construct a knot vector with the proper multiplicity.

### Inputs

<b>`cv_count [in]`</b>\
The number of cvs for which this knot vector will be used.

<b>`degree [in]`</b>\
The degree of the bSpline (determines the multiplicity).

<b>`remap_range [in]`</b>\
The default range is 0 to spans. If `remap_range` is true, the `min` and `max` input values get used.

<b>`min [in]`</b>\
Default start value for generated knot vector if it's not supplied.

<b>`max [in]`</b>\
Default end value for generated knot vector if it's not supplied.

### Outputs

<b>`knots [out]`</b>\
The output knot vector

---

# parameter_array
Similar to the native `sequence_array` node but instead of a start and step size, this takes creates `size` samples between `start` and `end` inclusive.

### Inputs

<b>`size [in]`</b>\
The number of parameters.

<b>`start [in]`</b>\
The first value in the parameter array.

<b>`end [in]`</b>\
The last value in the parameter array.

### Outputs

<b>`parameters [out]`</b>\
The parameter array.

---

# bSpline_scope
An easy visualization compound for bSplines.
> [!NOTE]  
> It appears for a zero-degree bSpline the visualization is off. As far as I understand, a p=0 bSpline is stepped. Given the visualization through one strand connecting all the CVs, the stepping will be invisible as the actual bSpline parameters are all lying on the points themselves. Thus a zero-degree bSpline visualized will look like a first-degree bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to visualize.

<b>`steps_per_span [in]`</b>\
The number of sample steps per span. Maya's nurbs equivalent of this is 4 or 16 depending if subdivision preview is turned on.

<b>`color [in]`</b>\
The visualization color.

<b>`shape [in]`</b>\
The shape, this corresponds to the shape on the strand shape.

<b>`thickness [in]`</b>\
The thickness of the shape, only applicable when `shape` is `tube`.

<b>`screen_aligned [in]`</b>\
If the shape is screen aligned, only applicable when `shape` is `tube`.

### Outputs

<b>`strands [out]`</b>\
The strands created from the bSpline for visualization purposes.

---

# get_d1_bSpline_length (internal)
Calculate the accurate length of a degree 1 bSpline curve

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to get the length from.

<b>`custom_range [in]`</b>\
If true, the length is calculated on a subsection of the curve.

<b>`min [in]`</b>\
The start parameter of the sub curve.

<b>`max [in]`</b>\
The end parameter of the sub curve.

### Outputs

<b>`length [out]`</b>\
The accurate length.

<b>`sample_positions [out]`</b>\
The sampled positions used to calculate the length.

---

# get_dN_bSpline_length (internal)
Calculate the approximate length of a bSpline of any degree.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to get the length from.

<b>`steps [in]`</b>\
The total number of substeps used to estimate the length.

<b>`custom_range [in]`</b>\
If true, the length is calculated on a subsection of the curve.

<b>`min [in]`</b>\
The start parameter of the sub curve.

<b>`max [in]`</b>\
The end parameter of the sub curve.

### Outputs

<b>`length [out]`</b>\
The approximate length.

<b>`sample_positions [out]`</b>\
The sampled positions used to calculate the length.

---

# get_bSpline_length
Get the length of a given (sub) bSpline. The result will be accurate for a degree 1 spline but always smaller than the real length for any bSpline of degree greater than 1. 

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to get the length from.

<b>`custom_range [in]`</b>\
If true, the length is calculated on a subsection of the curve.

<b>`min [in]`</b>\
The start parameter of the sub curve.

<b>`max [in]`</b>\
The end parameter of the sub curve.

<b>`steps [in]`</b>\
The total number of substeps used to estimate the length.

<b>`color [in]`</b>\
The visualization color.

<b>`shape [in]`</b>\
The shape, this corresponds to the shape on the strand shape.

<b>`thickness [in]`</b>\
The thickness of the shape, only applicable when `shape` is `tube`.

<b>`screen_aligned [in]`</b>\
If the shape is screen aligned, only applicable when `shape` is `tube`.

### Outputs

<b>`length [out]`</b>\
The approximate length.

<b>`strands [out]`</b>\
The strands created from the bSpline for visualization purposes.

---

# deconstruct_bSpline
Deconstruct a bSpline into it's components.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to query.

### Outputs

<b>`cvs [out]`</b>\
The control points.

<b>`cv_count [out]`</b>\
The control point count.

<b>`degree [out]`</b>\
The degree.

<b>`knots [out]`</b>\
The knot vector.

<b>`min [out]`</b>\
The minimum value in the knot vector.

<b>`max [out]`</b>\
The maximum value in the knot vector.

---

# get_bSpline_cvs
Get control point info from a bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to query.

### Outputs

<b>`cvs [out]`</b>\
The control points.

<b>`cv_count [out]`</b>\
The control point count.

---

# get_bSpline_degree
Get the degree info from a bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to query.

### Outputs

<b>`degree [out]`</b>\
The degree.

---

# get_bSpline_knots
Get the knot vector info from a bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to query.

### Outputs

<b>`knots [out]`</b>\
The knot vector.

<b>`min [out]`</b>\
The minimum value in the knot vector.

<b>`max [out]`</b>\
The maximum value in the knot vector.

---

# deBoor (internal)
Simple deBoor implementation to sample a bSpline. While slower than the matrix representation of bSplines, I found this to produce an output matching Maya NURBS curves.

### Inputs

<b>`c__cvs [in]`</b>\
The control point array.

<b>`p__degree [in]`</b>\
The degree of the curve.

<b>`t__knots [in]`</b>\
The knot vector.

<b>`x__parameter [in]`</b>\
The parameter to query at.

<b>`k__span [in]`</b>\
The span in which the parameter lies.

### Outputs

<b>`position [out]`</b>\
The calculated output position.

---

# find_span (internal)
Find the span for the deBoor algorithm from a given parameter and the knot vector.

### Inputs

<b>`parameter [in]`</b>\
The parameter to find the span for.

<b>`knots [in]`</b>\
The knot vector of the bSpline.

### Outputs

<b>`parameter_clamped [out]`</b>\
The parameter clamped in the valid knot vector range.

<b>`span [out]`</b>\
The span in which the parameter lies.

---

# sample_bSpline
Sample a bSpline at a given parameter

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to query.

<b>`parameter [in]`</b>\
The parameter to sample the bSpline at.

### Outputs

<b>`position [out]`</b>\
The sampled position.

---

# sample_bSpline_per_span
Sample a bSpline several times at each span at equally spaced parameter intervals.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to query.

<b>`steps [in]`</b>\
The number of parameter steps per span.

### Outputs

<b>`positions [out]`</b>\
The sampled positions.

<b>`parameters [out]`</b>\
The parameters at which the positions got sampled.

---

# reparameterize_bSpline
Reparameterize a given bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to resample.

<b>`samples [in]`</b>\
The number of samples per span. This uses `sample_bSpline_per_span` under the hood.

<b>`degree [in]`</b>\
The desired output degree. As a higher order bSpline tends to shift 'inwards' of the CVs and the CVs get sampled on the existing bSpline, a higher number of `samples` is required to maintain the shape as best as possible.

<b>`remap_range [in]`</b>\
If false, the range of the input bSpline is used. If `remap_range` is true, the `min` and `max` input values get used.

<b>`min [in]`</b>\
Start value for new bSpline.

<b>`max [in]`</b>\
End value for new bSpline.

### Outputs

<b>`new_bSpline [out]`</b>\
The reparameterized bSpline.

---

# compute_bSpline_derivative
Compute the n-th derivative of a given bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to compute the derivative of. Must be at least first-degree.

<b>`order [in]`</b>\
The n-th order derivative. This value internally gets clamped between 1 and `bSpline.degree`.

### Outputs

<b>`derivative_bSpline [out]`</b>\
The derivative bSpline.

<b>`derivative_cvs [out]`</b>\
The derivative control points.

<b>`derivative_degree [out]`</b>\
The derivative degree.

<b>`derivative_knots [out]`</b>\
The derivative knots.

---

# measure_linear_curve
Utility to measure the distances along a linear curve (array of 3D points).

### Inputs

<b>`control_points [in]`</b>\
The control points.

### Outputs

<b>`lengths [out]`</b>\
An array containing the length of each segment.

<b>`cumulative [out]`</b>\
An array containing the cumulative length for each segment.

<b>`total [out]`</b>\
The total length of the curve (equivalent to the last value in cumulative).

---

# bSpline_parameter_scope
For easy visualization of parameters on a bSpline.

### Inputs

<b>`bSpline [in]`</b>\
The bSpline to sample the parameters on.

<b>`parameters [in]`</b>\
The parameters to sample.

<b>`color [in]`</b>\
The visualization color.

<b>`shape [in]`</b>\
This corresponds to the shape on the point shape. Do not use `numeric` as I did not provide a way to specify the property name.

<b>`size [in]`</b>\
The size of the shape. Not applicable when `shape` is `point`.

<b>`screen_aligned [in]`</b>\
If the shape is screen aligned. Not applicable when `shape` is `point`.

### Outputs

<b>`points [out]`</b>\
The points created for visualization purposes.

---

# matrix_from_bSplines
Given a main and up bSpline curves and a parameter, this calculates a no-scale, no-shear matrix. Currently limited to +X pointing towards the increasing parameter value and +Y to the sampled location on the up curve.

### Inputs

<b>`bSpline_main [in]`</b>\
The main curve.

<b>`bSpline_up [in]`</b>\
The up curve. The CVs and the degree of this node get used together with the min/max knot values from `bSpline_main` to construct a curve that has the same valid sample space.

<b>`parameters [in]`</b>\
The parameter at which both bSplines get sampled.

### Outputs

<b>`matrix [out]`</b>\
The output matrix.
