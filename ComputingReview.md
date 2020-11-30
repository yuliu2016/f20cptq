## 1P13 Fall 2020 Computing Review Questions

Questions authored by: peg#9672



**Question 1**: Consider the following function that takes a string polynomial expression in the form of `ax^c + bx^d + ...` and returns its derivative using the power rule:

```python
def polynomial_derivative(poly):
    """Compute the derivative of a polynomial expression"""
    
    # Split the polynomial expression by the plus sign
    terms = poly.split("+")
    
    # Start with an empty list for the derivative terms
    deriv_terms = []
    
    for term in terms:
        # Remove extra spaces around the term
    	term_stripped = term.strip()
    	
    	# Find where x^ is in the expression, and extract
    	# the coefficient and exponent from before and after
    	index_of_x = term_stripped.index("x^")
    	coefficient = int(term_stripped[:index_of_x])
    	exponent = int(term_stripped[index_of_x + 2:])
    	
    	# Apply the power rule
    	deriv_coeff = coefficient * exponent
    	deriv_exp = exponent - 1
    	
        # Add a new derivative term to the list
    	deriv_term = str(deriv_coeff) + "x^" + str(deriv_exp)
    	deriv_terms.append(deriv_term)
    
    # Join all the terms of the derivatives with a plus sign
    return " + ".join(deriv_terms)
```
For example, `polynomial_derivative("5x^4 + 3x^3")` will return `"20x^3 + 9x^2"`. This implementation however does not handle many common cases, resulting in errors. Which one of the following function calls computes the derivative correctly?

**A.** `polynomial_derivative("9x^7 + 4x")`
**B.** `polynomial_derivative("-3x^11+5x^-2")`
**C.** `polynomial_derivative("x^6 + \n4x^3")`
**D.** `polynomial_derivative("7x^5 + 6*x^4")`
**E.** `polynomial_derivative("1.3x^8+5x^0")`



**Question 2:** Consider the following function meant to change the order of items in a list by comparing the their values:

```python
def change_order(items):
    """Change the order of a list using the insertion sort algorithm"""
    
    # Iterate from 1 to length of items - 1
    # Starting from 1 because if i is 0, nothing
    # is compared and nothing would happen
    for i in range(1, len(items)):
        # Get the key value to be compared
        key = items[i] 
  
        # Move elements of items[0:i - 1], that are 
        # smaller than key, to one position ahead 
        # of their current position.
        j = i - 1
        while j >= 0 and key > items[j]:
            items[j + 1] = items[j] 
            j -= 1
        
        # Insert key into the position that is now empty
        items[j + 1] = key 

# testing the change_order function
test_items = [1, 6, 4, 5, -3]
change_order(test_items)
```

What are the contents of `test_items` after `change_order` is called?

**A.** Nothing changed. `test_items` has a different scope as the parameter `items` in `change_order` and therefore its contents are not changed.
**B.** The function `change_order` would raise an IndexError and terminate the program
**C.** `[-3, 5, 4, 6, 1]`
**D.** `[-3, 1, 4, 5, 6]`
**E.** `[6, 5, 4, 1, -3]`
**F.** `[1, -3, 4, 5, 6]`
**G.** `[6, 5, 4, -3, 1]`



**Question 3**: Consider the following function that calculates the total moment of inerta of a system of particles, based on a list of information about each particle. Each item of the list is a sub-list in the form of `[mass, distance from origin, angle radians from axis]`. All three values are floating-point numbers.  The moment of inertia for a single particle is `mr^2`, where `r` is the perpendicular distance from the axis of rotation.

```python
import math

def calculate_moi(particles):
    """Calculate the total moment of inertia for a system of particles"""
    # TODO Implementation code here
```



What is a correct implementation of this function?

**A.** 

```python
i = 0
total_moi = 0
while i < len(particles):
    i += 1
    mass, dist, angle = particles[i]
    r = math.sin(angle) * dist
    total_moi += mass * r ** 2
return total_moi
```

**B.** 

```python
particle_moments = []
for mass, dist, angle in particles:
    r = math.sin(angle) * dist
    particle_moment = (mass * r) ** 2
    particle_moments.append(particle_moment)
return sum(particle_moments) / len(particle_moments)
```

**C.** 

```python
total_moi = 0
for particle in particles:
    mass = particle[0]
    dist = particle[1]
    angle = particle[2]
    r = math.sin(angle) * dist
    total_moi += mass * r ** 2
	return total_moi
```

**D.** 

```python
total_moi = 0
for mass, dist, angle in particles:
    r = math.sin(angle) * dist
    total_moi += mass * r ** 2
return total_moi
```

**E.** 

```python
i = 0
total_moi = 0
while i < len(particles)
    mass, dist, angle = particles[i]
    r = math.sin(angle) * dist
    total_moi += mass * r ** 2
    i += 1
return total_moi
```



