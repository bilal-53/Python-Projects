import math


#Unchanging values
ONE_METER_IN_FEET = 3.28
DENSITY = 1.225
MASS_1 = 100000
BURNING_FUEL_1 = 1360
MASS_2 = 400000
BURNING_FUEL_2 = 2000
BURNING_FUEL_3 = 2721
COST_METAL = 5
COST_FUEL = 6.1
TAX_QUEBEC = 115/100
MIN_WEIGHT_BOX = 20
MAX_WEIGHT_BOX = 500
MIN_VOLUME_BOX = 0.125
MAX_PERCENTAGE_WEIGHT = 0.05
MAX_PERCENTAGE_VOLUME = 0.40
ACCELERATION_GRAVITY = 9.81


def feet_to_meter(length_f):
    '''
    Converts a given length in feet to meters
    
    Parameter:
        length_f (positive float): given length in feet
    
    Returns:
        length_m (positive float): The converted length (in meters)
    
    Examples:
    
    >>> feet_to_meter(5.0)
    1.52
    
    >>> feet_to_meter(678.9)
    206.98
    
    >>> feet_to_meter(19998.98)
    6097.25
    '''
    # Converts a length from feet to meters
    length_m = round(length_f / ONE_METER_IN_FEET, 2)
    return length_m

def rocket_volume(radius, height_cone, height_cyl):
    '''
    Computes the volume of a rocket
    
    Parameters:
        radius (positive float): radius of the cylinder\
        (and the base of the cone)(in meters)
        height_cone (positive float): height of the cone (in meters)
        height_cyl (positive float): height of the cylinder
    
    Returns:
        rocket_volume (positive float): the volume of the rocket\
        (cylinder+cone)(in m**3)
    
    Examples:
    >>> rocket_volume(13.4, 17.6, 3.9)
    5509.42
    
    >>> rocket_volume(16.3, 34.2, 42.3)
    44822.84
    
    >>> rocket_volume(9.4, 6.8, 3.2)
    1517.5
    '''
    # Calculates the volume of the rocket (cone + cylinder)
    volume_cone = math.pi * radius ** 2 * height_cone / 3
    volume_cyl = math.pi * radius ** 2 * height_cyl
    volume_rocket = round(volume_cone + volume_cyl, 2)
    return volume_rocket

def rocket_area(radius, height_cone, height_cyl):
    '''
    Calculates the surface area of a rocket
   
    Parameters:
        radius (positive float): radius of the cylinder\
        (and the base of the cone) (in meters)
        height_cone (positive float): height of the cone (in meters)
        height_cyl (positive float): height of the cylinder (in meters)
    
    Returns:
        rocket_area (positive float): the surface area of the rocket (in m**2)
    
    Examples:
    
    >>> rocket_area(13.4, 17.6, 3.9)
    1823.68
    
    >>> rocket_area(2.8, 9.6, 4.3)
    188.24
    
    >>> rocket_area(1.6, 7.8, 8.9)
    137.54
    '''
    # Determines the total surface area of a rocket
    area_cone = math.pi * radius *\
    (radius + math.sqrt(height_cone ** 2 + radius ** 2))
    area_cyl = 2 * math.pi * radius * (height_cyl + radius)
    area_circle = math.pi * radius ** 2
    area_rocket = round(area_cone + area_cyl - 2 * area_circle, 2)
    return area_rocket

def rocket_mass(radius, height_cone, height_cyl):
    '''
    Calculates the mass of a rocket
    
    Parameters:
        radius (positive float): radius of the cylinder\
        (and the base of the cone)(in meters)
        height_cone (positive float): height of the cone (in meters)
        height_cyl (positive float): height of the cylinder (in meters)
    
    Returns:
        rocket_mass (positive float): the total mass of the rocket (in kg)
    
    Examples:
    
    >>> rocket_mass(13.4, 17.6, 3.9)
    6749.04
    
    >>> rocket_mass(6.9, 3.4, 5.8)
    1270.36
   
    >>> rocket_mass(19.8, 34.5, 65.7)
    116475.24
    '''
    #Computes the mass of a rocket based on its volume and density
    mass_rocket = round (DENSITY *\
    rocket_volume(radius, height_cone, height_cyl), 2)
    return mass_rocket

