En la infraestructura de AWS tenemos los siguientes componentes:

* Regiones
* Zonas de Disponibilidad
* Zonas Locales
* Zonas de Longitud de Onda

# Regiones vs Zonas de Disponibilidad

Cuando Amazon monta un Data Center en una región, no lo monta aislado, sino que monta un clúster de Data Centers para que si falla uno esté el otro disponible.

Sin embargo, esto no implica que cada Data Center sea una zona de disponibilidad. Las zonas de disponibilidad son **distintos clúster de data centers dentro de una misma región**.

![[Pasted image 20240816003436.png]]

Las regiones normalmente suelen tener tres o más zonas de disponibilidad.

En una estructura de diseño en la que estamos usando varias EC2 con un balanceador de carga lo correcto sería colocar cada EC2 en una Avaliability Zone (AZ) diferente, lo cual me protege de un fallo en una AZ.

Sin embargo, si coloco las EC2 en distintas regiones ya no estaríamos hablando de balanceador de carga, sino de Recuperación de Desastres o Disaster Recovery, que tiene unos costes diferentes (mayores).

# Puntos de presencia

También son centros de cómputo, en los que no hay AZ, pero que si tienen algunos servicios, como DNS.

# ¿Cómo elegir mi región?

Debo elegir mi región en base a 4 criterios:

* Por cuestiones legales (p.e. en la comunidad europea deben estar los datos de los alumnos europeos)
* Por cercanía a mis clientes.
* Por la disponibilidad de ciertos servicios en una región.
* Por precio.


