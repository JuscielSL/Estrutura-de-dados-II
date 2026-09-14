PARTE 1 – PESQUISA: BUBBLE SORT E QUICK SORT
Bubble Sort
O Bubble Sort é um algoritmo de ordenação que compara elementos vizinhos de um array e troca suas posições quando estão fora de ordem.

Durante cada passagem pelo array, os maiores elementos vão sendo deslocados para o final, como se "flutuassem" para suas posições corretas.

Como funciona
O algoritmo compara dois elementos vizinhos.
Se o primeiro for maior que o segundo, eles são trocados.
O processo continua até o final do array.
Após cada passagem, o maior elemento restante fica em sua posição.
O processo é repetido até que todos os elementos estejam ordenados.
Complexidade
Melhor caso: O(n), quando o array já está ordenado e não são necessárias trocas.
Caso médio: O(n²).
Pior caso: O(n²).
Memória
O Bubble Sort utiliza O(1) de memória adicional, pois realiza a ordenação diretamente no próprio array.

Vantagens
Fácil de entender.
Fácil de implementar.
Utiliza pouca memória.
Pode ser adequado para conjuntos de dados muito pequenos.
Limitações
Possui baixo desempenho para grandes quantidades de dados.
Realiza muitas comparações e trocas.
Não é adequado para aplicações que precisam ordenar grandes volumes de dados rapidamente.
Quando utilizar
O Bubble Sort pode ser utilizado em:

Arrays muito pequenos.
Exercícios acadêmicos.
Situações didáticas para estudar algoritmos de ordenação.
Situações em que a simplicidade seja mais importante que o desempenho.
Quando não utilizar
Não é recomendado para:

Grandes volumes de dados.
Sistemas que precisam de alto desempenho.
Situações em que a ordenação é executada frequentemente sobre grandes conjuntos de dados.
Quick Sort
O Quick Sort é um algoritmo de ordenação baseado na estratégia de divisão e conquista.

Ele escolhe um elemento chamado pivô e reorganiza os elementos de forma que os menores fiquem de um lado e os maiores do outro. Depois, o mesmo processo é aplicado recursivamente às partes menores.

Como funciona
Escolhe um elemento como pivô.
Divide o array em partes menores e maiores que o pivô.
Coloca o pivô em sua posição correta.
Aplica o mesmo processo à parte esquerda.
Aplica o mesmo processo à parte direita.
O processo continua até que todas as partes estejam ordenadas.
Complexidade
Melhor caso: O(n log n).
Caso médio: O(n log n).
Pior caso: O(n²), quando as divisões são muito desequilibradas.
Memória
O Quick Sort utiliza aproximadamente O(log n) de memória adicional em média devido à recursão, podendo chegar a O(n) no pior caso.

Vantagens
Possui excelente desempenho médio.
É eficiente para conjuntos de dados médios e grandes.
Geralmente realiza menos operações que o Bubble Sort em conjuntos maiores.
Utiliza uma estratégia eficiente de divisão e conquista.
Limitações
O desempenho pode chegar a O(n²) no pior caso.
A escolha do pivô influencia seu desempenho.
Utiliza recursão.
Quando utilizar
O Quick Sort é indicado para:

Arrays médios ou grandes.
Situações que exigem boa eficiência.
Aplicações que precisam ordenar grandes quantidades de dados.
Quando não utilizar
Não é a melhor escolha quando:

É necessário garantir O(n log n) no pior caso.
A implementação precisa ser extremamente simples.
O conjunto de dados é muito pequeno e a simplicidade é prioridade.
Comparação entre Bubble Sort e Quick Sort
      Característica

 Bubble Sort

 Quick Sort

        Princípio

 Comparação e troca de elementos vizinhos

 Divisão e conquista

      Melhor caso

 O(n)

 O(n log n)

      Caso médio

 O(n²)

 O(n log n)

      Pior caso

 O(n²)

 O(n²)

      Memória

 O(1)

 O(log n) em média

      Principal vantagem

 Simplicidade

 Eficiência média

      Principal limitação

 Baixo desempenho

 Pior caso O(n²)

      Aplicação recomendada

 Arrays pequenos e didáticos

 Arrays médios e grandes

      Os dois algoritmos conseguem produzir o mesmo resultado final, porém podem realizar quantidades muito diferentes de operações. Essa diferença se torna mais evidente conforme aumenta a quantidade de elementos.



