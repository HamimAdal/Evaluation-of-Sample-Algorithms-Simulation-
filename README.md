
# Evaluation of Sample Algorithms in Unity Game Engine.

Solving this equation may be computationally expensive but it should be possible to do so if one has a precise model of the impact of the devices on the space, i.e., one has an accurate model of the physics for each device and access to the geometry of the space.  We do not rule out the possibility that in the future powerful servers may be associated with each space and available to deliver instantaneous results via standard user interfaces, but this is not the reality of today.  For now, IoT devices do not come with associated physics models and there are no dedicated spatial modeling servers in every home and every office. Realistic solutions need to be nimble and opportunistic, readily adapted to the specific set of devices encountered in a given space, and rely on the limited knowledge the space provides. One reasonable approach is to assume that the space incorporates sensors and not only actuators.  Sensors are relatively inexpensive and already in use across many applications.  A complementary approach is to rely to some extent on user feedback.  After all, the overall intent is to satisfy the user's needs.  Finally, it makes sense for the space to learn from prior interactions with the user and gradually become more responsive, i.e., able to make accurate decisions faster and without imposing on the user.
In this section, we seek to develop an understanding of how user feedback, availability of sensors, and historical data contribute to solving the equation above.  With this goal in mind, we seek to explore the domain of algorithmic solutions made possible by exploiting these different resources alone and in various combinations along the lines summarized in Table 1.

In the subsections that follow, we consider each of the six combinations above (three cases when there is no history data available in the space, and three cases when the space exploits the history data) in an attempt to establish fundamental limitations, general solution strategies, accuracy reached under various conditions, achievable performance, etc.  Sample research questions that will need to be addressed include: When using feedback alone, is there a convergence guarantee?  When sensors are used, what is the impact of sensor density on the performance? When history is used, what machine learning algorithm should be employed?

**Table 1:** Algorithm taxonomy based on the availability of resources.


| Context                            | Case              | Available Resources            |
|------------------------------------|---|------------------------------------------------|
| History data is not available      | 1.| Feedback                                       |
|                                    | 2.| Sensor                                         |
|                                    | 3.| Feedback + Sensor                              |
| History data is available          | 1.| Feedback + History                             |
|                                    | 2.| Sensor + History                               |
|                                    | 3.| Feedback + Sensor + History                    |


**4.1. Context 1. Meeting user requests without relying on history of user interactions.**

In the absence of a history of user interactions, leveraging real-time user feedback and sensors emerges as a viable solution for optimizing adaptive smart spaces. A variety of alternative resources can be employed, such as IP cameras, and infrared cameras where high dynamic range technology [1], and thermal image technique [5-6] are exploited to serve as illumination and temperature sensors. However, the use of cameras poses privacy concerns, necessitating alternative methods. Deployment of occupancy detection sensors [7-10] is one good choice, however, these system modules are limited to providing uniform lighting or temperature, with no capacity for maintaining specific levels unless the space exploits the right sensors related to the characteristics being investigated. Although some studies have employed wireless sensing modules, the stipulation of one light sensor per luminaire [11] results in inefficiencies due to an excessive number of sensors, elevated power consumption, and high-cost maintenance. This research investigates how human feedback and sensors (with a limited number) can function independently or in conjunction to effectively satisfy user requirements while respecting the constraints of a space's resources.

Before we go into the details of the algorithms, it is important to identify and address the primary challenges that underpin this research. This involves examining critical aspects that are pivotal to developing the algorithms, as depicted in Figure 4. One key investigation concerns the selection of a suitable heuristic such as sorting devices by minimum distance, maximum capacity, or other reasonable estimations that guides the algorithms in prioritizing the order of device exploration. Another crucial investigation involves determining the Device Exploration Technique, which can be either static or dynamic. The former uses a fixed searching technique, while the latter adjusts the list of device configurations as the algorithm progresses. Additional research query pertains to the determination of the termination condition (user-specified, or algorithm-specified), which dictates how long the algorithm explores the search space. Finally, defining Constraints can be another relevant aspect of the research which increases the algorithm’s efficiency. Next, we investigate instances of three algorithms that exploits different heuristics and search techniques and rely on real-time human feedback and/or sensors to generate possible outcomes. Let us consider the input request consisting of desired characteristic (illumination) value r at location p so that metric, δ (ρ ,r, p) = |r - ρ | is minimized, where |r - ρ | ≤ a. Here, ρ  is the achieved solution, and a is the threshold. 

<table>
  <tr>
    <td>Figure 1: Concept of Spatial Characteristics and the factors impacting them.</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/algorithm_framework.jpg" width=800 height=400></td>
  </tr>
</table>



<table>
  <tr>
    <td>Figure 1: Concept of Spatial Characteristics and the factors impacting them.</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c1_cdf_steps.png" width=800 height=400></td>
  </tr>
</table>

