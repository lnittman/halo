# 🐙 PMNDRS 3D/WebGL Libraries Documentation

## 🦉 Overview

This documentation covers the PMNDRS (Poimandres) ecosystem of 3D/WebGL libraries, focusing on their integration with React Three Fiber and advanced rendering techniques including ray-marching and fluid simulations.

## 🐊 Quick Start

### Installation
```bash
# Core libraries
npm install three @react-three/fiber

# Essential helpers and utilities
npm install @react-three/drei @react-three/postprocessing

# Physics engines
npm install @react-three/rapier  # Recommended: WASM-based, faster
# or
npm install @react-three/cannon  # Alternative: Web worker-based

# Additional libraries
npm install @react-three/flex    # Flexbox layouts in 3D
npm install @react-three/xr      # VR/AR support
npm install @pmndrs/detect-gpu   # GPU performance detection
```

## 🦝 Core Libraries

### 🦋 @react-three/drei

Drei is a collection of useful helpers and abstractions for React Three Fiber. It's essentially a toolkit that makes common 3D tasks easier.

#### Core Features
```javascript
import { 
  Box, Sphere, Torus,           // Geometry helpers
  OrbitControls,                // Camera controls
  Environment,                  // HDRI environments
  PerspectiveCamera,           // Cameras
  Text, Text3D,                // Typography
  useGLTF, useTexture,         // Asset loaders
  MeshReflectorMaterial,       // Special materials
  Float, Sparkles,             // Effects
  useHelper                    // Debug helpers
} from '@react-three/drei'
```

#### Common Patterns

**Environment and Lighting:**
```javascript
function Scene() {
  return (
    <>
      <Environment preset="sunset" background />
      <OrbitControls enablePan={false} />
      <PerspectiveCamera makeDefault position={[0, 0, 10]} />
      
      <Float speed={2} rotationIntensity={1}>
        <Box>
          <MeshReflectorMaterial 
            blur={[300, 100]}
            resolution={2048}
            mixBlur={1}
            mixStrength={80}
            roughness={1}
            depthScale={1.2}
            minDepthThreshold={0.4}
            maxDepthThreshold={1.4}
            color="#101010"
            metalness={0.5}
          />
        </Box>
      </Float>
    </>
  )
}
```

**Loading Assets:**
```javascript
function Model() {
  const { nodes, materials } = useGLTF('/model.glb')
  const texture = useTexture('/texture.jpg')
  
  return (
    <mesh geometry={nodes.Model.geometry} material={materials.Material}>
      <meshStandardMaterial map={texture} />
    </mesh>
  )
}
```

### 🐆 @react-three/postprocessing

React wrapper for the postprocessing library, enabling advanced visual effects.

#### Basic Setup
```javascript
import { EffectComposer, Bloom, DepthOfField, Noise, Vignette } from '@react-three/postprocessing'

function Effects() {
  return (
    <EffectComposer>
      <DepthOfField 
        focusDistance={0} 
        focalLength={0.02} 
        bokehScale={2} 
        height={480} 
      />
      <Bloom 
        luminanceThreshold={0} 
        luminanceSmoothing={0.9} 
        height={300} 
        intensity={1.5}
      />
      <Noise opacity={0.02} />
      <Vignette eskil={false} offset={0.1} darkness={1.1} />
    </EffectComposer>
  )
}
```

#### Advanced Effects for Fluid Simulations

**Custom Shader Effect:**
```javascript
import { Effect } from 'postprocessing'
import { Uniform } from 'three'

class FluidDistortionEffect extends Effect {
  constructor({ frequency = 0.1, amplitude = 0.1 } = {}) {
    super('FluidDistortionEffect', fragmentShader, {
      uniforms: new Map([
        ['frequency', new Uniform(frequency)],
        ['amplitude', new Uniform(amplitude)],
        ['time', new Uniform(0)]
      ])
    })
  }

  update(renderer, inputBuffer, deltaTime) {
    this.uniforms.get('time').value += deltaTime
  }
}

const fragmentShader = `
  uniform float frequency;
  uniform float amplitude;
  uniform float time;

  void mainImage(const in vec4 inputColor, const in vec2 uv, out vec4 outputColor) {
    vec2 distortedUV = uv + vec2(
      sin(uv.y * frequency + time) * amplitude,
      cos(uv.x * frequency + time) * amplitude
    );
    outputColor = texture2D(inputBuffer, distortedUV);
  }
`
```

### 🦝 Physics Libraries

#### @react-three/rapier (Recommended)

Rapier is a WASM-based physics engine that's faster and more stable than Cannon.

