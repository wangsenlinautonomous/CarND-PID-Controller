# CarND-PID-Controller
## Overview
Partical filter mainly contains the following four steps:
* P Controller
* PD Controller
* PID Controller
* Twiddle
* Implemetaion in C++

---

## P Controller

P, or "proportional", component had the most directly observable effect on the car’s behaviour. It causes the car to steer proportional (and opposite) to the car’s distance from the lane center(CTE) - if the car is far to the right it steers hard to the left, if it’s slightly to the left it steers slightly to the right.It sets the steering angle in proportion to CTE with a proportional factor tau.

```
-tau * cte
```

<img src="https://user-images.githubusercontent.com/40875720/52987012-81ac3080-3434-11e9-9316-49692975eca4.PNG" width="600">

## PD Controller

P controller can help to reduce the error very quickly, but it can easily cause overshoot(like the below pic shows).In this case, PD controller can be a good solution.
Basically, PD controller also consider derivative of the error. When the error is approach to zero, the D component(differentila) will be smaller, then the output of the PD controller will be smaller. By using this method, it can help to reduce the overshoot

```
diff_cte = cte - prev_cte
prev_cte = cte
- tau_d * diff_cte
```

<img src="https://user-images.githubusercontent.com/40875720/52987698-31829d80-3437-11e9-9a7d-f07ffcbd9a72.PNG" width="600">
<img src="https://user-images.githubusercontent.com/40875720/52987020-8bce2f00-3434-11e9-94dc-f8f0f3c48739.PNG" width="600">

## PID Controller
In most of cases, PD controller is good enough, but in some cases(like steering drift(steering bias)) constant bias may happen. In these special cases, PID controller can help. I means integgral of the sum of error to deal with systematic biases.

In other words, the I, or "integral", component counteracts a bias in the CTE which prevents the P-D controller from reaching the center line. This bias can take several forms, such as a steering drift , but I believe that in this particular implementation the I component particularly serves to reduce the CTE around curves.

<img src="https://user-images.githubusercontent.com/40875720/52987028-94266a00-3434-11e9-8de1-5ee8f9501006.PNG" width="600">
<img src="https://user-images.githubusercontent.com/40875720/52987040-9d173b80-3434-11e9-802c-58eefb29b29e.PNG" width="600">

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)