def rocket_fuel(radius, height_cone, height_cyl, velocity_e, velocity_i, time):
    '''
    Calculates the amount of fuel a rocket needs
    
    Parameters:
        radius (positive float): radius of the cylinder\
        (and the base of the cone)(in meters)
        height_cone (positive float): height of the cone (in meters)
        height_cyl (positive float): height of the cylinder (in meters)
        velocity_e (positive float): exhaust velocity of the rocket\
        (in meters per seconds)
        velocity_i (positive float): initial velocity of the rocket\
        (in meters per seconds)
        time (positive float): time corresponding to the amount of fuel\
        the rocket needs (in seconds)
    
    Returns:
        rocket_fuel (positive float): the total fuel needed (in kg)
    
    Examples:
    
    >>> rocket_fuel(11.2, 51.8, 105.7, 123.45, 99.65, 81.94)
    185145.0
    
    >>> rocket_fuel(13.8, 3987.6, 11948.7, 10876.9, 4398.7, 3876.9)
    15399295.07
    
    >>> rocket_fuel(18.9, 37.6, 48.7, 76.9, 98.7, 38.9)
    272540.36   
    '''
    # Estimates the amount of fuel required for the rocket's launch
    mass_fuel_launch = rocket_mass(radius, height_cone, height_cyl) *\
    (math.e ** (velocity_i / velocity_e) - 1)
    if rocket_mass(radius, height_cone, height_cyl) < MASS_1:
        
        mass_fuel_burn = BURNING_FUEL_1 * time
        
    elif rocket_mass(radius, height_cone, height_cyl) < MASS_2:
        
        mass_fuel_burn = BURNING_FUEL_2 * time
        
    else:
        
        mass_fuel_burn = BURNING_FUEL_3 * time
    fuel_rocket = round(mass_fuel_launch + mass_fuel_burn, 2)      
    return fuel_rocket

def calculate_cost(radius, height_cone, height_cyl, velocity_e,\
velocity_i, time, tax):
    '''
    Calculates the cost of building and launching a rocket
    
    Parameters:
        radius (positive float): radius of the cylinder\
        (and the base of the cone)(in meters)
        height_cone (positive float): height of the cone (in meters)
        height_cyl (positive float): height of the cylinder (in meters)
        velocity_e (positive float): exhaust velocity of the rocket\
        (in meters per seconds)
        velocity_i (positive float): initial velocity of the rocket\
        (in meters per seconds)
        time (positive float): time corresponding to the amount of fuel\
        the rocket needs (in seconds)
        tax (boolean): whether or not there are taxes in the calculation    
    
    Returns:
        cost (positive float): the total cost of building and\
        launching this rocket (in $)
    
    Examples:
   
    >>> calculate_cost(50.0, 100.0, 800.0, 700.0, 300.0, 120.0, False)
    29544028.78
   
    >>>  calculate_cost(174.9, 5.8, 1057.9, 153.4, 96.8, 81.4, True)
    779163825.82
    
    >>>  calculate_cost(1732.9, 51828.7, 1057.32, 140.9, 94.5, 33.8, True)
    1422030275406.94
    '''
    # Calculates the overall cost of building and launching a rocket
    if tax == 0: # If we don't consider the taxes
        
        cost = round(COST_METAL * rocket_area(radius, height_cone, height_cyl)\
        + COST_FUEL * rocket_fuel(radius, height_cone, height_cyl, velocity_e,\
        velocity_i, time),2) 
    elif tax == 1: # If we consider the taxes
        
        cost = round(TAX_QUEBEC * (COST_METAL * \
        rocket_area(radius, height_cone, height_cyl) + \
        COST_FUEL * rocket_fuel(radius, height_cone, height_cyl,\
        velocity_e, velocity_i, time)), 2)
    return cost

def compute_storage_space(radius, height_cyl):
    '''
    Computes the dimensions of the rectangular storage box
    
    Parameters:
        radius (positive float): radius of the rocket (in meters)
        height_cyl (positive float): height of the cylinder (in meters)
    
    Returns:
        storage_space_width (positive float): \
        width of the storage box (in meters)
        storage_space_length (positive float): \
        length of the storage box (in meters)
        storage_space_height (positive float): \
        height of the storage box (in meters)
    
    Examples:
    
    >>> compute_storage_space(25.6, 94.3)
    (36.2, 36.2, 47.15)
    
    >>> compute_storage_space(345.9, 459.7)
    (489.18, 489.18, 229.85)
    
    >>> compute_storage_space(18325.9, 34432.8)
    (25916.74, 25916.74, 17216.4)
    '''
    # Determines the dimensions of a rectangular storage box
    storage_space_width = storage_space_length =\
    round(math.sqrt(2) * radius, 2)
    storage_space_height = round(height_cyl/2, 2)
    return storage_space_width,\
    storage_space_length, storage_space_height

