
###套路
let camera, 相机
    screen, 场景
    renderer, 渲染器
    controls 控制器

资源准备好之后 window.onload = () =>{ 
    对齐进行初始化 init();
    animate(); 动画
}

init:

- camera = new THREE.Per(角度，w/h(水平端起相机),)
- camera.position.z 拍摄的总的距离
- scene = new THREE.Scene(); 拍摄的场景
- const container = docuemn ..... ('div') 挂载点 挂载到DOM节点上（renderer渲染的地方）
- 添加以类名
- THREE.CSS3DObject 特殊的Object类型
- scene.add(..)将之添加进去
- 创建渲染器，设置大小为这个屏幕的大小
- 将其挂载到container上
- 调用一下render();

render():
- renderer.render(scene,camera);

animate():
- requestAnimateFrame(animate);

