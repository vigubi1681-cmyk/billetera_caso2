Integrantes – Grupo 9

- Víctor Ernesto Gutiérrez Birot
- Renzo Enrique Lara Condori
- Karen Narciso Checasaca
- Ana Gabriela Silva Yauyo



# Caso 2: Billetera Digital (Angular)

Una billetera digital sencilla hecha con Angular para la evaluación T1 del curso Soluciones Web y Aplicaciones Distribuidas. Permite recargar saldo, registrar gastos y ver el historial de movimientos. Todo vive en memoria: si recargas la página, la billetera vuelve a empezar con S/ 250.00.

## Cómo funciona

La app tiene dos componentes que se reparten el trabajo:

- **BilleteraComponent (padre):** guarda el saldo y la lista de movimientos. Muestra el saldo, el historial (el más reciente primero) y un mensaje cuando todavía no hay movimientos.
- **NuevoMovimientoComponent (hijo):** muestra el formulario con el tipo (recarga o gasto) y el monto. Valida lo que se escribe y, solo cuando el movimiento es válido, se lo avisa al padre. El hijo no toca el saldo ni el historial.

El padre le pasa el saldo al hijo con `input()`, y el hijo le avisa de un movimiento válido con `output()`.

## Reglas de la billetera

- El saldo inicial es S/ 250.00 y el historial empieza vacío.
- **Recarga:** suma un monto positivo al saldo.
- **Gasto:** resta un monto positivo, siempre que no supere el saldo disponible.
- Si el monto está vacío, no es un número o es cero o negativo, se rechaza y se muestra un    mensaje.
- Si un gasto es mayor al saldo, se muestra "Saldo insuficiente" y el botón queda deshabilitado.
- Un movimiento inválido nunca cambia el saldo ni el historial.

## Versiones utilizadas
# Caso2

- Angular CLI: 22.2.6
- Node.js: 22.23.4
- npm: 12.2.2
- Bootstrap: 5.3.9 (se instala con `npm install`)

## Cómo ejecutarlo

Se requiere tener instalados Node.js y Angular CLI (`npm install -g @angular/cli`).

1. Clona el repositorio y entra a la carpeta del proyecto:
   ```
   git clone https://github.com/vigubi1681-cmyk/billetera_caso2
   cd caso2
   ```
2. Instala las dependencias:
   ```
   npm install
   ```
3. Inicia la aplicación:
   ```
   ng serve
   ```
4. Abre http://localhost:4200/ en el navegador.

Si PowerShell bloquea el comando `ng`, ejecuta una vez
`Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned` o usa `ng.cmd` en lugar de `ng`.

## Estructura principal

```
src/app/
├── componentes/
│   ├── billetera/            # componente padre
│   └── nuevo-movimiento/     # componente hijo
├── modelos/
│   └── movimiento.ts         # tipo y forma de un movimiento
├── app.ts                    # contenedor de la aplicación
└── app.html
```

## Pruebas manuales

| Acción | Resultado esperado |
|---|---|
| Abrir la aplicación | Saldo S/ 250.00 e historial vacío |
| Recarga de S/ 100.00 | Saldo S/ 350.00, aparece en el historial |
| Gasto de S/ 50.00 | Saldo S/ 300.00, el gasto aparece antes que la recarga |
| Gasto de S/ 400.00 | Error de saldo insuficiente, saldo sigue en S/ 300.00 |
| Cero, negativo o monto vacío | Se rechaza, no cambia el saldo ni el historial |
