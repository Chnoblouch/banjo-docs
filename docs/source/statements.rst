==========
Statements
==========

.. highlight:: banjo

if
==

::

    if i == 0 {
        println("Zero");
    } else if i == 1 {
        println("One");
    } else {
        println("Other number");
    }

while
=====

::

    var i = 0;

    while i < 100 {
        println(i);
        i += 1;
    }


for
===

::

    for i in 0..10 {
        println(i);
    }