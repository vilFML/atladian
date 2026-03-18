Tarea 1: Juego de tenis

Juego corre siempre (ciclo `while`), condiciones para que termine el juego:
while (juego corriendo):
	Algún jugador llega a los 45 ptos, termina juego.
	`if ptosA == 45 or ptosB == 45`
		dar ganador
		break ciclo
	En caso de ambos en 40 ptos.: Desempate, nuevo bucle `while`:
	`if ptosA == 40 and ptosB == 40:`
		nuevo bucle while
		`while:` siempre activo
			`if` alguno tiene 45 ptos:
				salir break
			nuevo sistema de ptaje: siguen con 40 ptos, pero ganador se le asigna ventaja
			`input` ganador de punto
			`if` tenia ventaja
				dar 5 ptos
				break ciclo interior
			`if` no tenía ventaja y el otro tampoco, dar ventaja al ganador
				dar ventaja
			`if` si no tenia ventaja y el otro sí, quitársela al otro
				quitar ventaja al perdedor
		`check` si alguno tiene 45 ptos.
		Ingresar ganador de punto, sumarle 5


\* Cómo tener ganador y perdedor?
siempre se están checkeando los ptajes de ambos jugadores, de ahi se podría sacar.

if  ganador no tenia ventaja y 