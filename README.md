#include <stdio.h>
#include <math.h>

#define N 5  // Número de elementos en el dataset

// Estructura del dataset con los valores de Batch Size y sus correspondientes valores de salida
typedef struct {
    double x[N];  // Variable independiente (Batch Size)
    double y[N];  // Variable dependiente
} DataSet;

// Función para inicializar el dataset
void initializeDataSet(DataSet *dataSet) {
    // Valores predefinidos (puedes cambiar estos valores)
    dataSet->x[0] = 5;   dataSet->y[0] = 3;
    dataSet->x[1] = 10;  dataSet->y[1] = 6;
    dataSet->x[2] = 15;  dataSet->y[2] = 9;
    dataSet->x[3] = 20;  dataSet->y[3] = 12;
    dataSet->x[4] = 25;  dataSet->y[4] = 15;
}

// Función para calcular la regresión lineal
void calculateRegression(const DataSet *dataSet, double *beta0, double *beta1) {
    double sumX = 0, sumY = 0, sumXY = 0, sumX2 = 0;
    for (int i = 0; i < N; i++) {
        sumX += dataSet->x[i];
        sumY += dataSet->y[i];
        sumXY += dataSet->x[i] * dataSet->y[i];
        sumX2 += dataSet->x[i] * dataSet->x[i];
    }
    double meanX = sumX / N;
    double meanY = sumY / N;
    *beta1 = (sumXY - N * meanX * meanY) / (sumX2 - N * meanX * meanX);
    *beta0 = meanY - (*beta1) * meanX;
}

// Función para calcular la correlación y el coeficiente de determinación (R^2)
void calculateCorrelationAndDetermination(const DataSet *dataSet, double *correlation, double *rSquared) {
    double sumX = 0, sumY = 0;
    for (int i = 0; i < N; i++) {
        sumX += dataSet->x[i];
        sumY += dataSet->y[i];
    }
    double meanX = sumX / N;
    double meanY = sumY / N;

    double sumNumerator = 0, sumXDenominator = 0, sumYDenominator = 0;
    for (int i = 0; i < N; i++) {
        double xDiff = dataSet->x[i] - meanX;
        double yDiff = dataSet->y[i] - meanY;
        sumNumerator += xDiff * yDiff;
        sumXDenominator += xDiff * xDiff;
        sumYDenominator += yDiff * yDiff;
    }

    *correlation = sumNumerator / sqrt(sumXDenominator * sumYDenominator);
    *rSquared = (*correlation) * (*correlation);
}

// Función para predecir el valor de y dado un valor de x (Batch Size)
double predict(double beta0, double beta1, double x) {
    return beta0 + beta1 * x;
}

int main() {
    DataSet dataSet;
    initializeDataSet(&dataSet);

    double beta0, beta1;
    calculateRegression(&dataSet, &beta0, &beta1);

    // Imprimir la ecuación de regresión
    printf("Ecuación de Regresión: y = %.2f + %.2f * x\n", beta0, beta1);

    // Calcular la correlación y el coeficiente de determinación (R^2)
    double correlation, rSquared;
    calculateCorrelationAndDetermination(&dataSet, &correlation, &rSquared);
    printf("Correlación: %.2f\n", correlation);
    printf("Coeficiente de Determinación (R^2): %.2f\n", rSquared);

    // Realizar cinco predicciones para diferentes valores de Batch Size
    double batchSizes[] = {5, 10, 15, 30, 50};
    int numPredictions = sizeof(batchSizes) / sizeof(batchSizes[0]);

    for (int i = 0; i < numPredictions; i++) {
        double predictedY = predict(beta0, beta1, batchSizes[i]);
        printf("Predicción para Batch Size %.2f: y = %.2f\n", batchSizes[i], predictedY);
    }

    return 0;
}
Práctica 4 Programación, regresión cuadrática SANTIAGO JIMENEZ.c
Mostrando Práctica 4 Programación, regresión cuadrática SANTIAGO JIMENEZ.c.
Hands-on 4: Programming, Quadratic Regression
José Antonio Aviña Méndez
•
26 sept
100 puntos
1. Indicaciones en la presentación anexa
2- El programa -en Java-  se revisará de manera individual en fecha por definir.
3- Una vez evaluados se les solicitará que suban su código fuente a un Repositorio Público en Github del cual compartirán la URL pública para acceder al mismo.
4- Fecha de entrega por definir

Se comparte como enlace el DataSet del caso Benetton.

ProbEst 2024B
Presentaciones de Google
/100
/30
