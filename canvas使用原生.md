http://docs.cocos.com/creator/manual/zh/render/camera.html?h=%E6%91%84%E5%83%8F%E6%9C%BA
// 接下来就可以对这些数据进行操作了
```javascript
let canvas = document.createElement('canvas');
let ctx = canvas.getContext('2d');
canvas.width = texture.width;
canvas.height = texture.height;

let rowBytes = width * 4;
for (let row = 0; row < height; row++) {
    let srow = height - 1 - row;
    let imageData = ctx.createImageData(width, 1);
    let start = srow*width*4;
    for (let i = 0; i < rowBytes; i++) {
        imageData.data[i] = data[start+i];
    }

    ctx.putImageData(imageData, 0, row);
}

let dataURL = canvas.toDataURL("image/jpeg");
let img = document.createElement("img");
img.src = dataURL
```
