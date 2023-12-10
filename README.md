
# Evaluation of Sample Algorithms in Unity Game Engine.

Solving this equation may be computationally expensive but it should be possible to do so if one has a precise model of the impact of the devices on the space, i.e., one has an accurate model of the physics for each device and access to the geometry of the space.  We do not rule out the possibility that in the future powerful servers may be associated with each space and available to deliver instantaneous results via standard user interfaces, but this is not the reality of today.  For now, IoT devices do not come with associated physics models and there are no dedicated spatial modeling servers in every home and every office. Realistic solutions need to be nimble and opportunistic, readily adapted to the specific set of devices encountered in a given space, and rely on the limited knowledge the space provides. One reasonable approach is to assume that the space incorporates sensors and not only actuators.  Sensors are relatively inexpensive and already in use across many applications.  A complementary approach is to rely to some extent on user feedback.  After all, the overall intent is to satisfy the user's needs.  Finally, it makes sense for the space to learn from prior interactions with the user and gradually become more responsive, i.e., able to make accurate decisions faster and without imposing on the user.
In this section, we seek to develop an understanding of how user feedback, availability of sensors, and historical data contribute to solving the equation above.  With this goal in mind, we seek to explore the domain of algorithmic solutions made possible by exploiting these different resources alone and in various combinations along the lines summarized in Table 1.

**Table 1:** Algorithm taxonomy based on the availability of resources.


| Context                            | Case              | Available Resources            |
|------------------------------------|---|------------------------------------------------|
| History data is not available      | 1.| Feedback                                       |
|                                    | 2.| Sensor                                         |
|                                    | 3.| Feedback + Sensor                              |
| History data is available          | 1.| Feedback + History                             |
|                                    | 2.| Sensor + History                               |
|                                    | 3.| Feedback + Sensor + History                    |




<table>
  <tr>
    <td>Figure 1: Concept of Spatial Characteristics and the factors impacting them.</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c1_cdf_steps.png" width=800 height=400></td>
  </tr>
</table>

