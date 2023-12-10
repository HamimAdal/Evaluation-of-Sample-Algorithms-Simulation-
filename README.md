
# Evaluation of Sample Algorithms in Unity Game Engine.

**Working Platform.**

-- Simulation Software: Unity Game Engine

-- Programming: C#, Python

-- Libraries: pandas, matplotlib, NumPy

**Getting Started.**

Solving equations to fulfill requests in terms of the  <i><a href="https://github.com/HamimAdal/Spatial-Characteristics"> Spatial Characteristics</a></i> model in smart space may be computationally expensive but it should be possible to do so if one has a precise model of the impact of the devices on the space, i.e., one has an accurate model of the physics for each device and access to the geometry of the space. We do not rule out the possibility that in the future powerful servers may be associated with each space and available to deliver instantaneous results via standard user interfaces, but this is not the reality of today. For now, IoT devices do not come with associated physics models and there are no dedicated spatial modeling servers in every home and every office. Realistic solutions need to be nimble and opportunistic, readily adapted to the specific set of devices encountered in a given space, and rely on the limited knowledge the space provides. 

One reasonable approach is to assume that the space incorporates sensors and not only actuators.  Sensors are relatively inexpensive and already in use across many applications.  A complementary approach is to rely to some extent on user feedback.  After all, the overall intent is to satisfy the user's needs.  Finally, it makes sense for the space to learn from prior interactions with the user and gradually become more responsive, i.e., able to make accurate decisions faster and without imposing on the user.

In this investigation, our motive is to develop an understanding of how user feedback, availability of sensors, and historical data contribute to solving equations.  With this goal in mind, we seek to explore the domain of algorithmic solutions made possible by exploiting these different resources alone and in various combinations along the lines summarized in Table 1. In the subsections that follow, we consider each of the six combinations above (three cases when there is no history data available in the space, and three cases when the space exploits the history data) in an attempt to establish fundamental limitations, general solution strategies, accuracy reached under various conditions, achievable performance, etc.  Sample research questions that will need to be addressed include: When using feedback alone, is there a convergence guarantee?  When sensors are used, what is the impact of sensor density on the performance? When history is used, what machine learning algorithm should be employed?

**Table 1:** Algorithm taxonomy based on the availability of resources.


| Context                            | Case              | Available Resources            |
|------------------------------------|---|------------------------------------------------|
| 1. History data is not available   | 1.| Feedback                                       |
|                                    | 2.| Sensor                                         |
|                                    | 3.| Feedback + Sensor                              |
| 2. History data is available       | 1.| Feedback + History                             |
|                                    | 2.| Sensor + History                               |
|                                    | 3.| Feedback + Sensor + History                    |


# Context 1. Meeting user requests without relying on history of user interactions.

In the absence of a history of user interactions, leveraging real-time user feedback and sensors emerges as a viable solution for optimizing adaptive smart spaces. A variety of alternative resources can be employed, such as IP cameras, and infrared cameras where high dynamic range technology [1], and thermal image technique [2-3] are exploited to serve as illumination and temperature sensors. However, the use of cameras poses privacy concerns, necessitating alternative methods. Deployment of occupancy detection sensors [4-7] is one good choice, however, these system modules are limited to providing uniform lighting or temperature, with no capacity for maintaining specific levels unless the space exploits the right sensors related to the characteristics being investigated. Although some studies have employed wireless sensing modules, the stipulation of one light sensor per luminaire [11] results in inefficiencies due to an excessive number of sensors, elevated power consumption, and high-cost maintenance. This research investigates how human feedback and sensors (with a limited number) can function independently or in conjunction to effectively satisfy user requirements while respecting the constraints of a space's resources.

Before we go into the details of the algorithms, it is important to identify and address the primary challenges that underpin this research. This involves examining critical aspects that are pivotal to developing the algorithms, as depicted in Figure 1. One key investigation concerns the selection of a suitable heuristic such as sorting devices by minimum distance, maximum capacity, or other reasonable estimations that guides the algorithms in prioritizing the order of device exploration. Another crucial investigation involves determining the Device Exploration Technique, which can be either static or dynamic. The former uses a fixed searching technique, while the latter adjusts the list of device configurations as the algorithm progresses. Additional research query pertains to the determination of the termination condition (user-specified, or algorithm-specified), which dictates how long the algorithm explores the search space. Finally, defining Constraints can be another relevant aspect of the research which increases the algorithm’s efficiency. 

