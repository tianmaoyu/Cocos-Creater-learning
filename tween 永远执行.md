
# tween
cc.tween(this.node)
    .repeat(10,
        cc.tween().by(1, { scale: 1 })
    )
    .start()

## 当使用两个永远执行时的坑
 cc.tween(this.node)
            .repeatForever(
                cc.tween().to(1, { scale: 1.2 })
                    .to(1, { scale: 1 })
            ).start()
