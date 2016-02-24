# 24.febrero.2016

#### 24 de febrero###

##### ejercicio clase
### bajar la base de datos  Variables del cuestionario de ocupación y empleo I del portal del INEGI del segundo trimestre 
###del 2015 
##Importar la base de datos .dbf en R
#### seleccionar solo a las entidades... 
### etiquetar las preguntas ¿Aproximadamente cuántas personas, incluyendo al dueño, laboran donde trabaja ...?p3L
###NO HACERLO###1) 1 a 5 personas, 2) 6 a 10, 3) 11 a 20, 4) 21 a 50 y 5) 51 y mas 
##¿La jornada de trabajo de ... es
###NO HACERLO### 1... dia, 2 ... noche, 3 mixto o rola turno, 4 no sabe
## p2e... 
###NO HACERLO###1) ausente temporal, 2) pensionado o jubilado, 3) se dedica al hogar o tiene limitaciones, 4) otra condicion, 9) no sabe
### hacer 3 tablas expandidas de las variables que etiquetaron con sexo.... ####NUEVO#####

###importar
require(foreign)
cuestionario<-read.dbf("C:\\Users\\SAQLA-C12\\Downloads\\coe1t215.dbf")
cuestionario<-data.frame(cuestionario)

tablasonora <- subset (cuestionario, (ENT ==26))

###pregunta 1
tablasonora$P3L<-ordered(tablasonora$P3L,levels=c("01","02","03","04","05","06","07","08","09","10","11","99"),labels=c("1 persona","2 a 5 personas","6 a 10 personas","11 a 15 personas","16 a 20 personas","21 a 30 personas","31 a 50 personas","51 a 100 personas","101 a 250 personas","251 a 500 personas","501 y más personas","No sabe"))
table(tablasonora$P3L) 
View(table(tablasonora$P3L))

###pregunta 2
tablasonora$P5<-ordered(tablasonora$P5,levels=c("1","2","3","4","9"),labels=c("de día? (entre las 6 am y las 8 pm)","de noche? (entre las 8 pm y las 6 am)","mixta?","rola turnos?","No sabe"))
table(tablasonora$P5) 
View(table(tablasonora$P5))

###pregunta 3
tablasonora$P2E<-ordered(tablasonora$P2E,levels=c("1","2","3","4","5","6","9"),labels=c("una persona temporalmente ausente de su actividad u oficio?","pensionado o jubilado de su empleo? estudiante?","una persona que se dedica a los quehaceres de su","una persona con alguna limitación física o mental que le impide trabajar por el resto de su vida?","una persona con alguna limitación física o mental que le impide trabajar por el resto de su vida?","Otra condición"," No sabe"))
table(tablasonora$P2E) 
View(table(tablasonora$P2E))
table(tablasonora$P2E)

### cruzar dos preguntas y hacer tabla
###primero etiquetamos lapregunta con la cual vamos a hacer la tabla
tablasonora$P1<-ordered(tablasonora$P1,levels=c("1","2"),labels=c("SI TRABAJA","NO TRABAJA"))
table(tablasonora$P1) 
View(table(tablasonora$P1))

#CRUZAR TABLAS

install.packages("questionr")
library (questionr)
tabla1<-wtd.table(tablasonora$P3L,tablasonora$P1,weights =tablasonora$FAC)
tabla1
tabla2<- wtd.table(tablasonora$P5,tablasonora$P1,weights =tablasonora$FAC)
(tabla2)
tabla3<- wtd.table(tablasonora$P2E,tablasonora$P1,weights =tablasonora$FAC)
(tabla3)
