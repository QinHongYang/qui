<template>
  <div>

  </div>
</template>

<script lang="ts">
import * as THREE from "three";
import { Vue,Component } from  'vue-property-decorator';

@Component({
    name: "three1"
})
export default class Three1 extends Vue {
    private scene!:THREE.Scene;
    private camera!:THREE.PerspectiveCamera;
    private renderer!:THREE.WebGLRenderer;

    created(){
      // this.$QDialog.open({title:'222',message:'333'});
        /**创建场景对象Scene*/
        this.scene = new THREE.Scene();
        /** 创建一个立方体几何对象Geometry 宽,高,纵深*/
        let geometry = new THREE.BoxGeometry(100, 100, 100);
        /** 创建一个球体几何对象 */
        // let geometry = new THREE.SphereGeometry(60, 40, 40);

        this.camera = new THREE.PerspectiveCamera(45,window.innerWidth/window.innerHeight,1,2000);
        this.renderer = new THREE.WebGLRenderer();
        let material = new THREE.MeshLambertMaterial({
            color: 'red'
        }); //材质对象Material
        let mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
        this.scene.add(mesh); //网格模型添加到场景中
        /**
         * 光源设置
         */
            //点光源
        let point = new THREE.PointLight(0xffffff);
        point.position.set(400, 200, 300); //点光源位置
        this.scene.add(point); //点光源添加到场景中
        //环境光
        let ambient = new THREE.AmbientLight(0x444444);
        this.scene.add(ambient);
        // console.log(scene)
        // console.log(scene.children)
        /**
         * 相机设置
         */
        let width = 300; //窗口宽度
        let height = 300; //窗口高度
        let k = width / height; //窗口宽高比
        let s = 200; //三维场景显示范围控制系数，系数越大，显示的范围越大
        //创建相机对象
        let camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);
        camera.position.set(200, 200, 200); //设置相机位置
        camera.lookAt(this.scene.position); //设置相机方向(指向的场景对象)
        /**
         * 创建渲染器对象
         */
        let renderer = new THREE.WebGLRenderer();
        renderer.setSize(width, height);//设置渲染区域尺寸
        renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
        renderer.domElement.style.display = "inline-block";
        document.body.appendChild(renderer.domElement); //body元素中插入canvas对象
        //执行渲染操作   指定场景、相机作为参数
        renderer.render(this.scene, camera);
    }
}
</script>

<style scoped>

</style>