Next, we investigate instances of three algorithms that exploit different heuristics and search techniques and rely on real-time human feedback and/or sensors to generate possible outcomes. Let us consider the input request consisting of the desired characteristic (illumination) value r at location p so that metric, δ (ρ ,r, p) = |r - ρ | is minimized, where |r - ρ | ≤ a. Here, ρ  is the achieved solution, and a is the threshold. 

<table>
  <tr>
    <td>Figure 1: Concept of Spatial Characteristics and the factors impacting them.</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/algorithm_framework.jpg" width=800 height=400></td>
  </tr>
</table>

**Algorithm 1 (Linear search [8] on distance).** In this algorithm, our research aimed to identify the closest smart device that can offer the desired level of luminance at a specific location. To accomplish this, we utilized the linear search algorithm to examine a sorted list of smart devices, taking their minimal distance (heuristic) from the target location into consideration. 

**Algorithm 2 (Linear search [9] on estimates).** This Algorithm investigates the impact of a new heuristic on the behavior of the algorithm. To this end, we employed a unique solution strategy that leverages the capacity and location of each device, utilizing a lighting formula as the heuristic to estimate the level of illumination produced by each device configuration. The algorithm then sifts through the promising combinations of device configurations whose luminance levels fall within the acceptable threshold, resulting in a sorted list of devices ranked by the ascending order of the estimations generated by the device configurations. Finally, linear search algorithm is used to identify the optimal device configuration from the list that meets the user's requirements. 

**Algorithm 3 (Binary search [9] on estimates).** In this research study, we sought to investigate the impact of a different search technique on the performance of algorithms, specifically comparing the effectiveness of linear search and binary search. To achieve this objective, we retained the structure of Algorithm 3 similar to that of Algorithm 2, but instead utilized binary search on the sorted list of devices, in contrast to linear search used in Algorithms 1 and 2. Through this experiment, we aimed to uncover the potential improvements in the algorithm's performance with the use of binary search. The findings of this investigation provide valuable insights into the comparative efficacy of different search techniques in exploring the sorted list of devices.

To evaluate the algorithm’s flexibility and generality, we conducted a unique set of experiments under different circumstances that measured the success rate, number of user interactions/iterations, and devices needed for each algorithm. The evaluation process was carried out in the <b>Unity Game Engine</b> platform that exercised the characteristic “illumination”. There are a few assumptions that underlie the remaining discussions in this section. First, we assume a 3D space (a rectangular room of fixed dimensions, 25mX24mX10m), that is an inhabitant of a single user (avatar). Multiple Point lights (that cast light in all directions), and Light sensors (upon availability) were dispersed at random throughout the space. We further assumed that a localization system exists and provides continuous access to the location of the avatar, light devices, and sensors. Lastly, we presumed that the space also has knowledge of each device’s capacity. The evaluation conducted a considerable number of trials (>150), varying numbers of light fixtures (4 to 6), and their capacity (ranging from- 1 to 8 candela, with two device settings- turning on/off). The target illumination level at the avatar’s location (which varied across the space) fluctuated from 400 to 450 lux with a threshold of 40 lux for each trial. For evaluation purposes, the space had access to ground truth value (a light sensor was placed above the avatar). 


# Case 1. Only feedback, no sensors.

To assess the impact of human feedback on the performance of three algorithms, we conducted a simulation comprising 172 experiments. Figure 2(a) displays the probability that each algorithm reached a solution in Y number of user interactions or less. Algorithm 1, which investigated a more extensive range of device configurations, had a higher success rate (172 out of 172, 100%) outperforming Algorithm 2 (144 out of 172, 83.72%) and Algorithm 3 (131 out of 172, 76.16%), which assessed a restricted set of configurations based on estimations. The results were significantly influenced by the search technique implemented by each algorithm. Linear search explores every device configuration in the list, while binary search eliminates half of the device configurations at each iteration. Hence, Algorithm 3 which exploited binary search conceded fewer user interactions (1.61 on average) than Algorithm 2 (2.93 on average) and Algorithm 1 (4.69 on average) which exploited linear search. Finally, we analyzed the number of devices required by each solution in Figure 2(b), where the X-axis representing the probability that the algorithms reached a solution with Y number of devices or fewer. The results revealed that Algorithm 1 required fewer devices (2.06 on average) than Algorithm 2 (2.72 on average) and Algorithm 3 (3.16 on average). Overall, this study provides valuable insights into the impact of human feedback on algorithm performance, highlighting the importance of search techniques and the number of configurations considered in achieving optimal results.

