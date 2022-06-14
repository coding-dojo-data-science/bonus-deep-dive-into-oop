# Object-Oriented Programming 

## Topics

- **OOP-Vocabulary**
- **Defining/Initializing Classes**
- **Inspecting classes:**
    - `help(obj)` vs `dir(obj)`
    
- **Deeper dive into Classes/Objects**
    - special methods/properties (`__repr__(),__str__(),__call__(),__version__(),__name__()`)
    - Methods: vs Bound Methods vs Static Methods 
    
- **Extended Activity: Building a Deck of PlayingCards**

# What does it mean to be 'Object-Oriented'?

> ### ___"Everything is an object."___
- some Python sensei


- Any function, method, class, variable are ALL objects. 
    - Built from a template Class
    - Can be stored in memory under any name 


```python
## Any function can be assigned to a new variable and will behave the same way
prove_it = None
prove_it
```


```python
# test our "prove_it" functon
prove_it("This is now equal to print.")
```


```python
# run help on prove_it

```


```python
## what is the __name__ of our function?
prove_it.__name__
```

# OOP VOCABULARY


#### VOCAB RELATED TO FUNCTIONS:

- **Function: A resuable, fleixbile block of code that runs a process**  

    - Parameters: inputs that are expected by python/that function
    
    - Argument: the actual value/variable passed into the function. 
        - Positional Argument:
        - Keyword/default Arguments:

- "Calling" a function: `( )`


```python
def my_func(posarg1, 
            posarg2, kwarg1='example',kwarg2='example2'):
    print('positional arguments:')
    print(f"    {posarg1}, {posarg2}")
    
    print("keyword arguments:")
    print(f"    kwarg1={kwarg1}")
    print(f"    kwarg2={kwarg2}")
```


```python
## What does my_func look like?
my_func
```


```python
## Run my_func with posarg1=1,posarg2=2
my_func(1,2)
```


```python
## Change kwarg1 to something else
my_func(1,2,kwarg1='something else')
```

#### VOCAB RELATED TO CLASSES:

- "Object": 
- **Class:** 
- Instance: 
- Attribute:
- Method:
- Private Attributes/Methods: 
- Getters/Setters:


- Object: 

- "dunders" = double underscores __ 

# Defining and Initializing Classes


- Use `class NewClassName():` like you use `def function_name():` for functions.
    - the `()` are optional for classes. (used to inherit other classes, more on that later)

#### Naming Classes
    
- Convention for naming classes = `UpperCamelCase`
- Convention for naming function = `snake_case`


```python
## Bare minimum to define a class.

```

## Attributes and Methods

- Attribute: a variable is stored inside a class/object

- Method: a function that is stored inside of and (usually) operates on the object/class

## What makes a PlayingCard?

***Card:***
- *Value / Name*:
    - 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K, A
- *Suit*:
    - Hearts (H), Spades(S), Clubs(C), Diamonds(D) 
- *Color*:
    - black or red


```python
## Make a new PlayingCard class with a value of 2 and a suit of spades, and color=black

```


```python
## Make an instance of a PlayingCard and display it

```


```python
## Print out the vard's value and suit in one statement

```

> Improving our class: let's add a `.flip()` method that will print the value and suit. 



```python
## Copy previous version of class and add the .flip method.

```


```python
## Insantiate a playing card and run .flip()    

```

> Ruh roh! What happened?! What does the error message mean?

### Know thy `self`

- Because Methods are designed to operate on the `object_its.attached_to()`, Python automatically gives every method a copy of instance its attached to, which we call `self`
- We have to pass `self` as the first parameter for every method we make.
- Otherwise it will think that the first thing we give it is actually itself. This will cause an *existential crisis** and corresponding error.


```python
## Update our class by adding self where its needed.

        
```


```python
## Instantiate a playing card and test out .flip()

```

## Initialization 


- As we have seen, we create an instance by setting a `instance = ClassName()`
-  This uses the template `ClassName` to create an instance of the class ( which we named `instance`).
> - How do we change our PlayingCard class so that we can make other cards besides the 2 of spades?

### `__init__`

> - When an instance is `initialized`, we `call` it using `()`, which runs a default `__init__()` method.


```python
## Update our class by adding an __init__ that controls value, suit, color

        
```


