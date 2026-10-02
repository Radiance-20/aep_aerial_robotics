# DEAD RECKONING: How Machines Know Where They Are

## What is Dead Reckoning?

Dead reckoning is a navigation technique used to estimate the current position of a moving object based on its previously known position, direction, speed, and the amount of time it has been moving. Instead of constantly asking an external system where it is, the object uses information about its own movement to calculate where it should be.

In aerial robotics, dead reckoning is used by drones and other autonomous aircraft to estimate their position, velocity, direction, and orientation. It becomes particularly useful when GPS/GNSS is unavailable, unreliable, or temporarily lost. The drone can use onboard motion sensors to continue estimating its position until a reliable external reference becomes available again.


## How Does It Work?

Dead reckoning begins with a known starting position. As the drone moves, its onboard sensors measure changes in acceleration, rotation, direction, altitude, and sometimes movement relative to the ground. The system then uses these measurements to estimate the drone's new state.

Some of the important sensors include an accelerometer, which measures linear acceleration, and a gyroscope, which measures rotation and changes in orientation. A magnetometer can help determine heading, while a barometer can provide information about changes in altitude. Optical-flow or vision sensors can also help estimate movement relative to the ground.

The basic process can be represented as:

Known position → Measure movement → Calculate new position → Repeat

For example, if a drone knows its starting position and its sensors indicate that it has moved 10 metres forward, its estimated position is updated to approximately 10 metres ahead of its starting point.

Modern flight controllers can combine information from several sensors using techniques such as the Extended Kalman Filter (EKF). This helps produce a more reliable estimate than relying on a single sensor. 


## Example

Imagine a drone takes off from point A.

Its starting position is:

Position = (0, 0)

The drone estimates that it is travelling at:

Velocity = 2 m/s

If it continues moving for:

Time = 5 seconds

The distance travelled can be calculated as:

d = vt

d = 2 * 5 = 10m

Therefore, the drone estimates that it has travelled approximately 10 metres from its starting position in the direction of travel.

The important point is that this is an estimate. If the sensors contain small errors, those errors can accumulate as the drone continues flying, causing the estimated position to gradually differ from its actual position.


## How Is It Used in Real Life?

Dead reckoning is useful in situations where a drone cannot continuously depend on GPS/GNSS. For example, an aerial robot may temporarily lose satellite signals when flying near large structures, under bridges, inside certain buildings, or in other environments where satellite signals are obstructed or degraded.

It can also be useful for search-and-rescue drones, autonomous aircraft, and other systems operating in environments where reliable external positioning is difficult. Flight-control platforms such as PX4 provide functionality for degraded or denied GNSS conditions, while ArduPilot includes dead-reckoning-related failsafe functionality. 

## Advantages

Dead reckoning has several advantages in aerial robotics. It allows a drone to continue estimating its movement even when GPS/GNSS is unavailable, making it useful for autonomous navigation and temporary positioning failures.

It also relies primarily on onboard sensors, meaning the drone does not always need an external positioning system to estimate its movement. In addition, dead reckoning can be combined with GPS, optical flow, cameras, and other navigation technologies to create a more robust navigation system.


## Disadvantages

The major disadvantage of dead reckoning is error accumulation, commonly called drift. Even very small errors in sensor measurements can become significant after the measurements are continuously integrated over time.

For example, a small error in the accelerometer can produce an incorrect velocity estimate. That velocity error can then produce an even larger position error. Similarly, small errors in orientation can cause the drone to believe that it is travelling in a slightly different direction from its actual direction.

Other challenges include sensor noise, sensor bias, gyroscope drift, incorrect initial position or orientation, and dependence on proper sensor calibration. As a result, dead reckoning alone may become increasingly inaccurate during long periods without position correction. 


## How Can We Reduce the Error?

The most effective approach is generally to avoid relying on dead reckoning alone. Instead, information from multiple sensors can be combined so that one source can help correct the errors of another.

For example, a drone may combine:

IMU + GPS/GNSS + Magnetometer + Barometer + Optical Flow

An Extended Kalman Filter (EKF) can process these different measurements and estimate the drone's position, velocity, and orientation. When a reliable reference such as GPS becomes available, it can be used to correct accumulated drift in the inertial estimate. 

Other ways to reduce errors include **proper accelerometer and gyroscope calibration, magnetometer calibration, higher-quality sensors, optical-flow or vision-based positioning, and periodically correcting the estimated position using a known reference**.

### In simple terms:

Dead reckoning tells the drone: “Based on where I was and how I have moved, I think I am here.”

Sensor fusion tells the drone: “Let's compare that estimate with other sensors and correct it if necessary.”


## Sources

* [ArduPilot — Extended Kalman Filter](https://ardupilot.org/dev/docs/extended-kalman-filter.html?utm_source=chatgpt.com)
* [ArduPilot — Extended Kalman Filter Overview](https://software.ardupilot.org/copter/docs/common-apm-navigation-extended-kalman-filter-overview.html?utm_source=chatgpt.com)
* [PX4 — Navigation Filter (EKF2)](https://docs.px4.io/main/en/advanced_config/tuning_the_ecl_ekf?utm_source=chatgpt.com)
* [PX4 — GNSS-Degraded & Denied Flight](https://docs.px4.io/main/en/advanced_config/gnss_degraded_or_denied_flight?utm_source=chatgpt.com)