**Figure 2:** Performance evaluation of the algorithms in Case 1.


<table>
  <tr>
    <td>(a)	Density of Probability vs Number of User Interaction</td>
    <td>(b) Density of Probability vs Number of Devices</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c1_cdf_steps.png" width=400 height=300></td>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c1_cdf_devices.png" width=400 height=300></td>
 
  </tr>
</table>



In this case, we employed "perfect" feedback to evaluate the performance of three algorithms. However, such a circumstance is rarely encountered in real-world situations. Human fallibility in the feedback mechanism can introduce deviations in the algorithms' ability to provide accurate results. Similarly, the accuracy of sensor readings can be influenced by external factors within the environment. Therefore, in the subsequent case, we introduced a simulated disruption in the estimated sensor readings to understand and acknowledge the limitations and challenges posed by real-world scenarios, emphasizing the need for further refinement and development of algorithms for reliable and accurate results.

# Case 2. Only sensor, no feedback.

This case follows a further inspection of how well the space leverages sensors and what effects do the distribution of sensors have on the algorithm’s functionality. To make the problem more challenging, we do not assume the estimated sensor readings at the target location to be perfect. As a matter of fact, the precision of the projected sensor reading at the desired location is entirely dependent on the interpolation method (we used Inverse Distance Weighting Formula) employed to compute the level of illumination. 

The first key study in this case was to find out whether the distribution of sensors in space has any effect on the performances of the algorithms. Table 2 compares and summarizes the success rates of the algorithms when the sensors are randomly distributed across the space and when they are systematically placed following a certain protocol. Our analysis revealed that distributing sensors in a particular order (such as virtual dotted regular polygons depicted in Figure 3(b), where red icons represent sensors attached to each vertex) tended to result in a higher success rate of providing solutions compared to random sensor placement.   

**Table 2:** Performance difference of the algorithms based on the distribution of sensors in the Space.


| Sensor Distribution                         | Number of Experiments Conducted | Found Solution for Algorithm 1 | Found Solution for Algorithm 2 | Found Solution for Algorithm 3 |
|---------------------------------------------|---------------------------------|--------------------------------|--------------------------------|--------------------------------|
| Random in the space                         | 191                             | 140 (73.29%)                   | 113 (59.16%)                   | 107 (56.02%)                   |
| Vertices of regular (virtual) polygons      | 187                             | 167 (89.30%)                   | 129 (68.98%)                   | 127 (67.91%)                   |


<table>
  <tr>
    <td>Figure 3: Placement of sesnors in the space!</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/algo_sensor.jpg" width=800 height=400></td>
  </tr>
</table>

The next research study addresses how well the algorithms utilized sensor feedbacks to produce desired solution given that there is some disruption in the estimated sensor readings. In the simulation, a total of 187 experiments were run. Figure 4(a) portrays, Algorithm 1 emerged as the most successful with 167 solutions (89.30%) delivered, while Algorithm 2 and Algorithm 3 managed to provide 127 (67.91%) and 129 (68.98%) solutions, respectively. Because of lack of accuracy in sensor readings, the success rate of each algorithm in this case is lower than the algorithms in Case 1 that had perfect human feedback. The investigation also reveals- the more accurate the interpolation formula is in estimating the illumination level from the available sensors, the better the success rate is.

**Figure 4:** Performance evaluation of the algorithms in Case 2.


<table>
  <tr>
    <td>(a)	Density of Probability vs Number of User Interaction</td>
    <td>(b) Density of Probability vs Number of Devices</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c2_cdf_steps.png" width=400 height=300></td>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c2_cdf_devices.png" width=400 height=300></td>
 
  </tr>
</table>

The final observation depicts the convergence rate of the algorithms in Figure 4(a) where Algorithm 3 demonstrated a considerably faster convergence rate, requiring fewer iterations (1.62 on average) to discover the ideal device configuration, compared to Algorithm 2 (2.88 on average) and Algorithm 1 (3.49 on average). Regarding the number of devices needed (Figure 4 (b)), Algorithm 2 required fewer devices (2.65 on average) than Algorithm 1 (4.46 on average) and Algorithm 3 (3.37 on average). In this case, where there was no choice for human response, the users needed to be contended with whatever solution the algorithms offered based on the projected sensor readings. The next case does an advanced investigation on how the space can capitalize on human feedback on top of sensor readings to improve the performance of the algorithms.