```python
## test out our updated playing card class by making  card1 = a 'J of Hearts'

```


```python
## test out our updated playing card class by making a 7 of Spades

```

### is card 1 greater than card 2?


```python

```

# Special Class Methods

#### Special Methods

It is common for a class to have magic methods. These are identifiable by the "dunder" (i.e. **d**ouble **under**score) prefixes and suffixes, such as `__init__()`. These methods will get called **automatically**, as we'll see below.

For more on these "magic methods", see [here](https://www.geeksforgeeks.org/dunder-magic-methods-python/).

## Using Special Methods to evaluate comparisons 

### `__gt__` & `__lt__`:



```python
## Add a __gt__ and __lt__ method to compare self to other

```


```python
## Remake card 1 and card2 and test if card1>card2

```

> - Ruh Roh! We can't compare a str and an int! Let's fix this with out `__init__ `



#### Adding our card's value

- Create a string-based `name` for the card
    - Update `.flip()` to use `name` instead of `value`
- Save the numeric `value` of the card for comparison
- 


```python
## Value dictionary for lookup 
value_dct = {
    '2': 2,'3': 3, '4': 4, '5': 5, '6': 6,
    '7': 7, '8': 8, '9': 9, '10': 10,
    'J': 11,'Q': 12, 'K': 13, 'A': 14
    }
value_dct
```


```python
## Create a string-based name for the card
# save the numeric value of the card for comparison

```


```python
## Run this cell to test our value comparison from before
card1 = PlayingCard('J','H')
card1.flip()

card2 = PlayingCard(7,'S')
card2.flip()

card1>card2
```


```python
## What about card1<card2?
card1<card2
```

> Success! This is great and all, but the PlayingCard isn't terribly fun-looking 


```python
## Display card1

```

## Using special methods to control the output of a class


```python
## Display card 1

```

### `__repr__()`  &  `__str__()`

- Whenever an object is displayed, it runs the object's  `__repr__()` method. 
- Whenever an object is printed, it runs the  `__str__()` method.

- They are both designed to return string-representations of the object. 
    - But `__repr__()` focuses on minimizing ambiguity while `__str__()` focuses on readability. 
- However, if your class has no `__str__()` method, it will fall back on `__repr__()` (if it exists!). 
    - For more on this distinction, see [this post](https://dbader.org/blog/python-repr-vs-str).

### Add a `__repr__` and ` __str__` method to our PlayingCard

- have `__repr__` return 'An Instance of a PlayingCard'
- have `__str__` return "A Playing Card"


```python
### add a __repr__() method that returns "A Playing Card"

```


```python
## Test out our __repr__ & __str__

```

### Making Things More Interesting

-  Instead of our text-based `__repr__` and `__str__`, let's be sneaky and use an image of card back for our `__repr__`.

<img src="card_back.png" width=100>


```python
from PIL import Image
img = Image.open("card_back.png")
img.resize((100,150))
```

> - Add a `back` attribute that stores the image of the card. 
- Replace our `__repr__` with display the image
    - Go ahead and delete our `__str__` since we want it to behave the same as `__repr__` anyway


```python
### add a .back containing the stored image of the card.

```


```python
## Test out our __repr__

```


```python
# test our __str__
```


```python
#test our .flip()

```

> Success!

### Making our class even MORE fun 

- Our `.flip()` method is kind of boring compared to our `__repr__`
- If only we had some way of using symbols in our text instead of just boring old font.... 🤔


```python
## Our dictionary of suit symbols
symbols = {'S':'♠️','C':'♣️','D':'♦️','H':'♥️'}
symbols
```

> #### Use these emoji symbols plus the provided make_ascii_card to overhaul our class's .flip()


```python
def make_ascii_card(name, suit):
    """Ascii Card adapted from: https://codereview.stackexchange.com/questions/82103/ascii-fication-of-playing-cards
    """
    symbols = {'S':'♠️','C':'♣️',
               'D':'♦️','H':'♥️'}
    suit_symbol = symbols[suit]
    if name == '10':
        space=''
    else:
        space = ' '

    # add the individual card on a line by line basis
    _ascii=[]
    _ascii.append('┌─────────┐')
    _ascii.append(f'│{name}{space}       │')#.format(rank, space))  # use two {} one for char, one for space or char
    _ascii.append('│         │')
    _ascii.append('│         │')
    _ascii.append(f'│    {suit_symbol}   │') #.format(suit))
    _ascii.append('│         │')
    _ascii.append('│         │')
    _ascii.append(f'│       {space}{name}│')#.format(space, rank))
    _ascii.append('└─────────┘')
    
    return '\n'.join(_ascii)



print(make_ascii_card('A','D'))
```

> - Add a .face containing the stored ascii version of the card.
- Change `.flip()` to use the new face.



```python
### add a .face containing the stored ascii version of the card.

```


```python
## Run this cell to test our value comparison from before
card1 = PlayingCard('J','H')
display(card1)
card1.flip()

card2 = PlayingCard(7,'S')
display(card2)
card2.flip()

card1>card2
```

> Yay!!! We are HUGE nerds but yay!!!!

# NEXT:  Make a `Deck` to Explore some additional special methods. 

### Overview - Whats in a Deck?

***A Deck***
- "a collection of Cards"
    - Contains all standard 52 cards in a `.cards` attribute.
- Has a  `.shuffle()` method.
- Returns the number of cards in the deck as the `__repr__`

- Has a `__getitem__` method to make the deck subscriptable


```python
import numpy as np


```


```python
## Test out the Deck class by running the next cells

```


```python
## Slice out the first .cards

```


```python
## Slice first card directly and flip

```


```python
## shuffle and flip the first card again

```


```python
## Completed Deck Class

```


```python

```

# Nice!

## To recap, we:

1. Built a Card object using `class`.
    - Used `__init__(self)` to set attributes and run processes when the object is created.
    - Created a method `flip(self)` which "flips the card over" (shows the name and suit).
    - Experimented with `__str__` and `__repr__`.

  
2. Built a Deck object that uses `Cards`!
    - Decks can `shuffle` and `shuffle_and_deal`.
    
---

There are some points which we missed for the sake of drawing up the example.

- We could clean up the Card functions for deciding what to do if a user tries to create a Card without a real `name` or `suit`.

- We also don't have a plan for what happens if the Deck uses `shuffle_and_deal` but doesn't have enough cards left!

___

# APPENDIX

## Inheritance


- We can inherit all of the properties of another class when we write a new one to save ourselves time and effort. 


### Use inheritance to make our own OneHotEncoder


```python
import pandas as pd
```


```python
# import cdds as ds
# ds.ihelp(ds.datasets.load_iowa_prisoners)
```


```python
## Getting the dataset ready (don't worry about this code for now)
url = url ='https://raw.githubusercontent.com/jirvingphd/iowa-prisoner-recidivism-mod-3-project/b6a92d1474c3eee790ab894f79751d69578bfb18/datasets/FULL_3-Year_Recidivism_for_Offenders_Released_from_Prison_in_Iowa.csv'
df= pd.read_csv(url)
df.fillna('MISSING',inplace=True)
drop_cols= [col for col in df.columns if 'New' in col]
drop_cols.append('Days to Recidivism')
df.drop(columns=drop_cols,inplace=True)
df.head()

```


```python
## let's encode "ReleaseType" using onehotencoder
from sklearn.preprocessing import OneHotEncoder
cols_to_encode = ['Release Type']

encoder = OneHotEncoder(sparse=False).fit(df[cols_to_encode])

data_ohe = encoder.transform(df[cols_to_encode])
data_ohe
```


```python
## Turn data_ohe into a dataframe:
data_ohe = pd.DataFrame(data_ohe,
                        columns = encoder.get_feature_names(cols_to_encode))
data_ohe
```

### Make our own Encoder


```python
class OurOneHotEncoder(OneHotEncoder):
    pass
```


```python
help(OurOneHotEncoder)
```

### Add a method to transform the data as a dataframe.


```python

def transform_as_df(self,X,orig_features):
    data_ohe = self.transform(X)
    df_ohe = pd.DataFrame(data_ohe,
                        columns = encoder.get_feature_names(orig_features))
    return df_ohe
    
OurOneHotEncoder.transform_as_df = transform_as_df

```


```python
cols_to_encode = ['Release Type']

encoder = OurOneHotEncoder(sparse=False).fit(df[cols_to_encode])
data_ohe = encoder.transform_as_df(df[cols_to_encode],cols_to_encode)
data_ohe
```


```python

```