PARTE 2 – EXPERIMENTO DE ORDENAÇÃO
Código utilizado
import random
 
 
def bubble_sort(arr):
    comparacoes = 0
    trocas = 0
    n = len(arr)
 
    for i in range(n - 1):
        houve_troca = False
 
        for j in range(n - 1 - i):
            comparacoes += 1
 
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                trocas += 1
                houve_troca = True
 
        if not houve_troca:
            break
 
    return comparacoes, trocas
 
 
def quick_sort(arr):
    comparacoes = 0
    movimentacoes = 0
 
    def ordenar(inicio, fim):
        nonlocal comparacoes, movimentacoes
 
        if inicio >= fim:
            return
 
        pivo = arr[fim]
        i = inicio - 1
 
        for j in range(inicio, fim):
            comparacoes += 1
 
            if arr[j] <= pivo:
                i += 1
 
                if i != j:
                    arr[i], arr[j] = arr[j], arr[i]
                    movimentacoes += 1
 
        if i + 1 != fim:
            arr[i + 1], arr[fim] = arr[fim], arr[i + 1]
            movimentacoes += 1
 
        posicao_pivo = i + 1
 
        ordenar(inicio, posicao_pivo - 1)
        ordenar(posicao_pivo + 1, fim)
 
    ordenar(0, len(arr) - 1)
 
    return comparacoes, movimentacoes
 
 
random.seed(42)
 
tamanhos = [10, 20, 1000]
resultados = []
 
for tamanho in tamanhos:
 
    dados = [random.randint(1, 10000) for _ in range(tamanho)]
 
    dados_bubble = dados.copy()
    dados_quick = dados.copy()
 
    comp_bubble, trocas_bubble = bubble_sort(dados_bubble)
 
    comp_quick, mov_quick = quick_sort(dados_quick)
 
    assert dados_bubble == dados_quick
    assert dados_bubble == sorted(dados)
 
    resultados.append([
        tamanho,
        comp_bubble,
        trocas_bubble,
        comp_quick,
        mov_quick
    ])
 
 
print("\nRESULTADOS DO EXPERIMENTO")
print("-" * 75)
 
print(
    f"{'Tamanho':<12}"
    f"{'Bubble Comp.':<18}"
    f"{'Bubble Trocas':<18}"
    f"{'Quick Comp.':<18}"
    f"{'Quick Mov.':<18}"
)
 
for resultado in resultados:
    print(
        f"{resultado[0]:<12}"
        f"{resultado[1]:<18}"
        f"{resultado[2]:<18}"
        f"{resultado[3]:<18}"
        f"{resultado[4]:<18}"
    )
 
Resultados obtidos
      Tamanho do array

 Bubble Comparações

 Bubble Trocas

 Quick Comparações

 Quick Movimentações

        10

 44

 19

 29

 7

      20

 189

 84

 58

 28

      1.000

 499.122

 239.681

 10.385

 4.543

      Os dois algoritmos receberam exatamente os mesmos dados em cada teste e produziram o mesmo resultado ordenado.

Análise
a) Qual algoritmo apresentou menos operações para 10 elementos?
O Quick Sort apresentou menos comparações e movimentações. Foram 29 comparações e 7 movimentações, contra 44 comparações e 19 trocas do Bubble Sort.
b) Para 20 elementos, o comportamento foi semelhante?
Sim. O Quick Sort continuou apresentando uma quantidade menor de operações. O Bubble Sort realizou 189 comparações e 84 trocas, enquanto o Quick Sort realizou 58 comparações e 28 movimentações.

c) O que aconteceu com 1.000 elementos?
A diferença ficou muito maior. O Bubble Sort realizou 499.122 comparações e 239.681 trocas, enquanto o Quick Sort realizou 10.385 comparações e 4.543 movimentações.

d) Qual algoritmo apresentou maior crescimento no número de operações?
O Bubble Sort apresentou o maior crescimento, principalmente devido à sua complexidade O(n²).

e) Os resultados são coerentes com as complexidades teóricas?
Sim. Os resultados são coerentes com a teoria. O Bubble Sort possui complexidade média O(n²), enquanto o Quick Sort possui complexidade média O(n log n).

