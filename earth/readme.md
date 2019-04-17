 3D 物体？
 是由 形状 + 表面的材质

 <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>WebGL-earth</title>
</head>

<body>
    <!-- 画布 ----webgl 的容器-->
    <canvas id="webglcanvas"></canvas>
    <script src="https://cdn.bootcss.com/three.js/r83/three.min.js"></script>
    <script>
        var canvas,   //幕布
            camera,  //摄像机
            scene,  //场景
            group, //群组
            renderer; //渲染器

        var mouseX = 0, mouseY = 0;
        var windowHalfX = window.innerWidth / 2;
        var windowHalfY = window.innerHeight / 2;


        // 准备
        init();
        
        function animate() {
            // requestAnimationFrame 请求运动帧

            // 不停的刷新canvas 的静态照片
            requestAnimationFrame(animate);
            render();
        }
        animate();

        function render() {
            camera.position.x += (mouseX - camera.position.x)*0.05;
            camera.position.y += (-mouseY - camera.position.y)*0.05;
            camera.lookAt(scene.position);
            renderer.render(scene, camera);
            group.rotation.y -= 0.005;
        }
        function init() {
            canvas = document.getElementById('webglcanvas');
            // THREE 有着 3D 的一切 
            camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHight, 1, 2000);
            //60：角度 1：最近距离  2000：最远距离  window.innerWidth / window.innerHight 横着拿相机
            camera.position.z = 500; // 相机离拿相机人的距离  500px

            scene = new THREE.Scene();
            scene.background = new THREE.Color(0xffffff); //背景颜色

            group = new THREE.Group();
            scene.add(group); //第一组先上

            // 地球 形状 + 表面材质 
            var loader = new THREE.TextureLoader();

            // 待加载完图片才能把它贴到形状上
            loader.load('earth.jpg', function (texture) {
                // 形状
                var geometry = new THREE.SphereGeometry(200, 20, 20);

                //材质
                var material = new THREE.MeshBasicMaterial({ map: texture });
                // 将 texture 作为 map 的value 作为 材质

                var mesh = new THREE.Mesh(geometry, material);
                // 将材质贴到 模型上去，形成一个物体

                group.add(mesh);  //完成准备
            });

            renderer = new THREE.WebGLRenderer({
                canvas: canvas,
                antialias: true  //抗拒齿
            });

            renderer.setSize(window.innerWidth, window.innerHeight);

            document.addEventListener('mousemove',onDocumentMouseMove,false);

        }
        function onDocumentMouseMove(event) {
            mouseX = (event.clientX - windowHalfX);

            mouseY = (event.clientY - windowHalfY);
            console.log(mouseX,mouseY);

        }

    </script>
</body>

</html>