```javascript
import { Physics, RigidBody, CuboidCollider } from '@react-three/rapier'

function PhysicsScene() {
  return (
    <Physics gravity={[0, -9.81, 0]} debug>
      <RigidBody type="dynamic" position={[0, 5, 0]}>
        <Box>
          <meshStandardMaterial color="hotpink" />
        </Box>
      </RigidBody>
      
      <RigidBody type="fixed">
        <Box args={[10, 0.5, 10]} position={[0, -2, 0]}>
          <meshStandardMaterial color="gray" />
        </Box>
      </RigidBody>
    </Physics>
  )
}
```

**Advanced Rapier Features:**
```javascript
// Compound shapes
<RigidBody>
  <Box position={[0, 0, 0]} />
  <Sphere position={[1, 0, 0]} />
  <CuboidCollider args={[0.5, 0.5, 0.5]} position={[2, 0, 0]} />
</RigidBody>

// Joints
const bodyA = useRef()
const bodyB = useRef()
const joint = useSphericalJoint(bodyA, bodyB, [
  [0, 0, 0], // Anchor on bodyA
  [0, 0, 0]  // Anchor on bodyB
])

// Force application
const rigidBody = useRef()
useFrame(() => {
  if (rigidBody.current) {
    rigidBody.current.applyImpulse({ x: 0, y: 10, z: 0 }, true)
  }
})
```

#### @react-three/cannon (Alternative)

Cannon runs in a web worker, which can be beneficial for performance isolation.

```javascript
import { Physics, useSphere, useBox, usePlane } from '@react-three/cannon'

function Ball() {
  const [ref] = useSphere(() => ({
    mass: 1,
    position: [0, 5, 0],
    args: [0.5] // radius
  }))
  
  return (
    <mesh ref={ref}>
      <sphereGeometry args={[0.5]} />
      <meshStandardMaterial color="orange" />
    </mesh>
  )
}
```

### 🦋 @react-three/flex

Flexbox layout system for 3D space, based on Facebook's Yoga layout engine.

```javascript
import { Flex, Box } from '@react-three/flex'

function Layout() {
  return (
    <Flex 
      flexDirection="row" 
      justifyContent="center" 
      alignItems="center"
      size={[10, 5, 0]}
    >
      <Box centerAnchor>
        <mesh>
          <boxGeometry />
          <meshStandardMaterial color="red" />
        </mesh>
      </Box>
      
      <Box flexGrow={1} centerAnchor>
        <mesh>
          <sphereGeometry />
          <meshStandardMaterial color="blue" />
        </mesh>
      </Box>
    </Flex>
  )
}
```

**Responsive 3D Layouts:**
```javascript
function ResponsiveLayout() {
  const reflow = useReflow()
  
  return (
    <Flex flexWrap="wrap" size={[10, 10, 0]}>
      <Box width="auto" height="auto" flexGrow={1}>
        {(width, height) => (
          <mesh>
            <planeGeometry args={[width, height]} />
            <meshBasicMaterial color="purple" />
          </mesh>
        )}
      </Box>
    </Flex>
  )
}
```

### 🐸 @react-three/xr

VR/AR support for React Three Fiber applications.

```javascript
import { XR, createXRStore, XROrigin } from '@react-three/xr'

const store = createXRStore()

function XRApp() {
  return (
    <>
      <button onClick={() => store.enterAR()}>Enter AR</button>
      <Canvas>
        <XR store={store}>
          <XROrigin position={[0, 0, 0]}>
            <Controllers />
            <Hands />
          </XROrigin>
          
          <mesh position={[0, 1, -2]}>
            <boxGeometry />
            <meshStandardMaterial color="green" />
          </mesh>
        </XR>
      </Canvas>
    </>
  )
}
```

### 🦚 @pmndrs/detect-gpu

GPU performance detection for adaptive quality settings.

```javascript
import { getGPUTier } from 'detect-gpu'

async function setupQuality() {
  const gpuTier = await getGPUTier()
  
  // Returns:
  // {
  //   tier: 1-3,
  //   isMobile: boolean,
  //   fps: number,
  //   gpu: string
  // }
  
  if (gpuTier.tier >= 3) {
    // High quality settings
    return {
      shadows: true,
      postprocessing: true,
      pixelRatio: window.devicePixelRatio
    }
  } else if (gpuTier.tier === 2) {
    // Medium quality
    return {
      shadows: true,
      postprocessing: false,
      pixelRatio: Math.min(window.devicePixelRatio, 1.5)
    }
  } else {
    // Low quality
    return {
      shadows: false,
      postprocessing: false,
      pixelRatio: 1
    }
  }
}
```

## 🦋 Advanced Patterns & Techniques

### Ray Marching with React Three Fiber

Ray marching is perfect for creating organic, fluid-like effects similar to Vercel's ferrofluid.

