#include <stdio.h>
#include <stdlib.h>

// 1. Calculo de permutacao
unsigned long long fatorial(int n) {
    if (n == 0 || n == 1) return 1;
    return n * fatorial(n - 1);
}

unsigned long long permutacao(int n, int k) {
    return fatorial(n) / fatorial(n - k);
}

// 2. Principio das Casas de Pombo
void casas_de_pombo(int pombos, int casas) {
    int minimo = (pombos + casas - 1) / casas;
    printf("Pelo principio das casas de pombo, pelo menos %d pombos estarao na mesma casa.\n", minimo);
}

// 3. Probabilidade condicional
double probabilidade_condicional(double pa_e_b, double pb) {
    if (pb == 0) {
        printf("Probabilidade de B nao pode ser zero.\n");
        return -1;
    }
    return pa_e_b / pb;
}

// 4. Relacao de recorrencia simples (Fibonacci)
int recorrencia_fibonacci(int n) {
    if (n <= 1) return n;
    return recorrencia_fibonacci(n - 1) + recorrencia_fibonacci(n - 2);
}

// Função para raiz quadrada aproximada (método de Newton)
double raiz_quadrada(double x) {
    if (x < 0) return -1; // inválido para negativos
    double guess = x / 2.0;
    double epsilon = 0.00001;
    while ((guess * guess - x) > epsilon || (x - guess * guess) > epsilon) {
        guess = (guess + x / guess) / 2.0;
    }
    return guess;
}

// 5. Analise estatistica 
void analise_estatistica(double dados[], int tamanho) {
    double soma = 0, media, variancia = 0, desvio;

    for (int i = 0; i < tamanho; i++) {
        soma += dados[i];
    }
    media = soma / tamanho;

    for (int i = 0; i < tamanho; i++) {
        double diff = dados[i] - media;
        variancia += diff * diff; // substituindo pow(diff, 2)
    }
    variancia /= tamanho;
    desvio = raiz_quadrada(variancia); // substituindo sqrt

    printf("Media: %.2lf\n", media);
    printf("Variancia: %.2lf\n", variancia);
    printf("Desvio padrao: %.2lf\n", desvio);
}

// Programa principal
int main() {
    int opcao;
    printf("Sistema de Analise Combinatoria e Estatistica\n");
    printf("Escolha uma opcao:\n");
    printf("1 - Calcular permutacao\n");
    printf("2 - Principio das casas de pombo\n");
    printf("3 - Probabilidade condicional\n");
    printf("4 - Relacao de recorrencia (Fibonacci)\n");
    printf("5 - Analise estatistica\n");
    scanf("%d", &opcao);

    switch(opcao) {
        case 1: {
            int n, k;
            printf("Digite n e k: ");
            scanf("%d %d", &n, &k);
            printf("Permutacao P(%d, %d) = %llu\n", n, k, permutacao(n, k));
            break;
        }
        case 2: {
            int pombos, casas;
            printf("Digite o numero de pombos e de casas: ");
            scanf("%d %d", &pombos, &casas);
            casas_de_pombo(pombos, casas);
            break;
        }
        case 3: {
            double paeb, pb;
            printf("Digite P(A e B) e P(B): ");
            scanf("%lf %lf", &paeb, &pb);
            double resultado = probabilidade_condicional(paeb, pb);
            if (resultado != -1)
                printf("P(A|B) = %.4lf\n", resultado);
            break;
        }
        case 4: {
            int n;
            printf("Digite n para calcular F(n) de Fibonacci: ");
            scanf("%d", &n);
            printf("F(%d) = %d\n", n, recorrencia_fibonacci(n));
            break;
        }
        case 5: {
            int tamanho;
            printf("Digite o numero de elementos: ");
            scanf("%d", &tamanho);
            double *dados = (double *) malloc(tamanho * sizeof(double));
            if (!dados) {
                printf("Erro ao alocar memoria.\n");
                return 1;
            }
            printf("Digite os elementos:\n");
            for (int i = 0; i < tamanho; i++) {
                scanf("%lf", &dados[i]);
            }
            analise_estatistica(dados, tamanho);
            free(dados);
            break;
        }
        default:
            printf("Opcao invalida.\n");
    }
    system("pause");
    return 0;
}
