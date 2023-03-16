- [Go back](README.md)

# Returning by Pointer
> Stephen Hamilton  
> 3-1-2023

C can only return a single variable.
However, there are certain cases where it's useful for a function
to return multiple values

For example, let's say we want to make a function that converts cartesian
coordinates to polar coordinates. We can do this with return by pointer,
like so:
```c
#include <math.h>

void cartesianToPolar(double x, double y, double* r, double* theta)
{
    *r = sqrt(x * x + y * y);
    *theta = atan2(y, x);
    *theta = *theta * 180 / M_PI; // Convert to degrees
}
```
Then, the calling function would do this to get both return values:
```c
double r;
double theta;
cartesianToPolar(3.0, 4.0, &r, &theta);
printf("r = %lf, theta = %lf\n", r, theta);
```
Output:
```
r = 5.000000, theta = 53.130102
```

- [Go back](README.md)
