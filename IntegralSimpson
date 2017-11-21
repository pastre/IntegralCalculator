#include <stdio.h>
#include <stdlib.h>
#include <math.h>

float calcF(float x){
	return pow(M_E, -x/10)*cos(x - 2) - sin(2 * x);
}

float calcH(float x0, float x1, int n){
	return (x1 - x0)/n;
}

float calcVarUmTerco(float x0, float x1, float passo){
	float i, res = 0;
	int mult = 4;

	for(i = x0; i < x1; i+= passo){
		res += mult * calcF(i);
		if(mult == 4)
			mult = 2;
		else
			mult = 4;
			//printf("TEMPRES: %f\n", res);
	}

	return res + 4 * calcF(i);
}

float integraUmTerco(float x0, float x1, float n){
	float passo = calcH(x0, x1, n);
	float car = calcVarUmTerco(x0 + passo, x1 - passo, passo);
//	printf ("CAR: %f\n", car);
	return passo * (calcF(x0) + calcF(x1) + car )/ 3;
}

float calcVarTresOitavos(float x0, float x1, float passo){
	float i, res = 0;
	int mult = 3, cont = 1;

	for(i = x0; i<=x1; i += passo){
		if( cont % 3 == 0)
			mult = 2;
		else
			mult = 3;
		res += mult * calcF(i);
	    cont ++;
	}

	return res;


}

float integraTresOitavos(float x0, float x1, float n){
	float passo = calcH(x0, x1, n);
	float car = calcVarTresOitavos(x0 + passo, x1 - passo, passo);

	return 3*passo*(calcF(x0) + calcF(x1), car)/8;
}

int main(int argc, char * * argv){
	if(argc != 4){
		printf("FORMATACAO ERRADA! Chame o programa com:\nintegra .exe limiteInferior limiteSuperior nIntervalos\n");
		exit(1);
	}
	float x0 = strtof(argv[1], NULL), x1 = strtof(argv[2], NULL), h, res;
	int n = strtol(argv[3], NULL, 10);
	h = calcH(x0, x1, n);
	int i;
	if(n % 2 == 0){
		res = integraUmTerco(x0, x1, n);
	}else if(n % 3 == 0){
		res = integraTresOitavos(x0, x1, n);
	}
	else{
		res += integraUmTerco(x0, x1 - 4*calcH(x0, x1, n), n);
		res += integraTresOitavos( x1 -  4*calcH(x0, x1, n), x1, n);
	}

	printf("Integrando de %f a %f com passo %f...\nResultado: %f\n",x0, x1, h, res);
//	system("PAUSE");
	return 0;
}