# Case 3. Feedback and Sensor

The algorithms used in this case are designed to operate in two distinct phases. In the first phase, sensor readings are utilized to predict a device configuration that is close to an ideal solution. The second phase involves withholding the selection of the final device configuration until the user approves it. If the user rejects the proposed configuration, the algorithms restart phase 1 and search for an alternative device configuration. This process iterates until all possible configurations have been examined, or the user consents to a proposed solution. This iterative approach provides a practical and effective method for achieving an optimal configuration for a device while ensuring user satisfaction. 

Running the algorithms in the Unity Simulation for this case produced results that showed notable performance variations. We begin with analyzing the success rates of the algorithms. In the simulation, a total of 194 experiments were run. Figure 5 portrays that Algorithm 1 delivered the most number of solutions (183 out of 194, 94.32%) compared to Algorithm 2 (148 out of 194, 76.28%) and Algorithm 3 (139 out of 194, 71.64%). 


**Figure 5:** Performance evaluation of the algorithms in Case 2.

<table>
  <tr>
    <td>(a)	Density of Probability vs Number of User Interaction</td>
    <td>(b) Density of Probability vs Number of Devices</td>
  </tr>
  <tr>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c3_cdf_steps.png" width=400 height=300></td>
    <td><img src="https://github.com/HamimAdal/Simulation-Unity/blob/main/Figures_simulation/c3_cdf_devices.png" width=400 height=300></td>
 
  </tr>
</table>


Now, if we compare the algorithms for this case (human feedback and sensors), with Case 1 (human feedback), we discover that the algorithms of this case significantly outperform Case 1's algorithms in terms of number of user interactions required (on average). While examining each algorithm individually, the results indicate that this case averaged 1.37 user engagements for Algorithm 1, which is less than the number of user interactions made by Algorithm 1 in Case 1 (4.69 on average). The same is true for other algorithms, where the number of user interactions carried out by Algorithm 2 (1.10 on average) and Algorithm 3 (1.07 on average) in this case is lower than the algorithms in Case 1 (2.93 and 1.67 on average, for Algorithm 2 and Algorithm 3, respectively). In relation to the quantity of devices utilized (Figure 5(b)), Algorithm 1 averaged 4.23 devices per trial, while Algorithm 2 and Algorithm 3 needed 2.73 and 3.42 devices (on average), respectively.     

# Context 2. Meeting user requests relying on history of user interactions (Ongoing work)


# Reference

1. Budhiyanto, Aris, and Yun-Shang Chiou. "Prototyping a Lighting Control System Using LabVIEW with Real-Time High Dynamic Range Images (HDRis) as the Luminance Sensor." Buildings 12.5 (2022): 650.

2.	Chen, Xiaomeng, et al. "Remote sensing of indoor thermal environment from outside the building through window opening gap by using infrared camera." Energy and Buildings (2023): 112975.
3.	D.-S. Lee, J.-H. Jo, Application of IR camera and pyranometer for estimation of longwave and shortwave mean radiant temperatures at multiple locations, Build. Environ. 207 (2022).
4.  Garg, Vishal, and Narendra K. Bansal. "Smart occupancy sensors to reduce energy consumption." Energy and Buildings 32.1 (2000): 81-87. 
5.	Guo, X., et al. "The performance of occupancy-based lighting control systems: A review." Lighting Research & Technology 42.4 (2010): 415-431.
6.	Yang, Junjing, Mattheos Santamouris, and Siew Eang Lee. "Review of occupancy sensing systems and occupancy modeling methodologies for the application in institutional buildings." Energy and Buildings 121 (2016): 344-349.
7.	V.L. Erickson, A.E. Cerpa, Occupancy based demand response HVAC control strategy, in: Proceedings of the Second ACM Workshop on Embedded Sensing Systems for Energy-efficiency in Buildings, ACM, Zürich, 2010, pp. 7–12.
8.  https://www.geeksforgeeks.org/linear-search/
9.	https://www.geeksforgeeks.org/binary-search/






