# Análisis de Calidad de Datos

##### ***Emma Arenas Villaverde***
***

<br>

## 1. Tratamiento de los Datos<a id="treatment"></a>

### 1.1. Importar Librerías<a id="libraries"></a>


```R
install.packages("readr") # para leer archivos CSV
install.packages("dplyr") # para manipulación de datos
library(readr) 
library(dplyr) 
```

### 1.2. Cargar Dataset <a id="data-info"></a>


```R
BBDD_Locales <- read_csv2("../data/BBDD_Locales.csv") #  la función read_csv2 viene configurada por defecto para utilizar el punto y coma como delimitador
```

<br>

## 2. Análisis <a id="analysis"></a>

### 2.1. Información de los Datos <a id="data-info"></a>


```R
dim(BBDD_Locales) # para obtener sus dimensiones
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>766</li><li>7</li></ol>




```R
str(BBDD_Locales) # para ver su estructura interna
```

    spc_tbl_ [766 × 7] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
     $ municipio   : chr [1:766] "Municipio29" "Municipio29" "Municipio29" "Municipio29" ...
     $ sector      : chr [1:766] "Menaje" "Otros" "No alimentario" "Otros" ...
     $ situacion   : chr [1:766] "calle" "calle" "calle" "calle" ...
     $ forma       : chr [1:766] "SL" "SL" "SA" "individual" ...
     $ superficie  : num [1:766] 99.3 22.5 NA 24.9 21.2 ...
     $ trabajadores: num [1:766] 6 3 3 1 2 5 3 4 1 4 ...
     $ antiguedad  : num [1:766] 36.5 14.2 9 11.4 17.1 26.9 13.3 13.5 29.6 6.4 ...
     - attr(*, "spec")=
      .. cols(
      ..   municipio = [31mcol_character()[39m,
      ..   sector = [31mcol_character()[39m,
      ..   situacion = [31mcol_character()[39m,
      ..   forma = [31mcol_character()[39m,
      ..   superficie = [32mcol_double()[39m,
      ..   trabajadores = [32mcol_double()[39m,
      ..   antiguedad = [32mcol_double()[39m
      .. )
     - attr(*, "problems")=<externalptr> 
    


```R
head(BBDD_Locales, n = 766) # para ver sus filas
```


<table class="dataframe">
<caption>A tibble: 766 × 7</caption>
<thead>
	<tr><th scope=col>municipio</th><th scope=col>sector</th><th scope=col>situacion</th><th scope=col>forma</th><th scope=col>superficie</th><th scope=col>trabajadores</th><th scope=col>antiguedad</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Municipio29</td><td>Menaje                  </td><td>calle           </td><td>SL        </td><td>99.32</td><td>6</td><td>36.5</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>SL        </td><td>22.51</td><td>3</td><td>14.2</td></tr>
	<tr><td>Municipio29</td><td>No alimentario          </td><td>calle           </td><td>SA        </td><td>   NA</td><td>3</td><td> 9.0</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>individual</td><td>24.85</td><td>1</td><td>11.4</td></tr>
	<tr><td>Municipio29</td><td>Equipamientos culturales</td><td>calle           </td><td>SA        </td><td>21.21</td><td>2</td><td>17.1</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>SA        </td><td>46.14</td><td>5</td><td>26.9</td></tr>
	<tr><td>Municipio29</td><td>No alimentario          </td><td>calle           </td><td>SA        </td><td>44.96</td><td>3</td><td>13.3</td></tr>
	<tr><td>Municipio29</td><td>Ocio y cultura          </td><td>centro comercial</td><td>SL        </td><td>35.16</td><td>4</td><td>13.5</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>SA        </td><td>20.48</td><td>1</td><td>29.6</td></tr>
	<tr><td>Municipio29</td><td>Menaje                  </td><td>calle           </td><td>SL        </td><td>57.44</td><td>4</td><td> 6.4</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>individual</td><td> 7.73</td><td>1</td><td>13.3</td></tr>
	<tr><td>Municipio29</td><td>Reparaciones            </td><td>calle           </td><td>SL        </td><td>44.75</td><td>4</td><td> 4.7</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>SA        </td><td>24.32</td><td>2</td><td>30.2</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>SL        </td><td>33.23</td><td>2</td><td> 7.6</td></tr>
	<tr><td>Municipio29</td><td>Menaje                  </td><td>calle           </td><td>individual</td><td>65.64</td><td>4</td><td>14.7</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>SA        </td><td>23.01</td><td>3</td><td>10.4</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>individual</td><td> 9.85</td><td>2</td><td>12.4</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>SL        </td><td>40.23</td><td>5</td><td>26.5</td></tr>
	<tr><td>Municipio29</td><td>Menaje                  </td><td>calle           </td><td>SL        </td><td>45.82</td><td>3</td><td>26.5</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>individual</td><td>10.30</td><td>1</td><td>18.1</td></tr>
	<tr><td>Municipio29</td><td>Equipamiento personal   </td><td>calle           </td><td>SL        </td><td>64.58</td><td>3</td><td> 3.0</td></tr>
	<tr><td>Municipio29</td><td>Enseñanza               </td><td>calle           </td><td>individual</td><td>43.54</td><td>3</td><td>50.3</td></tr>
	<tr><td>Municipio29</td><td>Menaje                  </td><td>centro comercial</td><td>SA        </td><td>48.11</td><td>3</td><td> 6.2</td></tr>
	<tr><td>Municipio29</td><td>Menaje                  </td><td>calle           </td><td>individual</td><td>61.69</td><td>2</td><td>32.7</td></tr>
	<tr><td>Municipio29</td><td>Otros                   </td><td>calle           </td><td>SL        </td><td> 5.26</td><td>2</td><td> 8.2</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>SA        </td><td>46.44</td><td>4</td><td> 5.9</td></tr>
	<tr><td>Municipio29</td><td>Enseñanza               </td><td>calle           </td><td>SL        </td><td>80.96</td><td>3</td><td>14.4</td></tr>
	<tr><td>Municipio29</td><td>Restauración            </td><td>calle           </td><td>SA        </td><td>69.24</td><td>3</td><td>19.0</td></tr>
	<tr><td>Municipio29</td><td>Alimentario             </td><td>calle           </td><td>individual</td><td> 9.98</td><td>1</td><td>16.3</td></tr>
	<tr><td>Municipio29</td><td>Restauración            </td><td>calle           </td><td>SA        </td><td>76.62</td><td>4</td><td> 3.8</td></tr>
	<tr><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td></tr>
	<tr><td>Municipio29</td><td>Alimentario          </td><td>calle</td><td>individual</td><td>12.23</td><td>1</td><td>13.7</td></tr>
	<tr><td>Municipio29</td><td>Sanidad              </td><td>calle</td><td>SL        </td><td>22.51</td><td>3</td><td> 7.6</td></tr>
	<tr><td>Municipio29</td><td>Otros                </td><td>calle</td><td>SL        </td><td>12.55</td><td>4</td><td> 9.6</td></tr>
	<tr><td>Municipio29</td><td>Restauración         </td><td>calle</td><td>SL        </td><td>59.56</td><td>4</td><td>25.1</td></tr>
	<tr><td>Municipio29</td><td>Sanidad              </td><td>calle</td><td>individual</td><td>11.51</td><td>1</td><td> 1.0</td></tr>
	<tr><td>Municipio29</td><td>Alimentario          </td><td>calle</td><td>SL        </td><td>34.74</td><td>3</td><td>39.4</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SL        </td><td>82.15</td><td>4</td><td>12.0</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>individual</td><td>37.58</td><td>2</td><td>30.2</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SA        </td><td>27.07</td><td>3</td><td>25.2</td></tr>
	<tr><td>Municipio29</td><td>Otros                </td><td>calle</td><td>SA        </td><td>16.45</td><td>1</td><td>13.6</td></tr>
	<tr><td>Municipio29</td><td>Restauración         </td><td>calle</td><td>SA        </td><td>51.91</td><td>4</td><td> 7.7</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SA        </td><td>38.09</td><td>4</td><td>20.9</td></tr>
	<tr><td>Municipio29</td><td>Alimentario          </td><td>calle</td><td>SL        </td><td>14.30</td><td>1</td><td>12.2</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SL        </td><td>96.53</td><td>4</td><td>17.4</td></tr>
	<tr><td>Municipio29</td><td>Otros                </td><td>calle</td><td>SA        </td><td>10.53</td><td>2</td><td>13.9</td></tr>
	<tr><td>Municipio29</td><td>Enseñanza            </td><td>calle</td><td>SL        </td><td>71.06</td><td>5</td><td>27.6</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SL        </td><td>68.50</td><td>4</td><td>17.0</td></tr>
	<tr><td>Municipio29</td><td>Alimentario          </td><td>calle</td><td>SL        </td><td>11.86</td><td>2</td><td> 7.8</td></tr>
	<tr><td>Municipio29</td><td>Restauración         </td><td>calle</td><td>SA        </td><td>35.91</td><td>3</td><td> 6.7</td></tr>
	<tr><td>Municipio29</td><td>Otros                </td><td>calle</td><td>SL        </td><td>40.58</td><td>2</td><td>16.8</td></tr>
	<tr><td>Municipio29</td><td>Restauración         </td><td>calle</td><td>SL        </td><td>48.83</td><td>4</td><td>11.0</td></tr>
	<tr><td>Municipio29</td><td>Equipamiento personal</td><td>calle</td><td>SL        </td><td>59.22</td><td>3</td><td>20.9</td></tr>
	<tr><td>Municipio29</td><td>Alimentario          </td><td>calle</td><td>SL        </td><td>16.06</td><td>2</td><td>15.1</td></tr>
	<tr><td>Municipio29</td><td>Otros                </td><td>calle</td><td>SL        </td><td> 8.71</td><td>1</td><td>15.8</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SA        </td><td>91.34</td><td>7</td><td>22.3</td></tr>
	<tr><td>Municipio29</td><td>Otros                </td><td>calle</td><td>individual</td><td>24.03</td><td>2</td><td> 4.0</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SA        </td><td>73.50</td><td>5</td><td> 3.4</td></tr>
	<tr><td>Municipio29</td><td>Alimentario          </td><td>calle</td><td>SL        </td><td>23.19</td><td>3</td><td>19.7</td></tr>
	<tr><td>Municipio29</td><td>Menaje               </td><td>calle</td><td>SL        </td><td>31.69</td><td>3</td><td>16.6</td></tr>
	<tr><td>Municipio29</td><td>Restauración         </td><td>calle</td><td>SL        </td><td>77.22</td><td>5</td><td>13.8</td></tr>
</tbody>
</table>



- **Número de registros**: la base de datos contiene un total de **766 registros**, donde cada uno ellos representa una entrada de datos correspondiente a `Municipio29`.  
- **Número de columnas**: la estructura de la base de datos cuenta con **7 columnas**, donde cada una de ellas posee atributos específicos relativos al municipio de estudio.  
- **Tipología de las variables**: en cuanto a la tipología de las variables, hay almacenados tanto datos de tipo numeric `num` (indicando números decimales), como de tipo character `chr` (reflejando cadenas de texto).

### 2.2. Detección de Registros Duplicados <a id="duplicates"></a>

En esta parte del estudio, se han identificado los registros duplicados y se han almacenado en `duplicados` para su visualización:


```R
duplicados<- BBDD_Locales %>% 
  filter(duplicated(.)) # para obtener sus duplicados
