![image-20210603164600304](6-3-one-flow.assets/image-20210603164600304.png)

![image-20210603164745172](6-3-one-flow.assets/image-20210603164745172.png)

![image-20210603164759131](6-3-one-flow.assets/image-20210603164759131.png)

![image-20210603164816513](6-3-one-flow.assets/image-20210603164816513.png)

![image-20210603164916518](6-3-one-flow.assets/image-20210603164916518.png)

![image-20210603165128971](6-3-one-flow.assets/image-20210603165128971.png)

![image-20210603165258095](6-3-one-flow.assets/image-20210603165258095.png)

![image-20210603165350986](6-3-one-flow.assets/image-20210603165350986.png)

![image-20210603165407128](6-3-one-flow.assets/image-20210603165407128.png)

![image-20210603165420501](6-3-one-flow.assets/image-20210603165420501.png)

![image-20210603165429683](6-3-one-flow.assets/image-20210603165429683.png)

-   related：超算， MPI

![image-20210603165518803](6-3-one-flow.assets/image-20210603165518803.png)

![image-20210603165556778](6-3-one-flow.assets/image-20210603165556778.png)

![image-20210603165611478](6-3-one-flow.assets/image-20210603165611478.png)

case-by-case 并行设计 vs 半自动并行化设计

![image-20210603165920273](6-3-one-flow.assets/image-20210603165920273.png)

Scheduler 需要流控，目前没有考虑资源约束，可能导致OOM或死锁

![image-20210603170308902](6-3-one-flow.assets/image-20210603170308902.png)

![image-20210603170320817](6-3-one-flow.assets/image-20210603170320817.png)

方法： allocator与scheduler对话，进行query， 但会导致抽象泄漏

![image-20210603170444455](6-3-one-flow.assets/image-20210603170444455.png)

![image-20210603170647428](6-3-one-flow.assets/image-20210603170819187.png)

![image-20210603170854851](6-3-one-flow.assets/image-20210603170854851.png)

SBP 类似 GShard 中的annotation

-   Partial操作GShard中没有

![image-20210603171039258](6-3-one-flow.assets/image-20210603171039258.png)

![image-20210603171135931](6-3-one-flow.assets/image-20210603171135931.png)

![image-20210603171210443](6-3-one-flow.assets/image-20210603171210443.png)

![image-20210603171230530](6-3-one-flow.assets/image-20210603171230530.png)

![image-20210603171255107](6-3-one-flow.assets/image-20210603171255107.png)

![image-20210603171308830](6-3-one-flow.assets/image-20210603171308830.png)

![image-20210603171333657](6-3-one-flow.assets/image-20210603171333657.png)

# 去中心化系统

![image-20210603171342831](6-3-one-flow.assets/image-20210603171342831.png)

![image-20210603171352788](6-3-one-flow.assets/image-20210603171352788.png)

![image-20210603171432309](6-3-one-flow.assets/image-20210603171432309.png)

![image-20210603171529107](6-3-one-flow.assets/image-20210603171529107.png)

![image-20210603171606110](6-3-one-flow.assets/image-20210603171606110.png)

![image-20210603171636892](6-3-one-flow.assets/image-20210603171636892.png)

![image-20210603171658550](6-3-one-flow.assets/image-20210603171658550.png)

![image-20210603171712611](6-3-one-flow.assets/image-20210603171712611.png)

![image-20210603171720880](6-3-one-flow.assets/image-20210603171720880.png)

![image-20210603171734761](6-3-one-flow.assets/image-20210603171734761.png)

![image-20210603171744931](6-3-one-flow.assets/image-20210603171744931.png)

![image-20210603171802898](6-3-one-flow.assets/image-20210603171802898.png)

![image-20210603171813619](6-3-one-flow.assets/image-20210603171813619.png)

![image-20210603171824186](6-3-one-flow.assets/image-20210603171824186.png)

![image-20210603171838098](6-3-one-flow.assets/image-20210603171838098.png)

![image-20210603171848515](6-3-one-flow.assets/image-20210603171848515.png)

![image-20210603171905077](6-3-one-flow.assets/image-20210603171905077.png)

-   SubLinear -重计算

![image-20210603171916029](6-3-one-flow.assets/image-20210603171916029.png)

![image-20210603172003656](6-3-one-flow.assets/image-20210603172003656.png)