f) Quando escolher o Bubble Sort?
O Bubble Sort deve ser escolhido principalmente para arrays muito pequenos, atividades didáticas ou situações em que a simplicidade do algoritmo seja mais importante que o desempenho.

g) Quando escolher o Quick Sort?
O Quick Sort deve ser escolhido para conjuntos de dados médios ou grandes, principalmente quando é necessário obter melhor desempenho médio na ordenação.



PARTE 3 – INVESTIGAÇÃO DE BUSCA EM MATRIZES
Busca sequencial
A busca sequencial percorre os elementos da matriz um por um, utilizando dois loops: um para percorrer as linhas e outro para percorrer as colunas.

def busca_matriz(matriz, valor):
    comparacoes = 0
 
    for i in range(len(matriz)):
        for j in range(len(matriz[i])):
            comparacoes += 1
 
            if matriz[i][j] == valor:
                return True, i, j, comparacoes
 
    return False, -1, -1, comparacoes
 
 
def criar_matriz(linhas, colunas):
    matriz = []
    valor = 1
 
    for i in range(linhas):
        linha = []
 
        for j in range(colunas):
            linha.append(valor)
            valor += 1
 
        matriz.append(linha)
 
    return matriz
 
 
def testar_matriz(linhas, colunas):
 
    matriz = criar_matriz(linhas, colunas)
 
    primeiro = matriz[0][0]
    ultimo = matriz[linhas - 1][colunas - 1]
    inexistente = -1
 
    resultado_inicio = busca_matriz(matriz, primeiro)
    resultado_final = busca_matriz(matriz, ultimo)
    resultado_inexistente = busca_matriz(matriz, inexistente)
 
    print("\n" + "=" * 60)
    print(f"MATRIZ {linhas} x {colunas}")
    print("=" * 60)
 
    print(
        "Busca no início:",
        resultado_inicio[3],
        "comparação"
    )
 
    print(
        "Busca no final:",
        resultado_final[3],
        "comparações"
    )
 
    print(
        "Valor inexistente:",
        resultado_inexistente[3],
        "comparações"
    )
 
    print(
        "Posição do primeiro elemento:",
        resultado_inicio[1],
        resultado_inicio[2]
    )
 
    print(
        "Posição do último elemento:",
        resultado_final[1],
        resultado_final[2]
    )
 
 
testar_matriz(2, 2)
testar_matriz(10, 10)
testar_matriz(100, 100)
Resultados
      Matriz

 Elementos

 Busca no início

 Busca no final

 Valor inexistente

        2 × 2

 4

 1

 4

 4

      10 × 10

 100

 1

 100

 100

      100 × 100

 10.000

 1

 10.000

 10.000

     Análise
a) Por que a busca no início apresenta menos operações?
Porque a busca sequencial começa pela primeira posição da matriz, [0][0]. Quando o valor procurado está nessa posição, apenas uma comparação é necessária.

b) O que acontece quando o valor não existe?
O algoritmo precisa verificar todas as posições da matriz para ter certeza de que o valor não está presente.

Por isso, a quantidade de comparações corresponde ao número total de elementos.

c) Qual é o pior caso?
O pior caso acontece quando:

O elemento procurado está na última posição; ou
O elemento não existe na matriz.
Nos dois casos, todas as posições precisam ser verificadas.

d) Como as dimensões da matriz afetam as operações?
Quanto maior for a quantidade de linhas e colunas, maior será a quantidade de elementos que precisam ser analisados.

Por exemplo:

2 × 2 = 4 elementos.
10 × 10 = 100 elementos.
100 × 100 = 10.000 elementos.
Assim, o aumento das dimensões aumenta diretamente a quantidade de possíveis comparações.

e) Qual é a complexidade para uma matriz de m linhas e n colunas?
A complexidade da busca sequencial é:

O(m × n)

Isso acontece porque o algoritmo pode precisar percorrer todas as m linhas e as n colunas.



PARTE 4 – HANDS ON 1: INVESTIGAÇÃO DO ARRAY
Código
temperaturas = []
 
print("Digite 10 temperaturas:")
 
for i in range(10):
    temperatura = float(
        input(f"Temperatura {i}: ")
    )
 
    temperaturas.append(temperatura)
 
 
print("\nTEMPERATURAS")
 
for i in range(10):
    print(
        f"Índice {i}: "
        f"{temperaturas[i]:.2f} °C"
    )
 
 
