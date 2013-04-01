# Performing trigonometry

## Problem

You need to implement mathematical functions that require
trigonometry.

## Solution

All of the trigometric functions are accessible via `java.util.Math`,
which is available as `Math`. Use them like you would any other
namespaced function.

    ;; Calculating sin(a + b). The formula for this is
    ;; sin(a + b) = sin a * cos b + sin b cos a
    (defn sin-plus [a b]
      (+ (* (Math/sin a) (Math/cos b))
         (* (Math/sin b) (Math/cos a))))
         
    (sin-plus 0.1 0.3)
    ;; -> 0.38941834230865047

Trigonometric functions operate on values measured in radians. If you
have values measured in degrees, such as latitude or longitude, then
you'll need to convert them to radians first. Use `Math/toRadians` to
convert degrees to radians.

    ;; Calculating the distance in kilometres between two points on Earth
    (def earth-radius 6371.009)

    (defn degrees->radians [point]
      (mapv #(Math/toRadians %) point))

    (defn distance-between
      "Calculate the distance in km between two points on earth. Each
       point is a pair of degrees latitude and longitude, in that order."
      ([p1 p2] (distance-between p1 p2 earth-radius))
      ([p1 p2 radius]
         (let [[lat1 long1] (degrees->radians p1)
               [lat2 long2] (degrees->radians p2)]
           (* radius
              (Math/acos (+ (* (Math/sin lat1) (Math/sin lat2))
                            (* (Math/cos lat1) (Math/cos lat2) (Math/cos (- long1 long2)))))))))

    (distance-between [49.2000 -98.1000] [35.9939, -78.8989])
    ;; -> 2139.42827188432

## Discussion

MORE DISCUSSION

`java.lang.Math` isn't only for trigonometry, it also contains a
number of functions useful for dealing with exponentiation, logarithms
and roots. A full list of methods is available in the
[java.util.Math javadocs](http://docs.oracle.com/javase/7/docs/api/java/lang/Math.html).

## See Also

* Ch. 1 section on performance and type hinting.
* Other math sections?