```glsl
// Vertex shader
varying vec2 vUv;
varying vec3 vPosition;

void main() {
  vUv = uv;
  vPosition = position;
  gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
}

// Fragment shader
uniform float time;
uniform vec3 color;
varying vec2 vUv;
varying vec3 vPosition;

// SDF for a sphere
float sdSphere(vec3 p, float r) {
  return length(p) - r;
}

// SDF for metaballs
float sdMetaballs(vec3 p) {
  float d = sdSphere(p - vec3(sin(time) * 2.0, 0.0, 0.0), 1.0);
  d = min(d, sdSphere(p - vec3(0.0, cos(time) * 2.0, 0.0), 1.0));
  d = min(d, sdSphere(p - vec3(0.0, 0.0, sin(time * 1.5) * 2.0), 0.8));
  return d;
}

// Smooth minimum for fluid blending
float smin(float a, float b, float k) {
  float h = max(k - abs(a - b), 0.0) / k;
  return min(a, b) - h * h * h * k * (1.0 / 6.0);
}

void main() {
  vec3 rayOrigin = vPosition;
  vec3 rayDir = normalize(vPosition - cameraPosition);
  
  float totalDistance = 0.0;
  const int MAX_STEPS = 64;
  const float MAX_DIST = 100.0;
  const float EPSILON = 0.001;
  
  for (int i = 0; i < MAX_STEPS; i++) {
    vec3 p = rayOrigin + rayDir * totalDistance;
    float distance = sdMetaballs(p);
    
    if (distance < EPSILON) {
      // Hit! Calculate normal and lighting
      vec3 normal = normalize(vec3(
        sdMetaballs(p + vec3(EPSILON, 0, 0)) - distance,
        sdMetaballs(p + vec3(0, EPSILON, 0)) - distance,
        sdMetaballs(p + vec3(0, 0, EPSILON)) - distance
      ));
      
      float diffuse = max(dot(normal, vec3(0, 1, 0)), 0.0);
      vec3 finalColor = color * diffuse;
      
      gl_FragColor = vec4(finalColor, 1.0);
      return;
    }
    
    totalDistance += distance;
    
    if (totalDistance > MAX_DIST) break;
  }
  
  discard;
}
```

**React Component:**
```javascript
import { extend, useFrame } from '@react-three/fiber'
import { shaderMaterial } from '@react-three/drei'

const RayMarchMaterial = shaderMaterial(
  { time: 0, color: new THREE.Color('purple') },
  vertexShader,
  fragmentShader
)

extend({ RayMarchMaterial })

function RayMarchedFluid() {
  const materialRef = useRef()
  
  useFrame((state) => {
    if (materialRef.current) {
      materialRef.current.time = state.clock.elapsedTime
    }
  })
  
  return (
    <mesh>
      <boxGeometry args={[10, 10, 10]} />
      <rayMarchMaterial ref={materialRef} />
    </mesh>
  )
}
```

### Ferrofluid Effect Implementation

Creating a ferrofluid effect combining multiple techniques:

```javascript
import { useMemo, useRef } from 'react'
import { useFrame } from '@react-three/fiber'
import { MarchingCubes } from 'three/examples/jsm/objects/MarchingCubes'

function Ferrofluid() {
  const meshRef = useRef()
  const marchingCubes = useMemo(() => {
    const mc = new MarchingCubes(32, new THREE.MeshPhysicalMaterial({
      color: 0x000000,
      metalness: 1,
      roughness: 0.1,
      clearcoat: 1,
      clearcoatRoughness: 0,
      reflectivity: 1,
      envMapIntensity: 2
    }))
    mc.isolation = 80
    return mc
  }, [])
  
  useFrame((state) => {
    const time = state.clock.elapsedTime
    
    // Reset
    marchingCubes.reset()
    
    // Add metaballs
    const strength = 1.2
    const subtract = 12
    
    // Main blob
    marchingCubes.addBall(
      Math.sin(time * 0.7) * 0.5,
      Math.cos(time * 0.5) * 0.5,
      Math.sin(time * 0.9) * 0.5,
      strength,
      subtract
    )
    
    // Satellite blobs
    for (let i = 0; i < 3; i++) {
      const angle = (i / 3) * Math.PI * 2 + time
      marchingCubes.addBall(
        Math.cos(angle) * 0.3,
        Math.sin(angle * 1.2) * 0.3,
        Math.sin(angle * 0.8) * 0.3,
        strength * 0.5,
        subtract
    )
    }
    
    marchingCubes.update()
  })
  
  return <primitive object={marchingCubes} />
}
```

### Performance Optimization Patterns

