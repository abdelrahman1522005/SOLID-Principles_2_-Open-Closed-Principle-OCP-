# SOLID-Principles_2_-Open-Closed-Principle-OCP-

#Software entities (classes, modules, functions, etc.) should be open for extension,but closed for modification
from math import pi
class Shape:
  def __init__(self, shape_type, **kwargs):
    self.shape_type = shape_type
    if self.shape_type == "rectangle":
      self.width = kwargs["width"]
      self.height = kwargs["height"]
    elif self.shape_type == "circle":
      self.radius = kwargs["radius"]
  def calculate_area(self):
    if self.shape_type == "rectangle":
      return self.width * self.height
    elif self.shape_type == "circle":
      return pi * self.radius**2
#The initializer of Shape takes a shape_type argument that can beeither "rectangle" or "circle". It also takes a specific set of keyword argumentsusing the **kwargs syntax. If you set the shape type to "rectangle", then you shouldalso pass the width and height keyword arguments so that you can construct aproper rectangle.
#In contrast, if you set the shape type to "circle", then you must also passa radius argument to construct a circle.


from abc import ABC, abstractmethod
from math import pi
class Shape(ABC):
  def __init__(self, shape_type):
    self.shape_type = shape_type
  @abstractmethod
  def calculate_area(self):
    pass
class Circle(Shape):
  def __init__(self, radius):
    super().__init__("circle")
    self.radius = radius
  def calculate_area(self):
    return pi * self.radius**2
class Rectangle(Shape):
  def __init__(self, width, height):
    super().__init__("rectangle")
    self.width = width
    self.height = height
  def calculate_area(self):
    return self.width * self.height
class Square(Shape):
  def __init__(self, side):
    super().__init__("square")
    self.side = side
  def calculate_area(self):
    return self.side**2

#In this code, you completely refactored the Shape class, turning it into an abstractbase class (ABC). This class provides the required interface(API) for any shape thatyou’d like to define. That interface consists of a .shape_type attribute and a .calculate_area() method that you must override in all the subclasses. This
#update closes the class to modifications. Now you can add new shapes to your classdesign without the need to modify Shape. In every case, you’ll have to implement therequired interface, which also makes your classes polymorphic.
