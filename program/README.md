### test_path.cbot

<details>
<summary>test_predict_position_arc_p90_left</summary>

**Input**

* L = 0.5  `motor_left`
* R = 1  `motor_right`
* $\alpha = 90$  `angle between pos and pos_e`


**Output**

* t  `time_delta`

**Solution**

$r = \frac{2}{1-\frac{L}{R}}-1 = 3$  `MOTOR_VALUE_TO_RADIUS_2`

$V = \frac{S}{t}$  `Velocity definition`

$L = \frac{\alpha \phi r}{180}$  `Arc length`

$V = 2.5(L + R) = 3.75$  `PREDICT_VELOCITY`

$t = \frac{\phi r}{5(L + R)} = \frac{2}{5} \phi \\approx 1.256637$

![picture](../images/test_predict_position_arc_p90_left.png) |

</details>
