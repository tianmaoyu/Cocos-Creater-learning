# 物理引擎

## 概念

关键组件

1. 刚体：RigidBody
   1. GetMass() :质量
   2. GravtiyScale: 重力大小
   3. LinerVelocity:线速度
   4. LinerDamping :线性摩擦力
   5. angularVelocity: 旋转速度
   6. angularDamping: 旋转衰减速度
   7. enableContactListener:碰撞监听
   8. 刚体的分类
      1. Static :静态的， 都为零
      2. Dynamic: 动态的 有质量，受到重量，可设置速度
      3. kinematic:运动刚体，0质量，可以设置速度，不受重量影响
      4. Animated: 动画刚体，kinematic 的衍生物
2. 碰撞： Collider
   1. BOX:四边形
   2. Chain: 链条型
   3. Circle:圆形
   4. Polygon: 多边形
   5. sensor:指明是否是传感器，传感器会产生碰撞回调，但是不会发生物理碰撞效果
   6. density:碰撞体的密度，用于刚体的质量计算
   7. friction:碰撞时 的摩擦力
   8. restitution:碰撞的弹性系数

