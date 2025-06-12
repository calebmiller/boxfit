# boxfit:

**boxfit** is a fitting algorithm designed to account for uncertainites arising from detector resolution that result in no or unusual minimization. Unlike traditional methods that treat each "hit" as a point with associated uncertainties, boxfit models each hit as a 3D volume of equal likelihood. This approach provides a more realistic representation of spatial uncertainty in low-resolution tracking detectors.

## Installation

You can install boxfit using pip:

```
pip install boxfit
```

## Example Usage
boxfit is initialized with a detector geometry and then can be passed a list of hits to try and fit a track

```
from boxfit import boxfit as bf

# Define a basic geometry
x_weights = [0.5,1,1,0.5] #weight of each box in x
y_weights = [1] #non-specified values are set to [1]

x_step = 1 #stepsize in arbitrary units of each box. i.e. 1cm

orient = ['x','x'] #detector has two layers, both aligned in x
space = [10] #spacing between layers. len(space)-1 should = len(orient)

# Initialize boxfit with your geometry
myfit = bf(spacing=space, l_weights=x_weights, l_step=x_step,orientation=orient,spacing=space)

# Provide your list of hits 
hits = [[5,1,0],[4,2,10]] #arbitrary numbers, ordered in [x,y,z]  

# Perform the fit
score = myfit.fit(hits)

# Output the fit score
print(score) #output is [[meanx, meany, meanz, mean_thetax, mean_thetay],[5x5 covariance]]
```

