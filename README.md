# Geostatistical linear models (geolm's) in Julia

## Installation

```julia
Pkg.add("GeoLM")
```
will install this package (eventually, I hope)

The `GeoLM` package also depends on the `StatsBase` package.

# Examples

Create a response (y) and matrix of covariates (x).
```julia
julia> x1  = [4.17,5.58,5.18,6.11,4.50,4.61,5.17,4.53,5.33,5.14];

julia> y = [4.81,4.17,4.41,3.59,5.87,3.83,6.03,4.89,4.32,4.69];

julia> a = [1, 1, 1, 1, 1, 1, 1, 1, 1, 1];

julia> x = reshape([a, x1], 10, 2);
```
Fit minimal linear model (method = "qr" default).  **minlmfit** returns a **MinLmfit** type object.

```julia
julia> mylm = minlmfit(x, y);
```
Extract characteristics of interest from **MinLmfit** object.  **corr** extracts the scaled covariance matrix of the estimated regression coefficients, i.e., inv(x'*x).

```julia
julia> coef(myfit)
2-element Array{Float64,1}:
  7.79571 
 -0.622956

julia> residuals(myfit)
10-element Array{Float64,1}:
 -0.387988 
 -0.14962  
 -0.158803 
 -0.399454 
  0.877587 
 -1.09389  
  1.45497  
 -0.0837238
 -0.155359 
  0.0962792

julia> resid(myfit)
10-element Array{Float64,1}:
 -0.387988 
 -0.14962  
 -0.158803 
 -0.399454 
  0.877587 
 -1.09389  
  1.45497  
 -0.0837238
 -0.155359 
  0.0962792

julia> corr(myfit)
2x2 Array{Float64,2}:
  8.37495  -1.64447 
 -1.64447   0.326802
```


