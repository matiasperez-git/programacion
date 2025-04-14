# programacion
#include <stdio.h>

#define EST 5
#define MAT 3

int main() {
    float notas[EST][MAT];
    float promEst[EST], promMat[MAT];
    float maxEst[EST], minEst[EST];
    float maxMat[MAT], minMat[MAT];
    int apr[MAT] = {0}, rep[MAT] = {0};

    for (int i = 0; i < EST; i++) {
        printf("\nEstudiante #%d\n", i + 1);
        for (int j = 0; j < MAT; j++) {
            float n;
            do {
                printf("Nota materia #%d (0-10): ", j + 1);
                if (scanf("%f", &n) != 1) {
                    while (getchar() != '\n');
                    n = -1;
                }
                if (n < 0 || n > 10)
                    printf("⚠️  Nota inválida. Intente de nuevo.\n");
            } while (n < 0 || n > 10);
            notas[i][j] = n;
        }
    }

    for (int i = 0; i < EST; i++) {
        float suma = 0, max = notas[i][0], min = notas[i][0];
        for (int j = 0; j < MAT; j++) {
            float n = notas[i][j];
            suma += n;
            if (n > max) max = n;
            if (n < min) min = n;
        }
        promEst[i] = suma / MAT;
        maxEst[i] = max;
        minEst[i] = min;
    }

    for (int j = 0; j < MAT; j++) {
        float suma = 0, max = notas[0][j], min = notas[0][j];
        int a = 0;
        for (int i = 0; i < EST; i++) {
            float n = notas[i][j];
            suma += n;
            if (n > max) max = n;
            if (n < min) min = n;
            if (n >= 6) a++;
        }
        promMat[j] = suma / EST;
        maxMat[j] = max;
        minMat[j] = min;
        apr[j] = a;
        rep[j] = EST - a;
    }

    printf("\n--- Promedios por Estudiante ---\n");
    for (int i = 0; i < EST; i++)
        printf("Est #%d: %.2f\n", i + 1, promEst[i]);

    printf("\n--- Promedios por Materia ---\n");
    for (int j = 0; j < MAT; j++)
        printf("Mat #%d: %.2f\n", j + 1, promMat[j]);

    printf("\n--- Máx/Mín por Estudiante ---\n");
    for (int i = 0; i < EST; i++)
        printf("Est #%d - Max: %.2f | Min: %.2f\n", i + 1, maxEst[i], minEst[i]);

    printf("\n--- Máx/Mín por Materia ---\n");
    for (int j = 0; j < MAT; j++)
        printf("Mat #%d - Max: %.2f | Min: %.2f\n", j + 1, maxMat[j], minMat[j]);

    printf("\n--- Aprobados/Reprobados por Materia ---\n");
    for (int j = 0; j < MAT; j++)
        printf("Mat #%d - Aprob: %d | Reprob: %d\n", j + 1, apr[j], rep[j]);

    return 0;
}
