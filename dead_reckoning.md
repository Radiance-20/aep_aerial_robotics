# Dead Reckoning: Navigating Without a Map

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
