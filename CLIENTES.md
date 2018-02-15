# Cliente Multicaja Digital

## Definición
Un Cliente Multicaja es una persona natural que posee al menos un `rut` y un `email`.

## Clave
Un Cliente Multicaja puede registrarse y obtener una clave, la que será un número de 4 dígitos.
Para autenticarse, el cliente puede usar la tupla (`rut`, `clave`) o la tupla (`email`, `clave`)

## Datos de contacto
Al menos, todo Cliente Multicaja debe indicar un email. Opcionalmente, podrá indicar también un celular.
Los datos de contacto pueden estar validados o no. Estar validado significa que el cliente nos demostró estar en posesión de ese dato. 
En los correos, esto se verifica enviando un email con un link que el usuario debe clickear. 
En los celulares, se envía un SMS con un cdigo que el cliente debe ingresar en nuestra web.
Cuando un dato de contacto está validado, sólo se puede cambiar en la medida que el nuevo dato esté validado también.
