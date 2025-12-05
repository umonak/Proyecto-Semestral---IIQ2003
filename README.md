# Proyecto Semestral: Modelamiento de Emisión de Contaminantes en Ríos

### Información del Curso
* **Universidad:** Pontificia Universidad Católica de Chile
* **Departamento:** Departamento de Ingeniería Química y Bioprocesos
* **Curso:** IIQ2003- Fenómenos de Transporte 
* **Profesor:** Felipe Huerta Pérez
* **Semestre:** Segundo Semestre del 2025

---

### Detalles de la Entrega
* **Integrantes:** Benjamín Mondaca, Clemente de Geyter y Rona Tempel.
* **Ayudante:** Carlos Soto 
* **Profesor:** Felipe Huerta 
* **Fecha:** 9 de diciembre de 2025 

---

## Descripción general
Este proyecto aborda el modelamiento de la dispersión de contaminantes en cursos de agua (ríos o canales), enfocándose en la contaminación de estos, un problema crítico y de alta relevancia en Chile. La crisis hídrica en el país depende de muchos factores, siendo el desecho de productos químicos (como farmacéuticos o agroindustriales) uno de los factores más relevantes, donde un 14% de los problemas hídricos provienen de desechos químcos en la agroindustria (Universidad de Chile, 2022). 

Asimismo, la contaminación de cursos de agua representa uno de los problemas más relevantes en la actualidad, de manera que se tienen distintos Objetivos de Desarrollo Sustentable (ODS) relacionados a la contaminación de cursos de agua: ODS 6 (Agua limpia y saneamiento), ODS 12 (Producción y consumo responsables), ODS 14 (Vida submarina) y ODS 15 (Vida de ecosistemas terrestres) (Naciones Unidas, s.f.).

De esta manera, el objetivo de este proyecto es realizar un modelo relacionado a los fenómenos de transporte que rigen el curso del agua. En este caso, se consideró un modelo 2-D en estado estacionario, lo que permitirá simular la forma en que los contaminantes vertidos se distribuyen longitudinal y transversalmente a lo largo del río, con el principal objetivo de tener una idea sobre parámetros óptimos a la cual los distintos actores descargan sus desechos. 

## Sistema modelado
El transporte y dispersión de los contaminantes se rige principalmente por los siguientes fenómenos:
* **Advección:** Corresponde al fenómeno en donde los contaminantes son empujados por la velocidad de la corriente del río en la dirección longitudinal ($x$). Este fenómeno es el dominante en este eje.
* **Difusión turbulenta:** Se refiere a la dispersión del contaminante en la dirección transversal ($y$) debido a la turbulencia del flujo.
* **Reacción química:** Corresponde, en este caso, a la desintegración de los contaminantes (p. ej., biodegradación) en una velocidad de reacción de primero orden.

A su vez, para la simplificación del problema y un modelamiento correcto, los supuestos supuestos clave son:
* **Estado estacionario ($\frac{dC}{dt}$ = 0):** Concentración del contaminante y el caudal del río son constantes con el tiempo
* **Concentración constante en $z$:** Se asume que el río es poco profundo, permitiendo que se alcance una distribución uniforme del contaminante en la dirección vertical ($z$).
* **Difusión despreciable en $x$:** Transporte por advección es mucho mayor que el transporte por difusión en la dirección longitudinal, debido a la alta velocidad del flujo.
* **Difusividad transversal $y$ velocidades constantes:** $\epsilon_{y}$, $u(x,y)$, y $v(x,y)$ se asumen constantes ($\epsilon_{0}$, $u_{x}$, $v_{y}$) para simplificar la resolución numérica.

En base a lo mencionado con anterioridad, es posible definir la ecuación diferencial parcial (EDP) que define el problema de la siguiente manera:

![EDP problema.](./Imágenes/EDP.png)

con $C(x,y)$ la concentración del contaminante, $u$ y $\nu$ las velocidades longitudinal y transversal, $\epsilon_{y}$ el coeficiente de difusión turbulenta lateral y $k_{e}$ constante de la reacción de primer orden. Las condiciones de borde de este problema corresponden a 
* **C.B. Neumann (Paredes del Río):** $$\frac{dc}{dy}(y=0)=\frac{dc}{dy}(y=W)=0$$
* **C.B. Dirichlet (Entrada en $x=0$):** $$C(0,a\le y\le b)=C_{b} \quad \text{ y } \quad C(0,0\le y<a \text{ y } b<y\le W)=C_{0}$$
![Diagrama del proyecto](./imagenes/diagrama.png)

## Método numérico
Para resolver la EDP lineal de segundo orden del sistema, se ha seleccionado el método de Diferencias Finitas en conjunto con el método de solución iterativa de Sobre-Relajación Sucesiva (SOR). 

# Discretización EDP
El método de Diferencias Finitas es adecuado para discretizar porque permite transformar la EDP en un sistema de ecuaciones lineales al discretizar el dominio (el río) en una malla (o meshgrid) de puntos o nodos $(N_i, N_j)$.
* **Derivadas Longitudinal ($$\frac{\partial C}{\partial x}$$) y Transversal ($$\frac{\partial C}{\partial y}$$):** Se usa una diferencia finita hacia atrás, entonces queda
* $$\frac{\partial C}{\partial x} \approx \frac{C_{i,j}-C_{i-1,j}}{\Delta x} $$
* $$\frac{\partial C}{\partial y} \approx \frac{C_{i,j}-C_{i,j-1}}{\Delta y} $$
  

## Instrucciones ejecución código 
## Resultados
## Referencias bibliográficas 
## Apéndice