def load_rocket(initial_weight, radius, height_cyl):
    '''
    Simulates loading items into a rocket's storage

    Parameters:
    initial_weight (positive float): initial weight\
    of the rocket (in kg)
    radius (positive float): radius of the rocket (in meters)
    height_cyl (positive float): height of the cylinder (in meters)

    Returns:
    
    total_rocket_weight (positive float): rounded weight\
    of the rocket after loading items
    
    Examples:
    
    >>> load_rocket(10000.0, 1.0, 1.0)
    Please enter the weight of the next item\
    (type "Done" when you are done filling the rocket): 20.0
    Enter item width: 1.0
    Enter item length: 0.3
    Enter item height: 1.0
    No more items can be added
    10020.0
    
    >>> load_rocket(56.5, 34.0, 98.0)
    No more items can be added
    56.5
    
    >>> load_rocket(3455.9, 546.7, 564.3)
    Please enter the weight of the next item \
    (type "Done" when you are done filling the rocket): 267.5
    Enter item width: 3.0
    Enter item length: 3.0
    Enter item height: 3.0
    Item could not be added... please try again...
    Please enter the weight of the next item\
    (type "Done" when you are done filling the rocket): 34.5
    Enter item width: 3.0
    Enter item length: 2.0
    Enter item height: 2.0
    Please enter the weight of the next item\
    (type "Done" when you are done filling the rocket): Done
    3490.4
    '''
    
    # Compute the volume of the storage space by calling the\
    # function compute_storage_space 
    width, length, height = \
    compute_storage_space(radius, height_cyl)
    storage_volume = width * length * height
    
    # Set the maximum allowable weight and volume for the items
    MAX_WEIGHT = initial_weight * MAX_PERCENTAGE_WEIGHT
    MAX_VOLUME = storage_volume * MAX_PERCENTAGE_VOLUME
    
    # Check if the rocket can hold any items 
    if (MAX_WEIGHT < MIN_WEIGHT_BOX) or (MAX_VOLUME < MIN_VOLUME_BOX):
        
        print('No more items can be added')
        return round(initial_weight, 2)
    
    else:
        
        # Initialize total weight and volume of the loaded items
        total_weight_items, total_volume_boxes = 0, 0
        weight_item = input('Please enter the weight of the next \
item(type "Done" when you are done filling the rocket): ')
        
        while (weight_item != 'Done'):
            
            # Ask the user for item weight, dimensions,\
            # and calculate the box volume
            weight_item = float(weight_item)
            width_item = float(input('Enter item width: '))
            length_item = float(input('Enter item length: '))
            height_item = float(input('Enter item height: '))
            volume_box = width_item * length_item * height_item
            total_weight_items += weight_item
            total_volume_boxes += volume_box
            
            # Check if the item exceeds weight constraints
            if (weight_item > MAX_WEIGHT_BOX or weight_item < MIN_WEIGHT_BOX)\
            or (total_weight_items > MAX_WEIGHT):
                
                print('Item could not be added... please try again...')
                total_weight_items -= weight_item # Undo the weight addition
                total_volume_boxes -= volume_box # Undo the volume addition
                weight_item = input('Please enter the weight of the next \
item (type "Done" when you are done filling the rocket): ')
                
            # Check if the item exceeds volume constraints
            elif (volume_box < MIN_VOLUME_BOX) or\
            (total_volume_boxes > MAX_VOLUME):
                
                print('Item could not be added... please try again...')
                total_weight_items -= weight_item
                total_volume_boxes -= volume_box
                weight_item = input('Please enter the weight of the next \
item (type "Done" when you are done filling the rocket): ')
                
            # Check if remaining space or weight can hold another box   
            elif (MAX_WEIGHT - total_weight_items < MIN_WEIGHT_BOX)\
            or (MAX_VOLUME - total_volume_boxes < MIN_VOLUME_BOX):
                
                print('No more items can be added')
                weight_item = 'Done'
                 
            # Prompt for the next item if constraints are not violated    
            else:
                
                weight_item = input('Please enter the weight of the next \
item (type "Done" when you are done filling the rocket): ')
                
        # Return the total rocket weight         
        total_rocket_weight = initial_weight + total_weight_items
        return round(total_rocket_weight, 2)


