# Actividad 1

<img width="1515" height="706" alt="image" src="https://github.com/user-attachments/assets/69c61794-ef39-4c9e-ae74-54da9a4c9562" />

# Actividad 4 

La verdad en un inicio no sabia que hacer pero si sabia que queria iniciar con algo distinto a un cuadrado, asi que escogi un disco y su "contenedor" es una esfera.

<img width="1046" height="778" alt="image" src="https://github.com/user-attachments/assets/09979bbb-f230-4b4d-8ced-5791684811f7" />

Ya de ahí fue que empece a ver que fuerzas me gustaban par ami interpretación, entre ellas las primeras que utilice eran de atracción y repulsión, por esto la implemente primero en botones, pero también queria una primera fuerza distinta donde todas las prticulas se repelan entre sí causando que se pegaran a las paredes del contenedor y eso me permitio hacer ondas que vayan con el beat de la canción. Ya después  le fui implementando más cosas que explicaré a mayor profundidad en breve.

<img width="969" height="766" alt="image" src="https://github.com/user-attachments/assets/98703bb8-6781-4908-b933-8e8b6372258a" />

<img width="918" height="725" alt="image" src="https://github.com/user-attachments/assets/5e864deb-3fb2-49e4-8aee-fbad034fb759" />

Aquí hay combinaciones de fuerzas de atracción entre más debiles a más fuertes y la fuerza que hace que se repelan, y hacía patrones muy interesantes.

<img width="1497" height="781" alt="Captura de pantalla 2026-08-19 144708" src="https://github.com/user-attachments/assets/f74471ae-3aae-4d98-b22a-608801a9e36f" />

<img width="880" height="668" alt="image" src="https://github.com/user-attachments/assets/f263a516-cb37-456d-9550-c2baa623add1" />

### Mapa del sistema

- **Estado:** Tal como dice el enunciado de la unidad 3, el estado de cada particula es almacenado en src/simulation/createSimulation.js (positionBuffer, velocityBuffer), y esto se encarga como dice casi explicitamente de almacenar la posición y la velocidad de estas particula, alamcenados en arreys.

```js
  const positionBuffer = instancedArray(count, 'vec3');
  const velocityBuffer = instancedArray(count, 'vec3');
```

- **Fuerzas:** Las fuerzas acumuladas en este sistema son dispersión, viento (ejes X, Y, Z), atracción y repulsión radial, vórtice, rayos (variaciones caóticas de trayectoria), ramificación fractal (Sistema L) y resistencia (fricción o drag). Varias de estas ya estaban incluidas y otras se incluyeron y modificaron.

|Fuerza|Dirección|Ecuación|
|------|--------|----------|
|Repulsión|Sentido contrario al mouse|F*disp* = (P/p)* S *disp* *E *disp*|
|Viento| Según el componente| F *viento* = (W *xy* + W *z*) * E *viento*|
|Radial| Hacia el mouse| <img width="474" height="83" alt="image" src="https://github.com/user-attachments/assets/84133464-16a0-44ab-a6bc-11d9ebfb3207" />|
|Vortice| Perpendicular al vector radial| <img width="473" height="61" alt="image" src="https://github.com/user-attachments/assets/949301e6-083b-47f5-a34e-3938bba3d8aa" />|
|"Rayos"| Sigue el mouse pero también ocila caoticamente| F *rayos* =( F *directa* + F *caotica*) * E *rayos*|
|Ramificación| Tiene una dirección radial pero rota como un abanico| <img width="204" height="66" alt="image" src="https://github.com/user-attachments/assets/87c7c78f-21d5-414b-bf78-446155e8471b" />|
|Resistencia| Opuesta a la velocidad| <img width="374" height="55" alt="image" src="https://github.com/user-attachments/assets/dffffb87-ad30-406e-bf11-32ba53f301a5" />|

- **Integración:** En cuanto a la integración de las fuerzas, es importante saber que al ser este un sistema Motion 101, para que funcione en este caso es necesario asignar la masa, que en este caso se toma como 1, para que asi la aceleración sea igual a la fuerza neta. La aceleración también es el cambio de la velocidad en el tiempo, por ende para calcular la velocidad lo que se hace es multiplicar la fuerza neta por el cambio en el tiempo y se le suma la velocidad anterior, para finalmente calcular la posición con la velocidad actual por el cambio del tiempo más la posición anterior.

- **Render:** Este calculo no se hace más de una vez porque la memoria del GPUweb esta compartida con la GPU del computador y también porque se separa el calculo (compute shader, el cual almacena los nuevos datos en los buffers de posición y velocidad) del dibujo (sistema de nodos que leen la información de la GPU)

- **Controles:**
|Tecla/combinación|Acción/Slider|Intención|
|-------------------|---------------|-----------|
| (W) | Apagar y prender la influencia del viento | Poder decidir en que partes no usar el viento |
| Flechas horizontales | Aumentar o disminuir la infuencia del viento en x | para determinar que tanta fuerza tendrá |
| Flechas verticales | Aumentar o disminuir la infuencia del viento en y |  para determinar que tanta fuerza tendrá |
| 1 y 2 |  Aumentar o disminuir la infuencia del viento en z |  para determinar que tanta fuerza tendrá |
| 3 y 4 | Controla la velocidad | Disminuir o aumentar la velocidad maxima |
| (L) | Activa la función de los "rayos" | En realidad más que rayos e sun estado donde las particulas pueden sentirse muy o muy poco atraidas al movimeinto del mouse |
| 5 y 6 | Disminuye o aumenta la fuerza de esos "rayos" | Esto controla que tan dispersas se ven las particulas |
| (V) | Activa o desactiva el vortice | pararlo en los momentos necesarios |
| 7 y 8 | Disminuye o aumenta la fuerza del vortice | pararlo en los momentos necesarios |
| (T) | Activa el sistema de ramas | Para cambiar el momento rápidamente|
| (C) | Color | Cambiar el color con degradados tematicos | 
| (B) | Cambio de borde | Cambia entre 3 estados: borde firme, borde flexible y sin borde |
| (A) | Atracción | Activa y desactiva al tenerlo presionado | 
| (S) | Repulsión | Activa y desactiva al tenerlo presionado |
| (D) | Repulsión (entre ellas) | es lo que ayuda a generar ondas|