**1. Instanced Rendering:**
```javascript
function InstancedParticles({ count = 1000 }) {
  const meshRef = useRef()
  const [data] = useState(() => ({
    positions: new Float32Array(count * 3),
    scales: new Float32Array(count)
  }))
  
  useLayoutEffect(() => {
    for (let i = 0; i < count; i++) {
      data.positions[i * 3] = (Math.random() - 0.5) * 10
      data.positions[i * 3 + 1] = (Math.random() - 0.5) * 10
      data.positions[i * 3 + 2] = (Math.random() - 0.5) * 10
      data.scales[i] = Math.random() * 0.5 + 0.5
    }
  }, [count, data])
  
  useFrame((state) => {
    const time = state.clock.elapsedTime
    for (let i = 0; i < count; i++) {
      const i3 = i * 3
      data.positions[i3 + 1] = Math.sin(time + i * 0.1) * 2
    }
    meshRef.current.geometry.attributes.position.needsUpdate = true
  })
  
  return (
    <instancedMesh ref={meshRef} args={[null, null, count]}>
      <sphereGeometry args={[0.1]} />
      <meshStandardMaterial color="white" />
    </instancedMesh>
  )
}
```

**2. LOD (Level of Detail):**
```javascript
import { useLOD } from '@react-three/drei'

function AdaptiveModel() {
  const [gpuTier, setGpuTier] = useState(null)
  
  useEffect(() => {
    getGPUTier().then(setGpuTier)
  }, [])
  
  return (
    <LOD>
      <mesh visible={gpuTier?.tier >= 3} distance={5}>
        <sphereGeometry args={[1, 64, 64]} />
        <meshStandardMaterial />
      </mesh>
      <mesh visible={gpuTier?.tier === 2} distance={15}>
        <sphereGeometry args={[1, 32, 32]} />
        <meshStandardMaterial />
      </mesh>
      <mesh visible={gpuTier?.tier <= 1} distance={25}>
        <sphereGeometry args={[1, 16, 16]} />
        <meshBasicMaterial />
      </mesh>
    </LOD>
  )
}
```

**3. Render on Demand:**
```javascript
function OnDemandScene() {
  const { invalidate } = useThree()
  
  // Only render when something changes
  const handleInteraction = () => {
    // Update state
    invalidate() // Trigger a single render
  }
  
  return (
    <mesh onClick={handleInteraction}>
      <boxGeometry />
      <meshStandardMaterial />
    </mesh>
  )
}
```

## 🐝 Best Practices

### 1. Asset Loading
```javascript
// Preload assets
useGLTF.preload('/model.glb')
useTexture.preload('/texture.jpg')

// Use suspense
<Suspense fallback={<Loader />}>
  <Model />
</Suspense>
```

### 2. Memory Management
```javascript
function DisposableScene() {
  useEffect(() => {
    return () => {
      // Clean up geometries, materials, textures
      geometry.dispose()
      material.dispose()
      texture.dispose()
    }
  }, [])
}
```

### 3. Event Handling
```javascript
// Use pointer events efficiently
<mesh
  onPointerOver={(e) => e.stopPropagation()}
  onPointerOut={(e) => e.stopPropagation()}
  onClick={(e) => {
    e.stopPropagation()
    // Handle click
  }}
/>
```

### 4. State Management
```javascript
import { useThree } from '@react-three/fiber'
import create from 'zustand'

const useStore = create((set) => ({
  quality: 'medium',
  setQuality: (quality) => set({ quality })
}))

function QualityAwareScene() {
  const quality = useStore((state) => state.quality)
  const { gl } = useThree()
  
  useEffect(() => {
    if (quality === 'high') {
      gl.setPixelRatio(window.devicePixelRatio)
    } else {
      gl.setPixelRatio(1)
    }
  }, [quality, gl])
}
```

## 🦌 Resources

- [React Three Fiber Documentation](https://docs.pmnd.rs/react-three-fiber)
- [Drei Storybook](https://drei.pmnd.rs/)
- [Three.js Documentation](https://threejs.org/docs/)
- [WebGL Fundamentals](https://webglfundamentals.org/)
- [The Book of Shaders](https://thebookofshaders.com/)
- [IQ's Distance Functions](https://iquilezles.org/articles/distfunctions/)

## 🐊 Example Projects

### Ferrofluid Shader Ball
```javascript
// Complete example combining techniques
import { Canvas } from '@react-three/fiber'
import { Environment, Float } from '@react-three/drei'
import { EffectComposer, Bloom, ChromaticAberration } from '@react-three/postprocessing'

function App() {
  return (
    <Canvas camera={{ position: [0, 0, 5] }}>
      <Environment preset="city" />
      <Float speed={2} rotationIntensity={2}>
        <Ferrofluid />
      </Float>
      <EffectComposer>
        <Bloom luminanceThreshold={0.2} luminanceSmoothing={0.9} height={300} />
        <ChromaticAberration offset={[0.002, 0.002]} />
      </EffectComposer>
    </Canvas>
  )
}
```

This documentation provides a comprehensive guide to the PMNDRS 3D ecosystem, focusing on practical implementation and advanced techniques for creating stunning 3D experiences like ferrofluid effects and ray-marched visuals.