```


```R
head(duplicados)
```


<table class="dataframe">
<caption>A tibble: 2 × 7</caption>
<thead>
	<tr><th scope=col>municipio</th><th scope=col>sector</th><th scope=col>situacion</th><th scope=col>forma</th><th scope=col>superficie</th><th scope=col>trabajadores</th><th scope=col>antiguedad</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Municipio29</td><td>Menaje     </td><td>calle</td><td>SA        </td><td>16.45</td><td>1</td><td>16.2</td></tr>
	<tr><td>Municipio29</td><td>Alimentario</td><td>calle</td><td>individual</td><td>10.30</td><td>1</td><td>18.1</td></tr>
</tbody>
</table>



Tal y como se puede observar, se han detectado **2 registros duplicados**. A partir de aquí, se ha procedido a su eliminación, dejando al actual dataset sin duplicados.


```R
BBDD_Locales <- BBDD_Locales %>%
    distinct()
```

A continuación, se comprueba si se han eliminado correctamente:


```R
sum(duplicated(BBDD_Locales))
```


0


### 2.3. Detección de Valores “NA” <a id="na-values"></a>

> En Variable `superficie` : estimarlo con el estadístico **media**


```R
na_superficie <- any(is.na(BBDD_Locales$superficie)) # para detectar valores "NA"
na_superficie
```


TRUE


Una vez detectados los valores "NA", se realiza la estimación, asegurando excluir los valores faltantes en el cálculo mediante el argumento `na.rm = TRUE` :


```R
BBDD_Locales <- BBDD_Locales %>%
  mutate(superficie = ifelse(is.na(superficie), mean(superficie, na.rm = TRUE), superficie)) # para transformar las variables
