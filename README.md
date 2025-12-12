# finanzas-personales

Sistema para finanzas personales

1. pantalla para gasto fijo
	- Nombre
	- Fecha
	- Monto
	- categoría
	- forma de pago
		- debito / efectivo
		- tdc
Funcionalidades:
	- alta de gasto
	- modificación
	- asignar forma de pago
		- asignar a tarjeta de crédito
		- pago sin crédito
2. pantalla de créditos
	- nombre
	- total
	- capital
	- mensualidad
	- fecha de pago
	- tasa de interés
Funcionalidades:
	- nuevo crédito
	- Actualizar capital
	- Actualizar mensualidad

3. pantalla para alta de tarjeta de crédito
	- banco
	- fecha de corte
	- días para pagar
	- línea de crédito
Funcionalidades
	- nueva tarjeta de crédito
	- modificar línea de crédito
	- desactivar tarjeta de crédito

4. pantalla para compra con tarjeta de crédito
	- descripción
	- monto
	- tipo de compra
		- msi
		- pago único
	- número de parcialidades
	- fecha de compra
	- categoría
Funcionalidades
	- nueva compra
	- adelanto de mensualidad
	- cancelar compra / devolución de dinero
	
5. pantalla de resumen / calendarío de pagos
	- lista + total de pagos del mes anterior (resumen) 
	- lista + total de pagos del mes (resumen) 
	- lista + total de pagos del siguiente mes (resumen) 
	- calendario de pagosde créditos y tarjetas de crédito

6. Pantalla para indicar que ya fue pagado por mes
	- lista de pagos:
		- créditos
		- tdc
		- gastos fijos
funcionalidad
	- hacer check de que pagos se completaron para que aparezcan como ok en el calendario
7. Pantalla para registro de ingresos
	- descripción
	- monto
	- es recurrente?
	- fecha de ingreso
	


Tablas:

-- catalogos -- 

categoria
- id
- nombre
- estatus
[suscriptciones, hogar, movilidad]

forma_pago
- id
- nombre
[efectivo, debito, credito]

banco
- id
- nombre

tipo_pago
- id
- nombre
[gasto_fijo, credito, tdc]

-- tablas de flujo --

gasto_fijo
- id
- categoria_id
- nombre
- monto 
- monto_opcional
- estatus

pago_gasto_fijo
- id
- gasto_fijo_id
- forma_pago_id
- monto
- fecha_pago

crédito
- nombre
- fecha_inicio
- meses
- tasa_interés
- capital_original
- capital_actual
- mensualidad
- fecha_pago

pago_credito
- id
- credito_id
- monto
- cantidad_capital
- cantidad_interes
- cantidad_iva
- es_pago_a_capital

tarjeta_credito
- id
- banco_id
- descripcion_tarjeta
- linea_credito
- activa
- fecha_corte
- dias_para_pagar

compra_tdc
- id
- tarjeta_credito_id
- descripción
- monto
- monto_restante_por_pagar
- parcialidades
- esMSI
- fecha_compra
- estatus

pago_tdc
- id
- mes
- anio
- total_al_corte


calendario_pagos
- id
- tipo_pago_id
- esatus_pago_id
- pago_id
- fecha_pago
- fecha_limite_pago


Interfaces
1. pantalla para gasto fijo

GET /gastoFijo/{id}
GET /gastoFijo?pag={pag}&pagSize={pagSize}
POST /gastoFijo {nombre, fechaPago, monto, categoriaId, formaPagoId}
PUT /gastoFijo/{id} {nombre, monto, categoria, formaPago}
DELETE /gastoFijo/{id}
POST /gastoFijo/mandarTdc/

2. pantalla de créditos

GET /credito/{id}
GET /credito?pag={pag}&pagSize={pagSize}
POST /crédito {bancoId, descripcion, montoCapital, montoCapitalAlDia, mensualidad, fechaPago, tasaInteres}
PUT /crédito/{id} {bancoId, descripcion, montoCapital, montoCapitalAlDia, mensualidad, fechaPago, tasaInteres}
PUT /crédito/{id}/montoCapitalAlDia {montoCapitalAlDia}
PUT /crédito/{id}/mensualidad {mensualidad}


3. pantalla para alta de tarjeta de crédito

GET /tdc/{id}
GET /tdc?pag={pag}&pagSize={pagSize}
POST /tdc {bancoId, descripcion, lineaCredito, fechaCorte, diasParaPagar}
PUT /tdc/{id}/lineaCredito {lineaCredito}
DELETE /tdc/{id}


4. pantalla para compra con tarjeta de crédito

GET /compraTdc/{id}
GET /compraTdc?pag={pag}&pagSize={pagSize}
POST /compraTdc {tdcId, descripcion, monto, parcialidades, fechaCompra}
PUT /compraTDC/{id}/adelantoMensualidad {monto}
DELETE /compraTDC/{id}

5. pantalla de resumen / calendarío de pagos
POST /calendario/calculaCalendario {mes, anio}
GET /calendario?mes={mes}&anio={anio}


6. Pantalla para indicar que ya fue pagado por mes
POST /pago/credito {mes, anio, monto}
POST /pago/tdc {mes, anio monto}


	






