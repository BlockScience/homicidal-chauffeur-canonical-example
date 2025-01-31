Link: https://demonstrations.wolfram.com/TheHomicidalChauffeurProblem/

In this Demonstration, a chauffeur driving a car with a minimum turning radius $r_{\text {min }}$ pursues a slower pedestrian with an unrestricted turning radius. The car is red and the evading pedestrian is blue. Click "setup" to set values for $r_{\text {min }}$ and the velocity ratio $v_{\text {car }} / v_{\text {pedestrian }}$, and drag the locators to set the initial positions of the car and pedestrian and the orientation of the car. Then click "running" and move the locator to control the goal position of the pedestrian; after three seconds, the car attempts to run over the pedestrian. Avoid the car as long as possible!

## Details

The homicidal chauffeur is a pursuit-evasion game introduced in 1951 by Rufus Isaacs[1]. The object of the pursuer is to move within a [[Capture Radius|capture radius]] of the evader in minimum time. The evader seeks to maximize this time. The pursuer moves forward at a constant rate, and can vary its angular velocity between a hard left or a hard right around a circle of radius $r_{\text {min }}$. The minimum turn circles are drawn with dashed gray lines.

The optimal controls are not unique, and depend both on the speed ratio and minimum turning radius ratio between the pursuer and the evader. In 1971, Antony Merz identified 20 qualitatively different optimal solutions that depend on the values of those two parameters[2]; this Demonstration only implements one algorithm for the pursuer. The chauffeur steers toward the pedestrian if the latter cannot escape into the disks outlined by dashed gray lines; otherwise, it turns away from the pedestrian and increases separation until it determines the pedestrian can be captured. Furthermore, this Demonstration determines collision if the car boundary intersects the pedestrian, while the classic formulation defines capture if the evader is within the capture radius of the pursuer.

The car has forward velocity of $v_{\text {car }}$ units per second and is modeled as a Dubins car[3] with system equations:

$$
\begin{aligned}
& \frac{d}{d t} x=v_{\text {car }} \cos \theta, \\
& \frac{d}{d t} y=v_{\text {car }} \sin \theta, \\
& \frac{d}{d t} \theta=v_{\text {car }} u
\end{aligned}
$$

where $u$ is chosen from the interval $\left\{-1 / r_{\min }, 1 / r_{\min }\right\}$. This is often a reasonable model for a boat or car with no reverse gear or a fixed-wing airplane.

The pedestrian is a simple integrator with system equations:

$$
\begin{aligned}
& \frac{d}{d t} x=u_x \\
& \frac{d}{d t} y=u_y
\end{aligned}
$$

and a maximum speed constraint on the control inputs,

$$
\sqrt{u_x^2+u_y^2} \leq v_{\text {pedestrian }}
$$


The implemented algorithm is imperfect, so you can find regions of the parameter space where the evader can avoid collision forever.

The homicidal chauffeur model can be used to study surveillance where an aircraft must fly over evasive targets and is often used by researchers as an unclassified proxy for missile defense.