```

> En Variable `trabajadores` : estimarlo con el estadístico **máximo**


```R
na_trabajadores <- any(is.na(BBDD_Locales$trabajadores)) # para detectar valores "NA"
na_trabajadores
```


TRUE


En cuanto a la columna `trabajadores` , sus valores "NA" han sido sustituidos por el valor máximo, nuevamente excluyendo los valores faltantes en el cálculo:


```R
BBDD_Locales <- BBDD_Locales %>%
  mutate(trabajadores = ifelse(is.na(trabajadores), max(trabajadores, na.rm = TRUE), trabajadores)) # para transformar las variables
```

Finalmente, se comprueba que ya no existen valores vacíos:


```R
sum(is.na(BBDD_Locales$superficie)) # para contar la cantidad de NA
sum(is.na(BBDD_Locales$trabajadores)) # para contar la cantidad de NA
```


0



0


### 2.4. Detección de Valores Atípicos <a id="atypical-values"></a>

> Box-plot

Se crea un gráfico de los valores atípicos de la columna `superficie`:


```R
boxplot_superficie <- boxplot(BBDD_Locales$superficie,
                             horizontal = TRUE,
                             border = "red",
                             main = "Box plot de valores atípicos de Superficie",
                             xlab = "Superficie") # para crear un gráfico box-plot
