# Sistemaestoque
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX_OBJETOS 30

struct Objeto {
    char nome[30];
    char sala[30];
    char filial[30];
    int id;
};

int numObjetos = 0;
struct Objeto objetos[MAX_OBJETOS];

void imprimirRelatorio(struct Objeto obj) {
    printf("Nome do objeto: %s\n", obj.nome);
    printf("Sala individual do objeto: %s\n", obj.sala);
    printf("Filial do objeto: %s\n", obj.filial);
    printf("ID do objeto: %d\n", obj.id);
}

int main() {
    char funcionario[30];
    int id, opcao, idobj;
    bool continuar = true;

    while (continuar) {
        printf("Digite o Nome do Funcionário: ");
        fgets(funcionario, sizeof(funcionario), stdin);
        funcionario[strcspn(funcionario, "\n")] = '\0';

        printf("Digite o ID de Funcionário: ");
        scanf("%d", &id);
        getchar();

        printf("Escolha a operação:\n1 - Adicionar objeto;\n2 - Deletar objeto;\n3 - Relatório do objeto;\n4 - Consultar objetos por sala;\nOpção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                if (numObjetos < MAX_OBJETOS) {
                    printf("Digite o nome do novo objeto: ");
                    fgets(objetos[numObjetos].nome, sizeof(objetos[numObjetos].nome), stdin);
                    objetos[numObjetos].nome[strcspn(objetos[numObjetos].nome, "\n")] = '\0';

                    printf("Digite a sala individual do objeto: ");
                    fgets(objetos[numObjetos].sala, sizeof(objetos[numObjetos].sala), stdin);
                    objetos[numObjetos].sala[strcspn(objetos[numObjetos].sala, "\n")] = '\0';

                    printf("Digite a filial do objeto: ");
                    fgets(objetos[numObjetos].filial, sizeof(objetos[numObjetos].filial), stdin);
                    objetos[numObjetos].filial[strcspn(objetos[numObjetos].filial, "\n")] = '\0';

                    objetos[numObjetos].id = numObjetos;

                    printf("Por gentileza, confirme as informações do novo objeto;\n");
                    imprimirRelatorio(objetos[numObjetos]);

                    numObjetos++;
                } else {
                    printf("Limite de objetos atingido!\n");
                }
                break;

            case 2:
                printf("Digite o ID do objeto que deseja deletar: ");
                scanf("%d", &idobj);
                if (idobj >= 0 && idobj < numObjetos) {
                    for (int i = idobj; i < numObjetos - 1; i++) {
                        objetos[i] = objetos[i + 1];
                    }
                    numObjetos--;
                    printf("Objeto deletado com sucesso.\n");
                } else {
                    printf("ID de objeto inválido.\n");
                }
                break;

            case 3:
                printf("Digite o ID do objeto para gerar o relatório: ");
                scanf("%d", &idobj);
                if (idobj >= 0 && idobj < numObjetos) {
                    imprimirRelatorio(objetos[idobj]);
                } else {
                    printf("ID de objeto inválido.\n");
                }
                break;

            case 4:
                printf("Digite a sala para consultar os objetos: ");
                char sala_consulta[30];
                scanf("%s", sala_consulta);

                printf("Objetos na sala %s:\n", sala_consulta);
                for (int i = 0; i < numObjetos; i++) {
                    if (strcmp(objetos[i].sala, sala_consulta) == 0) {
                        imprimirRelatorio(objetos[i]);
                    }
                }
                break;

            default:
                printf("Opção inválida!\n");
                break;
        }
    }

    return 0;
}
