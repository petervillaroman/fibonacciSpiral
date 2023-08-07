<script>
    import { onMount, onDestroy } from 'svelte';
    import * as THREE from 'three';

    let container;
    let camera, scene, renderer;
    let geometry, material, mesh;

    onMount(() => {
        camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.01, 10);
        camera.position.z = 1;

        scene = new THREE.Scene();

        geometry = new THREE.BoxGeometry(0.4, 0.8, 0.1);
        material = new THREE.MeshNormalMaterial();

        mesh = new THREE.Mesh(geometry, material);
        scene.add(mesh);

        renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);

        animate();
        return onDestroy;
    });

    function animate() {
        requestAnimationFrame(animate);

        mesh.rotation.x += 0.01;
        mesh.rotation.y += 0.02;
        mesh.rotation.z += 0.00;

        renderer.render(scene, camera);
    }

    // onDestroy(() => {
    //     renderer.dispose();
    //     scene.dispose();
    //     geometry.dispose();
    //     material.dispose();
    // });
</script>

<div bind:this={container}></div>