```


    
![png](output_37_0.png)
    


Se detectan **12 desviaciones**:


```R
atipicos_superficie <- boxplot_superficie$out # para extraer los atípicos del box-plot
atipicos_superficie
numero_atipicos_superficie <- length(atipicos_superficie) # para conocer el número de átipicos
numero_atipicos_superficie
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>358.65</li><li>345.27</li><li>364.19</li><li>363.84</li><li>370.98</li><li>334.64</li><li>349.5</li><li>397.07</li><li>358.93</li><li>361.02</li><li>129.65</li><li>373.53</li></ol>




12


A continuación, se realiza exactamente el mismo proceso para la columna `trabajadores` .


```R
boxplot_trabajadores <- boxplot(BBDD_Locales$trabajadores,
                            horizontal = TRUE,
                            border = "red",
                            main = "Box plot de valores atípicos de Trabajadores",
                            xlab = "Trabajadores") # para crear un gráfico box-plot
```


    
![png](output_41_0.png)
    


Se detectan **14 desviaciones**:


```R
atipicos_trabajadores <- boxplot_trabajadores$out # para extraer los atípicos del box-plot
atipicos_trabajadores
numero_atipicos_trabajadores <- length(atipicos_trabajadores) # para conocer el número de átipicos
numero_atipicos_trabajadores
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>21</li><li>18</li><li>21</li><li>16</li><li>20</li><li>18</li><li>19</li><li>21</li><li>18</li><li>18</li><li>21</li><li>18</li><li>12</li><li>18</li></ol>




14


> Z-score

Respecto al método z-score, primeramente se usa la función `scale()` a fin de calcular las desviaciones de `superficie`. Luego, se establece un **umbral de 2** para identificar valores atípicos.


```R
z_scores_superficie <- scale(BBDD_Locales$superficie) # para calcular las desviaciones
atipicos_z_score_superficie <- which(abs(z_scores_superficie) > 2)
atipicos_z_score_superficie
numero_atipicos_superficie2 <- length(atipicos_z_score_superficie) # para conocer el número de átipicos
numero_atipicos_superficie2
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>90</li><li>111</li><li>186</li><li>260</li><li>270</li><li>306</li><li>334</li><li>339</li><li>347</li><li>451</li><li>696</li></ol>




