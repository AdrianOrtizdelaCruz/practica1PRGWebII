# practica1PRGWebII

# Respuestas:

1. Vue no detecta cambios dentro de objetos reactivos de la forma que esperarías. ¿Cómo podrías observar un cambio en una propiedad anidada?
Vue 3 con reactive() no rastrea cambios en propiedades anidadas de forma automática. Para observar cambios dentro de un objeto, es necesario usar watch() con la opción { deep: true }. Esto permite detectar modificaciones en cualquier propiedad dentro del objeto.

2. watch() permite escuchar cambios en propiedades específicas dentro de reactive(), explica cómo funciona.
watch() en Vue se usa para observar cambios en propiedades y ejecutar una función cuando cambian. Si se observa un objeto reactivo completo, Vue solo detectará cambios en la referencia del objeto, no en sus propiedades internas, a menos que se use { deep: true }. También se puede observar propiedades individuales usando una función de retorno.

3. ¿Cómo harías que un watch() detecte cambios en stock dentro de un array de productos?
Para detectar cambios en stock dentro de una lista de productos, se puede usar watch() en un mapeo de la propiedad stock, como en el código anterior:

watch(
  () => inventario.map(producto => producto.stock),
  (newStocks, oldStocks) => {
    inventario.forEach((producto, index) => {
      if (newStocks[index] === 0) {
        producto.disponible = false;
      } else if (newStocks[index] > 0) {
        producto.disponible = true;
      }
    });
  },
  { deep: true }
);

Esto asegura que cada vez que un stock cambie en cualquier producto, se actualice correctamente la disponibilidad.
