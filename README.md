# Escena Invernal de Rescate – Taller Práctico de Unity

Escena 3D en Unity de una patrulla de policía atrapada en una tormenta de nieve nocturna. El coche está semienterrado, sus sirenas giran sobre el techo, cae una ventisca y sale humo del escape.

**Autor:** Sebastián Saldaña
**Motor:** Unity 6.6 (6000.6.3f1) · Built-In Render Pipeline
**Escena principal:** `Assets/Scenes/SampleScene.unity`

## Cómo abrir el proyecto

1. Instala [Git LFS](https://git-lfs.com). El modelo del coche (`.fbx`) pesa más de 100 MB y se guarda con LFS.
2. Clona el repositorio:

   ```bash
   git lfs install
   git clone https://github.com/Saldana07/UnityTaller-Invierno-Saldana.git
   ```

3. Abre la carpeta desde Unity Hub con la versión 6000.6.3f1 o una compatible.
4. Abre `Assets/Scenes/SampleScene.unity` y pulsa **Play**.

## Jerarquía de la escena

```
Main Camera          Cámara en diagonal hacia el coche, fondo azul oscuro
Moon_Light           Luz direccional azul pálida (luz de luna)
Snow_Terrain         Plano con material de nieve (color + relieve)
Police_Car           Objeto padre del coche, hundido en Y = -0.5
    Car_Mesh         Modelo 3D de la patrulla
    Siren_Pivot      Punto de giro de las sirenas (lleva el script)
        Red_Light    Spot Light roja
        Blue_Light   Spot Light azul, apunta al lado opuesto
    Exhaust_Smoke    Partículas de humo del escape
Global_Blizzard      Partículas de la ventisca de nieve
```

Las luces son hijas de `Siren_Pivot`, así que giran con él sin animación por fotogramas clave.

## Script

`Assets/SirenRotation.cs` rota `Siren_Pivot` sobre su eje Y. La velocidad se ajusta en el Inspector con **Rotation Speed** (grados por segundo).

```csharp
transform.Rotate(0f, rotationSpeed * Time.deltaTime, 0f);
```

El uso de `Time.deltaTime` hace que la velocidad no dependa de los FPS.

## Sistemas de partículas

| Sistema | Qué hace | Ajustes principales |
| --- | --- | --- |
| Global_Blizzard | Nieve que cae sobre toda la escena con viento lateral | Emisor tipo Box 40×40, 1200 partículas/s, Velocity over Lifetime en X, Noise para remolinos, Prewarm |
| Exhaust_Smoke | Humo gris a bocanadas desde la parte trasera | Emisor tipo Cone, Bursts cada 0.8 s, se aclara y desvanece con Color over Lifetime, crece con Size over Lifetime |

## Materiales y texturas

- **M_Nieve:** textura de color y de relieve generadas para la escena (`Assets/Texturas_Nieve`), repetidas 10 veces sobre el plano.
- **Coche:** materiales del modelo en `Assets/Modelos/TEXTURES`, con la pintura de patrulla en blanco y negro.

## Historial de commits

1. `feat: configuracion inicial del proyecto y escena vacia`
2. `feat: agregar terreno nevado y coche enterrado`
3. `feat: jerarquia de luces y sirenas de emergencia`
4. `feat: implementar script SirenRotation.cs`
5. `feat: integrar particulas de nieve y humo de escape`

Después de estos commits se configuró Git LFS, se reemplazó el cubo por el modelo 3D de la patrulla y se mejoraron las texturas.

## Créditos

- **Modelo 3D:** "Dodge Charger SRT Police" por [temich](https://sketchfab.com/3d-models/dodge-charger-srt-police-c6d52512e32d42abb89466ced4d56c1d), descargado de Sketchfab. Licencia: [LICENCIA].
- Proyecto realizado como parte del Taller Práctico de Unity – Escena Invernal.
