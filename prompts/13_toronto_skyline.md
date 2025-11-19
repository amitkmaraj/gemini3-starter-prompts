

**Objective:** Build an ultra-detailed, photorealistic 3D real-time simulation of the **Toronto city skyline** using Three.js. The primary goal is to achieve visual fidelity and realism, moving beyond simple procedural blocks to a "digital twin" feel, while maintaining 60FPS performance.

**Core Visual Philosophy:** Avoid a "polygonal" or "CG" look. Focus on **PBR (Physically Based Rendering) materials**, sophisticated lighting, and high-resolution textures to mimic real-world photographic qualities.

---

### 🌃 I. Scene & Model Fidelity

This is the highest priority. The "rough" look comes from generic models.

* **1. Landmark "Hero" Models (High-Poly):** These must be high-fidelity, custom models, not procedural.
    * **CN Tower:** Model its specific components: the main pod (with its distinct "tire" shape and window-heavy observation deck), the *glass floor* section, the upper *SkyPod*, the "donut" radome, and the full needle.
    * **Rogers Centre:** Model the *entire* stadium structure, including the *retractable roof panels* (in a fixed open position) and the concrete superstructure. Include the attached hotel.
    * **Financial District (The "Postcard" Shot):**
        * **First Canadian Place:** Distinctive white marble, modeled with its window indentations.
        * **Scotia Plaza:** Accurate red granite, modeled with its "M" shaped crest and complex setbacks.
        * **TD Centre:** Model *all main towers* in the complex, capturing their iconic black steel and bronze-tinted glass (Mies van der Rohe style).
        * **CIBC Square:** Model both towers with their signature *diamond-patterned glass facade*.
    * **Scotiabank Arena:** Model its unique, curved "atrium" entrance and main bowl structure.
    * **Roy Thomson Hall:** Include its iconic sloped glass "tent" structure.

* **2. Hybrid Procedural Skyline (The "Filler"):** Do *not* use simple `BoxGeometry` cubes.
    * Create a "kit" of 20-30 pre-made, low-to-mid-poly building models with varied footprints, heights, and architectural styles (e.g., modern glass-and-steel, older brick/stone facades).
    * Procedurally place these "kit" models to fill out the city blocks, ensuring realistic density and height falloff (tallest near the core, shorter towards the edges).
    * **Roofs:** All buildings (hero and procedural) must have roof-top details: mechanical boxes, HVAC units, antennas, and small "penthouse" structures. This is critical for breaking up flat, "CG" surfaces.

* **3. Terrain & Landscape:**
    * **Toronto Islands:** Model as high-quality, textured low-poly terrain. Include distinct textures for **beaches**, **grass**, and **tree clusters** (`InstancedMesh` for trees).
    * **Billy Bishop Airport:** Model the runway, terminal, and a few static planes.
    * **Waterfront:** Model the specific piers, **HTO Park** (with its yellow umbrellas), and the **Queen's Quay** terminal.

---

### ✨ II. Materials & Texturing (Photorealism)

This is the key to "not looking like a rendering."

* **PBR Workflow:** **All** materials **must** be `MeshStandardMaterial` or `MeshPhysicalMaterial`.
* **Textures:** Use high-resolution textures.
    * **Buildings:** Use texture atlases for concrete, brick, metal panels, and *especially* window-grime/imperfection maps (subtle wear-and-tear) to break up sterile surfaces.
    * **Glass:** Building glass *must not* be 100% transparent. Use a `MeshPhysicalMaterial` with low `roughness`, high `reflectivity`, and a slight tint.
    * **Roads:** Use textured asphalt with `normal` and `roughness` maps for the Gardiner/Lakeshore.
* **Reflections (Crucial):**
    * **Sky & Environment:** Use a `CubeCamera` to generate a real-time (or semi-real-time) environment map from the scene. This map **must** be applied as the `.envMap` to all PBR materials (especially glass and water) to provide realistic reflections of the sky and city.
    * **Lake Ontario:** The GLSL shader must reflect the `Sky` shader, the sun, and the city lights (using a technique like Screen Space Reflection or by sampling the environment map).

---

### 💡 III. Lighting & Atmosphere

* **Lighting:**
    * **Sun:** A single `DirectionalLight` that simulates the sun. It **must cast shadows** (use `PCFSoftShadowMap`).
    * **Sky:** Use `three/examples/jsm/objects/Sky.js`. This shader dynamically changes the entire sky's appearance (color, turbidity, sun position) based *only* on the "Time" slider's sun elevation. This is far more realistic than just changing colors.
    * **Ambient:** Use a `HemisphereLight` (sky-to-ground) for subtle fill light.
* **Post-Processing (via `EffectComposer`):**
    * `SSAOPass` (Screen Space Ambient Occlusion): **Essential** for adding realistic contact shadows and depth, preventing the "flat" render look.
    * `UnrealBloomPass`: For emissive lights (cars, CN Tower, windows) at night. Tweak `threshold`, `strength`, and `radius` for a soft, photographic glow, not a laser-light look.
    * `ACESFilmicToneMapping`: For photorealistic HDR handling.
* **Night Mode Details:**
    * **CN Tower:** The light show must be programmable, using an array of `PointLight` or `SpotLight` objects (or faked with a texture) that change colors in sequence.
    * **Office Buildings:** At night, use an **emissive texture map** for windows. This map should be a grid of "on" and "off" (or various-colored) windows to simulate random office occupancy, creating a "salt and pepper" light pattern. Do *not* just make the whole building glow.

---

### 🚗 IV. Dynamic Elements

* **Traffic (`InstancedMesh`):**
    * **Models:** Use at least 3-4 different instanced car models (sedan, SUV, truck, bus) to break up repetition.
    * **Lights:** Cars must have *two* `Sprite` instances for headlight flares (using a "starburst" texture) and two for taillights. Add a *third* set of emissive red lights for brake lights that randomly activate.
* **TTC Streetcar:** Add 1-2 instances of the iconic red TTC streetcar (`InstancedMesh`) running on a simple track path along Queen's Quay.
* **Lake Activity:**
    * **Ferries:** Model the specific Toronto Island ferries (e.g., *Trillium*, *Sam McBride*).
    * **Boats:** `InstancedMesh` for 2-3 types of sailboats and yachts.
    * **Wakes:** All boats/ferries should have a simple particle `Sprite` system or a decal-based wake trailing them on the water's surface.

---

### 🛠️ V. Tech & UI

* **Core:** Single HTML file `toronto_skyline.html`. All assets (Three.js, addons, textures) must be loaded via CDN or encoded as Base64.
* **Optimization:**
    * **`InstancedMesh`:** Use aggressively for cars, lights, streetlights, trees, windows (if possible), and birds.
    * **`THREE.LOD` (Level of Detail):** Implement this for the "Hero" buildings. When the camera is far away, switch to a low-poly "impostor" model.
    * **Texture Atlases:** Combine multiple textures (e.g., different window types, concrete textures) into a single atlas to minimize draw calls.
* **UI:** Sleek, minimal sliders for:
    * **Time of Day** (0-24h) (This should be the *only* control for the `Sky` shader and sun position)
    * **Fog Density** (0-100%)
    * **Activity Density** (0-100%) (Controls car, boat, and bird count)
    * **Camera Zoom** (Dolly zoom, not FOV change)
    * **Post-Processing (Toggle):** A single checkbox to enable/disable SSAO and Bloom for performance comparison.