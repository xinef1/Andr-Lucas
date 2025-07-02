<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Darth Dev | Star Wars 3D</title>
  <style>
    html, body {
      margin: 0;
      height: 100%;
      overflow: hidden;
      background: black;
      font-family: 'Orbitron', sans-serif;
      color: #ff0000;
    }

    canvas {
      display: block;
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }

    .hud {
      position: absolute;
      top: 5%;
      left: 5%;
      background: rgba(0, 0, 0, 0.5);
      padding: 20px;
      border: 2px solid #ff0000;
      border-radius: 10px;
      max-width: 400px;
    }

    .hud h1 {
      font-size: 2rem;
      margin: 0 0 10px;
    }

    .hud p {
      margin: 5px 0;
    }
  </style>
</head>
<body>
  <div class="hud">
    <h1>Darth [SeuNome] 🚀</h1>
    <p>⚔️ Classe: Dev Sith Fullstack</p>
    <p>🧠 Habilidades: JavaScript, React, Node, MongoDB</p>
    <p>🌌 Alinhamento: Lado Sombrio do Código</p>
    <p>🌠 Repositório: <a href="https://github.com/seuusuario" style="color:#ff5555">GitHub</a></p>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script>
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Starfield
    const starsGeometry = new THREE.BufferGeometry();
    const starCount = 2000;
    const starVertices = [];
    for (let i = 0; i < starCount; i++) {
      starVertices.push((Math.random() - 0.5) * 2000);
      starVertices.push((Math.random() - 0.5) * 2000);
      starVertices.push(-Math.random() * 2000);
    }
    starsGeometry.setAttribute(
      'position',
      new THREE.Float32BufferAttribute(starVertices, 3)
    );

    const starsMaterial = new THREE.PointsMaterial({ color: 0xffffff });
    const starField = new THREE.Points(starsGeometry, starsMaterial);
    scene.add(starField);

    // Vader cube
    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial({ color: 0xff0000, wireframe: true });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    camera.position.z = 5;

    function animate() {
      requestAnimationFrame(animate);

      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
      starField.rotation.y += 0.0005;

      renderer.render(scene, camera);
    }

    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });
  </script>
</body>
</html>

