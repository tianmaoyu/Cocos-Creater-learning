# 一些代码技巧

## Math.random()

1. 获取一个 min 到 max 范围的值 y= min+ (Math.random())*max
2. 获取中 -x 到 x  两侧范围 y= (Math.random()-0.5)* x
3. 左右加速度计算方式 y=x*a^2 +x; 在update 中 this.xSpeed -= this.accel * 0.1 
4. 不能超个 最大速度  this.xSpeed = this.maxMoveSpeed * this.xSpeed / Math.abs(this.xSpeed);

 ```javascript
  update (dt) {
         // 根据当前加速度方向每帧更新速度
         if (this.accLeft) {
            this.xSpeed -= this.accel * dt;
        } else if (this.accRight) {
            this.xSpeed += this.accel * dt;
        }
        // 限制主角的速度不能超过最大值
        if ( Math.abs(this.xSpeed) > this.maxMoveSpeed ) {
            // if speed reach limit, use max speed with current direction
            this.xSpeed = this.maxMoveSpeed * this.xSpeed / Math.abs(this.xSpeed);
        }

        // 根据当前速度更新主角的位置
        this.node.x += this.xSpeed * dt;
     },

 ```

在一定的时间内消失逐渐消失

 ```javascript
       var opacityRatio = 1 - this.game.timer/this.game.starDuration;
        var minOpacity = 50;
        this.node.opacity = minOpacity + Math.floor(opacityRatio * (255 - minOpacity));
 ```

 
