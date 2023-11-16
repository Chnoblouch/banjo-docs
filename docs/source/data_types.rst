==========
Data Types
==========

.. highlight:: banjo

Primitives
==========

+-----------+--------------------------------+--------------+
| Data Type | Description                    | Size (Bits)  |
+===========+================================+==============+
| i8        | 8-bit signed integer           | 8            |
+-----------+--------------------------------+--------------+
| i16       | 16-bit signed integer          | 16           |
+-----------+--------------------------------+--------------+
| i32       | 32-bit signed integer          | 32           |
+-----------+--------------------------------+--------------+
| i64       | 64-bit signed integer          | 64           |
+-----------+--------------------------------+--------------+
| u8        | 8-bit unsigned integer         | 8            |
+-----------+--------------------------------+--------------+
| u16       | 16-bit unsigned integer        | 16           |
+-----------+--------------------------------+--------------+
| u32       | 32-bit unsigned integer        | 32           |
+-----------+--------------------------------+--------------+
| u64       | 64-bit unsigned integer        | 64           |
+-----------+--------------------------------+--------------+
| f32       | 32-bit floating point number   | 32           |
+-----------+--------------------------------+--------------+
| f64       | 64-bit floating point number   | 64           |
+-----------+--------------------------------+--------------+
| bool      | boolean (true or false)        | 8            |
+-----------+--------------------------------+--------------+
| usize     | pointer-sized unsigned integer | pointer size |
+-----------+--------------------------------+--------------+
| addr      | opaque pointer                 | pointer size |
+-----------+--------------------------------+--------------+

Pointers
========

::

    var a: i32 = 100;

    # Creating a pointer to a variable.
    var ptr: *i32 = &a;

    # Dereferencing the pointer.
    println(*ptr); # 100

    # Modifying the value through the pointer.
    *ptr = 50;
    println(a); # 50

    # Creating a null pointer
    var null_ptr: *i32 = null as *i32;

Structs
=======

::

    use std.math.sqrt;

    struct Vec2 {
        pub var x: f32;
        pub var y: f32;

        pub func new(x: f32, y: f32) -> Vec2 {
            return Vec2 {
                x: x,
                y: y
            };
        }

        pub func length(self) -> f32 {
            return sqrt(self.x * self.x + self.y * self.y);
        }
    }

Tuples
======

::

    var a: (i32, bool) = (100, true);
    println(a.0); # 100
    println(a.1); # true

    a.1 = false;
    println(a.1); # false

Arrays
======

::

    # Initializing arrays with a literal.
    var array: [i32] = [1, 2, 3];
    
    # Accessing array elements.
    println(array[0]);
    array[0] = 20;

    # Iterating over the elements.
    for value in array {
        println(value);
    }

    # Arrays are dynamic!
    array.append(4);

    # Arrays can be iterated over by reference.
    for *value in array {
        *value = 100;
    }

Optionals
=========

::

    func main() {
        # Initializing an optional with a value.
        var opt1: ?i32 = 100;
        println(opt1.has_value); # true
        println(opt1.value); # 100

        # Initializing an empty optional.
        var opt2 = none;
        println(opt2.has_value); # false
    }