**Question 4**: Consider the following function that estimates the area under a graph using right endpoints.

```python
def estimate_area(func, low, high, num_rects):
    """Estimate the net area under a graph using right endpoints"""
    # Assumption: func is a function of x, low < high, and num_rects > 0
    
    # Calculate the width of a single rectangle,
    # based on the total number of rectangles
    delta_x = (high - low) / num_rects
    
    # The sum of the areas of all rectangles
    area_sum = 0

    for i in range(num_rects):
    
    	# Calculate the x value of the right endpoint
        x = low + (i + 1) * delta_x
        
        # Evaluate the function, using x implicitly
        y = eval(func)
        
        # Add the area of the rectangle to the sum
        area_sum += y * delta_x

    return area_sum
```

What is the best way to change this function, so that it estimates the area using left endpoints instead?

**A.** Nothing. This implementation can already estimate using left endpoints.
**B.** Change `x = low + (i + 1) * delta_x` into `x = low + i * delta_x`
**C.** Change `x = low + (i + 1) * delta_x` into `x = low + (i - 1) * delta_x`
**D.** Change `for i in range(num_rects)` into `for i in range(1, num_rects + 1)`
**E.** Change `for i in range(num_rects)` into `for i in range(num_rects, 0, -1)`
**F.** Change `area_sum = 0` into `area_sum = -delta_x`
**G.** There is no easy way to do it; the above code should not be reused

















**Question 5**: Consider the following function that checks whether an electron's orbital and spin combination is valid. 

```python
def is_orbital_valid(N, L, ML, MS):
    "Check if a set of the 4 quantum numbers makes a valid orbital and spin"
    
    if N < 1: return False
    else:
    	if L < 0: return False
        elif L >= N: return False
        else:
            if ML < -L: return False
            elif ML > L: return False
            else:
                if MS == 0.5: return True
                elif MS == -0.5: return True
                else: return False
```

This code works as expected, but is very verbose and can be simplified to a single `return` statement. Which of the following is the correct simplified expression that is equivalent to the above function?

**A.** `return N >= 1 or 0 <= L < N or -L < ML < L or MS in [-0.5, 0.5]`
**B.** `return N >= 1 and 0 <= L < N and -L < ML < L and MS == -0.5 or MS == 0.5`
**C.** `return N >= 1 and 0 <= L < N and -L < ML < L and MS in [-0.5, 0.5]`
**D.** `return N >= 1 and 0 <= L or N > L and ML > -L or ML < L and MS == -0.5 or MS == 0.5`
**E.** `return not (N < 1 or L < 0 or L >= N or ML < -L or ML > L or MS in [-0.5, 1.5])`

**F.** `return not (N < 1 or L < 0 or L >= N or ML < -L or ML > L and MS in [-0.5, 1.5])`

























**Question 6:** All sensors, including EMG sensors, vision sensors, and encoders (used to measure amount of rotation in robotic arms) have some sensor noise when used in real life that can mess up the measured values. To mitigate this, a rolling average can be used. Consider the following function that uses a global variable to keep track of the average measurement over the last 10 measurements.

```python
import time

prev_measurements = []
prev_time = 0.0 # UNIX timestamp in seconds
MIN_TIME_DELTA = 0.02 # seconds

def get_rolling_average(new_measurement):
    """Compute the rolling average over the last 10 measurements"""
    global prev_time
    
    # Get the time in seconds, and keep track of the previous time
    curr_time = time.time()
    time_delta = curr_time - prev_time
    prev_time = curr_time
    
    # Only add the measurements to the rolling average
    # if the time delta is large enough, otherwise
    # replace the last value
    if time_delta < MIN_TIME_DELTA:
        # Check if the list is empty before replacing the value
        if prev_measurements:
            prev_measurements[-1] = new_measurement
        else:
            prev_measurements.append(new_measurement)
    else:
        # Add new_measurement to the end of the list,
        # but if the total exceeds 10 measurements, remove
        # the oldest one from the list to keep the average
        # measurement up to data
        
        # TODO missing code here
        pass
    
    # List is updated; Now return the average
    return sum(prev_measurements) / len(prev_measurements)
```

Which of the following is the correct missing code?

**A.** `prev_measurements[len(prev_measurements) - 1] = new_measurement`

**B.** `prev_measurements[0] = new_measurement`

**C.**

```python
prev_measurements.append(new_measurement)
if len(prev_measurements) >= 10:
    prev_measurements.pop(0)
```

**D.**

```python
prev_measurements.append(new_measurement)
if len(prev_measurements) > 10:
    prev_measurements.remove(0)
```

**E.**

```python
prev_measurements.append(new_measurement)
if len(prev_measurements) > 10:
    del prev_measurements[0]
```

**F.**

```python
prev_measurements.insert(0, new_measurement)
if len(prev_measurements) >=:
    prev_measurements.pop()
```