# Calcula a média
soma = 0
 
for temperatura in temperaturas:
    soma += temperatura
 
media = soma / len(temperaturas)
 
 
# Encontra maior e menor temperatura
maior = temperaturas[0]
menor = temperaturas[0]
 
indice_maior = 0
indice_menor = 0
 
 
for i in range(1, len(temperaturas)):
 
    if temperaturas[i] > maior:
        maior = temperaturas[i]
        indice_maior = i
 
    if temperaturas[i] < menor:
        menor = temperaturas[i]
        indice_menor = i
 
 
# Conta temperaturas acima da média
acima_media = 0
 
for temperatura in temperaturas:
 
    if temperatura > media:
        acima_media += 1
 
 
print("\nRESULTADOS")
 
print(
    f"Média: {media:.2f} °C"
)
 
print(
    f"Maior temperatura: "
    f"{maior:.2f} °C "
    f"(Índice {indice_maior})"
)
 
print(
    f"Menor temperatura: "
    f"{menor:.2f} °C "
    f"(Índice {indice_menor})"
)
 
print(
    f"Quantidade acima da média: "
    f"{acima_media}"
)
Análise
O programa realiza três principais percursos pelo array:

Percorre as temperaturas para calcular a média.
Percorre o array para encontrar a maior e a menor temperatura.
Percorre novamente para contar as temperaturas acima da média.
Considerando apenas os principais percursos, temos aproximadamente:

n + n + n = 3n

Para 10 temperaturas:

3 × 10 = aproximadamente 30 iterações de percurso.

Isso não representa todas as operações internas do programa, mas serve para demonstrar o crescimento dos percursos.

A complexidade do algoritmo é O(n).

Portanto:

10 elementos → aproximadamente 30 percursos.
100 elementos → aproximadamente 300 percursos.
1.000 elementos → aproximadamente 3.000 percursos.
O crescimento é linear.



PARTE 5 – HANDS ON 2: MATRIZ APLICADA – MONITORAMENTO DE SENSORES
Código
sensores = []
 
 
# Entrada das temperaturas
for i in range(5):
 
    linha = []
 
    print(f"\nSensor {i}")
 
    for j in range(24):
 
        temperatura = float(
            input(
                f"Temperatura na hora {j}: "
            )
        )
 
        linha.append(temperatura)
 
    sensores.append(linha)
 
 
# Calcula a média de cada sensor
medias = []
 
for i in range(5):
 
    soma = 0
 
    for j in range(24):
 
        soma += sensores[i][j]
 
    media = soma / 24
 
    medias.append(media)
 
 
# Encontra a maior temperatura
maior = sensores[0][0]
 
sensor_maior = 0
hora_maior = 0
 
 
for i in range(5):
 
    for j in range(24):
 
        if sensores[i][j] > maior:
 
            maior = sensores[i][j]
 
            sensor_maior = i
 
            hora_maior = j
 
 
# Calcula a média geral
soma_geral = 0
 
 
for i in range(5):
 
    for j in range(24):
 
        soma_geral += sensores[i][j]
 
 
media_geral = soma_geral / 120
 
 
# Define o limite
limite = float(
    input(
        "\nInforme o limite de temperatura: "
    )
)
 
 
# Conta leituras acima do limite
acima_limite = 0
 
 
for i in range(5):
 
    for j in range(24):
 
        if sensores[i][j] > limite:
 
            acima_limite += 1
 
 
# Exibe os resultados
print("\n" + "=" * 60)
print("RESULTADOS")
print("=" * 60)
 
 
for i in range(5):
 
    print(
        f"Média do sensor {i}: "
        f"{medias[i]:.2f} °C"
    )
 
 
print(
    f"Maior temperatura: "
    f"{maior:.2f} °C "
    f"(Sensor {sensor_maior}, "
    f"Horário {hora_maior}h)"
)
 
 
print(
    f"Média geral: "
    f"{media_geral:.2f} °C"
)
 
 
print(
    f"Leituras acima do limite "
    f"({limite:.2f} °C): "
    f"{acima_limite}"
)
Análise da matriz
A matriz possui:

5 sensores × 24 horas = 120 posições.

Cada posição representa uma temperatura medida por um sensor em determinado horário.

Por que são utilizados loops aninhados?
São utilizados loops aninhados porque a estrutura possui duas dimensões:

