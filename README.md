![image](https://github.com/HamimAdal/Simulation-Unity/assets/32908045/8320b6cc-2f41-41c3-b9d5-d4a938f725b5)
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

Algorithm 1 (Linear search [14] on distance). In this algorithm, our research aimed to identify the closest smart device that can offer the desired level of luminance at a specific location. To accomplish this, we utilized the linear search algorithm to examine a sorted list of smart devices, taking their minimal distance (heuristic) from the target location into consideration. 

Algorithm 2 (Linear search [14] on estimates). This Algorithm investigates the impact of a new heuristic on the behavior of the algorithm. To this end, we employed a unique solution strategy that leverages the capacity and location of each device, utilizing a lighting formula as the heuristic to estimate the level of illumination produced by each device configuration. The algorithm then sifts through the promising combinations of device configurations whose luminance levels fall within the acceptable threshold, resulting in a sorted list of devices ranked by the ascending order of the estimations generated by the device configurations. Finally, linear search algorithm is used to identify the optimal device configuration from the list that meets the user's requirements. 

Algorithm 3 (Binary search [15] on estimates). In this research study, we sought to investigate the impact of a different search technique on the performance of algorithms, specifically comparing the effectiveness of linear search and binary search. To achieve this objective, we retained the structure of Algorithm 3 similar to that of Algorithm 2, but instead utilized binary search on the sorted list of devices, in contrast to linear search used in Algorithms 1 and 2. Through this experiment, we aimed to uncover the potential improvements in the algorithm's performance with the use of binary search. The findings of this investigation provide valuable insights into the comparative efficacy of different search techniques in exploring the sorted list of devices.

To evaluate the algorithm’s flexibility and generality, we conducted unique set of experiments under different circumstances that measured succes rate, number of user interactions/iterations, and devices needed for each algorithm. The evaluation process was carried out in the Unity game engine platform that exercised the characteristic “illumination”. There are a few assumptions that underlie the remaining discussions in this section. First, we assume a 3D space (a rectangular room of fixed dimensions, 25mX24mX10m), that is an inhabitant of a single user (avatar). Multiple Point lights (that casts light in all directions), and Light sensors (upon availability) were dispersed at random throughout the space. We further assumed that a localization system exists and provides continuous access to the location of the avatar, light devices, and sensors. Lastly, we presumed that the space also has knowledge of each device’s capacity. The evaluation conducted a considerable number of trials (>150), varying numbers of light fixture (4 to 6), and their capacity (ranging from- 1 to 8 candela, with two device settings- turning on/off). The target illumination level at the avatar’s location (which varied across the space) fluctuated from 400 to 450 lux with a threshold of 40 lux for each trial. For evaluation purposes, the space had access to ground truth value (a light sensor was placed above the avatar). 




<table>
  <tr>
    <td>Figure 1: Concept of Spatial Characteristics and the factors impacting them.</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c1_cdf_steps.png" width=800 height=400></td>
  </tr>
</table>



# Reference

1. https://pysource.com/2019/06/05/control-webcam-with-servo-motor-and-raspberry-pi-opencv-with-python/

2. https://github.com/trieutuanvnu/AndroidWifiRasPi

3. https://github.com/trieutuanvnu/PiServoControlWifi
