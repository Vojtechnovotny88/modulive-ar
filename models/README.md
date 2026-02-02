# Složka pro 3D modely

## Požadované soubory

Pro Android (WebXR) potřebuješ soubory ve formátu `.glb`:
- house1.glb
- house2.glb
- house3.glb
- house4.glb
- house5.glb
- house6.glb

Pro iOS (AR Quick Look) potřebuješ soubory ve formátu `.usdz`:
- house1.usdz
- house2.usdz
- house3.usdz
- house4.usdz
- house5.usdz
- house6.usdz

## Kde sehnat testovací modely

Pro vyzkoušení aplikace můžeš stáhnout zdarma modely z:

1. **Sketchfab** (https://sketchfab.com)
   - Hledej "chair glb free" nebo "house glb free"
   - Stáhni ve formátu glTF/GLB

2. **Poly Haven** (https://polyhaven.com)
   - Sekce "Models"
   - Stáhni jako GLB

3. **market.pmnd.rs** (https://market.pmnd.rs)
   - Různé 3D modely zdarma

## Převod formátů

**GLB → USDZ (pro iOS):**
- Online: https://products.groupdocs.app/conversion/glb-to-usdz
- Nebo: https://www.creators3d.com/online-viewer

**Jiné formáty → GLB:**
- Online: https://modelconverter.com
- Nebo: https://gltf.report

## Doporučení pro projektanta

Řekni projektantovi:
1. Export do formátu GLB (GLTF Binary)
2. 1 jednotka v modelu = 1 metr ve skutečnosti
3. Model by měl obsahovat materiály/textury
4. Ideální velikost souboru: do 10 MB

Programy které umí exportovat GLB:
- Blender (File → Export → glTF 2.0)
- SketchUp (s pluginem)
- ArchiCAD (s pluginem)
- Revit (přes FBX do Blenderu)