def projectile_sim(simulation_time, interval, v0, angle):
    '''
    Simulates the projectile motion of a rocket and prints \
    its height at regular time intervals.
    
    Parameters:
        simulation_time (positive int) : time for which \
        the simulation will run (in seconds).
        interval (positive int) : time interval between \
        each data point (in seconds).
        v0 (positive float) : initial velocity of \
        the rocket (in meters per second).
        angle : (positive float) : launch angle of the rocket\
        (in degrees).
    
    Returns:
    None

    Examples:

    >>> projectile_sim(10, 1, 50.0, 0.79)
    0.0
    30.61
    51.42
    62.41
    63.59
    54.96
    36.53
    8.28
    
    >>> projectile_sim(30, 3, 140,6.57)
    0.0
    74.67
    61.05
    
    >>> projectile_sim(330, 6, 200, 13.6)
    0.0
    854.41
    1355.67
    1503.76
    1298.7
    740.47
    '''
    # Prints the intial height of zero 
    print(0.0)
    
    # We want to know the height of the rocket at  regular time intervals
    for time in range (0, simulation_time + 1, interval):
        height = (-1/2 * ACCELERATION_GRAVITY * time ** 2 +\
v0 * math.sin(angle) * time)
        
        # All not positive or zero height after the
        # initial one are not printed
        if height <= 0:
            time = time + interval
            
        # Prints the positive heights
        else:
            print(round(height, 2))
            time = time + interval

    
    
    
        
def rocket_main():
    '''
    Launch a projectile simulation with several informations
    
    Parameter:
    None
    
    Returns:
    None
    
    Example :
    >>> rocket_main()
    Welcome to the Rocket Simulation!
    Enter the rocket radius in feet: 50.0
    Enter the rocket cone height in feet: 100.0
    Enter the rocket cylinder height in feet: 200.0
    Enter the exhaust velocity for the upcoming trip: 700.0
    Enter the initial velocity for the upcoming trip: 300.0
    Enter the angle of launh for the upcoming trip: 0.8
    Enter the length of the upcoming trip: 1000.0
    Would you like to factor in tax? 1 for yes, 0 for no: 1
    This trip will cost $9826238.52
    Please enter the weight of the next \
item (type "Done" when you are done filling the rocket): 100.0
    Enter item width: 5.0
    Enter item length: 5.0
    Enter item height: 5.0
    Please enter the weight of the next \
item (type "Done" when you are done filling the rocket): Done
    The rocket and its equipment will weigh 63690.19 kg
    Enter the simulation total time: 8
    Enter the simulation interval: 2
    Now simulating the rocket trajectory:
    0.0
    410.79
    782.35
    1114.66
    1407.73
    '''
    # Ask the user for informations about the trip
    print('Welcome to the Rocket Simulation!')
    radius_f = float(input('Enter the rocket radius in feet: '))
    height_cone_f = float(input('Enter the rocket cone height in feet: '))
    height_cyl_f = float(input('Enter the rocket cylinder height in feet: '))
    velocity_e = float(input('Enter the exhaust velocity for the \
upcoming trip: '))
    velocity_i = float(input('Enter the initial velocity for the \
upcoming trip: '))
    angle = float(input('Enter the angle of launch for the upcoming trip: '))
    time = float(input('Enter the length of the upcoming trip: '))
    tax = bool(input('Would you like to factor in tax? 1 for yes, 0 for no: '))
    
    # Convert each feet value into meters
    radius = feet_to_meter(radius_f)
    height_cone = feet_to_meter(height_cone_f)
    height_cyl = feet_to_meter(height_cyl_f)
    
    # Calculates the cost of the trip and the weigh of\
    # the rocket anf its equipment
    print ('This trip will cost $'+str(calculate_cost(feet_to_meter(radius_f),\
    feet_to_meter(height_cone_f), feet_to_meter(height_cyl_f),\
    velocity_e, velocity_i, time, tax)))
    print ('Now loading the rocket:')
    print('The rocket and its equipment will weigh',load_rocket\
          (rocket_mass(radius,height_cone, height_cyl),\
          radius, height_cyl), 'kg' )
    
    # Ask the user for information about the simulation of the trip
    simulation_time = int(input('Enter the simulation total time: '))
    interval = int(input('Enter the simulation interval: '))
    
    # Launch the projectile simulation
    print('Now simulating the rocket trajectory:')
    projectile_sim(simulation_time, interval, velocity_i, angle)        
            
  
        
        