O primeiro loop percorre os sensores, representados pelas linhas.
O segundo loop percorre as 24 horas, representadas pelas colunas.
Assim, é possível acessar cada temperatura da matriz.

Qual é a função de [i][j]?
A expressão:

sensores[i][j]
representa uma posição específica da matriz.

i representa a linha, ou seja, o sensor.
j representa a coluna, ou seja, a hora.
Por exemplo:

sensores[2][10]
representa a temperatura do sensor 2 na hora 10.

Quantas posições existem na matriz?
A matriz possui:

5 × 24 = 120 posições.

Portanto, cada percurso completo pela matriz precisa analisar até 120 temperaturas.

Relação entre linhas, colunas e operações
Quanto maior o número de sensores e horários, maior será a quantidade de posições.

Se tivermos:

5 sensores × 24 horas = 120 posições.
10 sensores × 24 horas = 240 posições.
20 sensores × 24 horas = 480 posições.
A quantidade de operações aumenta de acordo com o número de elementos.

Para uma matriz geral com m linhas e n colunas, a complexidade dos percursos é:

O(m × n)

No programa, existem vários percursos completos pela matriz. Cada percurso completo analisa as 120 posições.



PARTE 6 – ANÁLISE E CONCLUSÃO


O tamanho da estrutura de dados afeta a quantidade de operações?
Sim.

Os experimentos demonstraram que, conforme aumenta a quantidade de elementos, aumenta também a quantidade de operações necessárias.

Isso pode ser observado tanto nos arrays quanto nas matrizes e nos algoritmos de ordenação.

Por exemplo, na busca sequencial:

2 × 2 → até 4 comparações.
10 × 10 → até 100 comparações.
100 × 100 → até 10.000 comparações.
Portanto, o tamanho da entrada influencia diretamente o número de operações.



Bubble Sort e Quick Sort crescem da mesma forma?
Não.

O Bubble Sort apresenta complexidade média O(n²), enquanto o Quick Sort apresenta complexidade média O(n log n).

Por isso, conforme o número de elementos aumenta, o Bubble Sort tende a realizar muito mais operações.

Os resultados experimentais demonstraram isso claramente.

Com 1.000 elementos:

Bubble Sort: 499.122 comparações e 239.681 trocas.
Quick Sort: 10.385 comparações e 4.543 movimentações.
A diferença demonstra como a complexidade computacional influencia o desempenho dos algoritmos.



Por que observar somente o resultado final não é suficiente para comparar algoritmos?
Porque dois algoritmos podem produzir exatamente o mesmo resultado, mas utilizar quantidades diferentes de operações, tempo e memória.

No experimento, Bubble Sort e Quick Sort produziram o mesmo array ordenado.

Entretanto, a quantidade de comparações e movimentações foi muito diferente.

Por isso, para comparar algoritmos, é necessário analisar fatores como:

Número de comparações.
Número de trocas ou movimentações.
Tempo de execução.
Uso de memória.
Complexidade computacional.
Dessa forma, é possível determinar qual algoritmo é mais adequado para determinada situação.



CONCLUSÃO GERAL
Os experimentos realizados demonstraram a importância da análise de estruturas de dados e algoritmos.

Foi possível observar que arrays e matrizes aumentam a quantidade de operações conforme aumenta o número de elementos. Na busca sequencial em matrizes, por exemplo, uma matriz de 100 × 100 pode exigir até 10.000 comparações.

Também foi possível comparar o Bubble Sort e o Quick Sort. Embora os dois algoritmos produzam o mesmo resultado final, o número de operações realizadas é bastante diferente. O Bubble Sort possui crescimento médio O(n²), enquanto o Quick Sort apresenta crescimento médio O(n log n), sendo mais eficiente para conjuntos maiores.

Nos exercícios com arrays e matrizes, também foi possível compreender a importância dos índices e dos loops. Em uma matriz, [i][j] permite identificar exatamente a linha e a coluna de cada elemento, enquanto os loops aninhados permitem percorrer todas as posições.

Assim, os experimentos confirmam a relação:

Tamanho da entrada → Número de operações → Complexidade → Eficiência

Portanto, analisar somente se um algoritmo funciona não é suficiente. É necessário também avaliar sua eficiência e entender como seu número de operações cresce conforme aumenta a quantidade de dados.