11


Ante esto, se observa que la diferencia de desviación entre métodos es de **1**. Esto se debe a que box-plot se basa en cuartiles y rangos intercuartiles (IQR) para identificar valores atípicos, lo que puede llevar a que los valores extremos se consideren atípicos solo si están muy lejos de la mayoría de los datos. El método z-score, por su parte, identifica un número diferente de valores atípicos; ya que se centra en la distancia entre cada punto de
datos y la media.


```R
plot(z_scores_superficie, main = "Z-Scores de Superficie", xlab = "Índice", ylab = "Z-Score",
     pch = 19, col = ifelse(abs(z_scores_superficie) > 2, "red", "black"))
```


    
![png](output_48_0.png)
    


Con la columna `trabajadores` se hace exactamente lo mismo, y esta vez la diferencia ha
sido nula:


```R
z_scores_trabajadores <- scale(BBDD_Locales$trabajadores) # para calcular las desviaciones
atipicos_z_score_trabajadores <- which(abs(z_scores_trabajadores) > 2)
atipicos_z_score_trabajadores
numeros_atipicos_trabajadores2 <- length(atipicos_z_score_trabajadores) # para conocer el número de átipicos
numeros_atipicos_trabajadores2
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>85</li><li>90</li><li>111</li><li>186</li><li>260</li><li>270</li><li>306</li><li>334</li><li>339</li><li>347</li><li>412</li><li>451</li><li>602</li><li>696</li></ol>




14


En este caso, puede ser que los datos sigan una distribución relativamente simétrica y los
valores atípicos se encuentren lejos de la media.


```R
plot(z_scores_trabajadores, main = "Z-Scores de Trabajadores", xlab = "Índice", ylab = "Z-Score",
     pch = 19, col = ifelse(abs(z_scores_trabajadores) > 2, "red", "black"))
```


    
![png](output_52_0.png)
    


<br>

## 3. Algunos Cálculos Estadísticos... <a id="calculations"></a>

> Superficie media por forma mercantil


```R
resultados_superficie <- BBDD_Locales %>%
  group_by(forma) %>%
  summarize(superficie_media = mean(superficie, na.rm = TRUE))
resultados_superficie
```


<table class="dataframe">
<caption>A tibble: 4 × 2</caption>
<thead>
	<tr><th scope=col>forma</th><th scope=col>superficie_media</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>SA         </td><td> 59.61605</td></tr>
	<tr><td>SL         </td><td> 46.13969</td></tr>
	<tr><td>cooperativa</td><td>361.38500</td></tr>
	<tr><td>individual </td><td> 30.49525</td></tr>
</tbody>
</table>



> Antigüedad mínima y máxima por situación del local


```R
resultados_antiguedad <- BBDD_Locales %>%
  group_by(situacion) %>%
  summarize(
    antiguedad_minima = min(antiguedad, na.rm = TRUE),
    antiguedad_maxima = max(antiguedad, na.rm = TRUE)
  )
resultados_antiguedad
```


<table class="dataframe">
<caption>A tibble: 2 × 3</caption>
<thead>
	<tr><th scope=col>situacion</th><th scope=col>antiguedad_minima</th><th scope=col>antiguedad_maxima</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>calle           </td><td>0.5</td><td>79.8</td></tr>
	<tr><td>centro comercial</td><td>0.7</td><td>36.9</td></tr>
</tbody>
</table>

