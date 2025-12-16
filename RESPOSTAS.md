# Respostas do Trabalho - Pipeline de ML

## Identificação do Grupo

- **Integrantes:**
  1. Nome: Anna Elisa de Lara (annafisica@gmail.com)
  2. Nome: Giselle de Oliveira Dias (simsgod@gmail.com)
  3. Nome: Vitor Zago Capanema (zago.vitor@gmail.com)
  4. Nome: ---

---

## Parte 1: Resultados do Pipeline

### 1.1 O pipeline executou sem erros?

<!-- Marque com X a opção correta -->

- [ X ] Sim
- [ ] Não

### 1.2 F1-Score obtido:
```
F1-Score: 0.4043 
```

### 1.3 Cole aqui o output final do pipeline:

```
(.venv) PS C:\00. MBA\Módulo 1 - Engenharia de Software e Data Engineering para ML\Mod1_Disc2_Pipelines de dados em Python\trabalho_Pipeline-1> python main.py  
>>

🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀
INICIANDO PIPELINE DE ML
🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀


[ETAPA 1/4] Carregando dados...
==================================================
EXPLORAÇÃO DOS DADOS
==================================================
(5000, 8)
cliente_id              int64
idade                   int64
renda_mensal          float64
tempo_conta_meses       int64
num_produtos            int64
tem_cartao_credito      int64
score_credito         float64
respondeu_campanha      int64
dtype: object
   cliente_id  idade  renda_mensal  tempo_conta_meses  num_produtos  tem_cartao_credito  score_credito  respondeu_campanha
0           1     56      46917.46                229             4                   1          600.0                   1
1           2     69      41274.41                  9             3                   0          758.2                   0
2           3     46      40649.98                 25             2                   1          595.7                   1
3           4     32      44336.79                217             5                   1          584.3                   0
4           5     60      35301.68                225             4                   0          797.8                   0
==================================================

DISTRIBUIÇÃO DO TARGET
------------------------------
respondeu_campanha
0    2803
1    2197
Name: count, dtype: int64
respondeu_campanha
0    0.5606
1    0.4394
Name: proportion, dtype: float64
------------------------------

[ETAPA 2/4] Validando dados...
C:\00. MBA\.venv\Lib\site-packages\pandera\_pandas_deprecated.py:146: FutureWarning: Importing pandas-specific classes and functions from the
top-level pandera module will be **removed in a future version of pandera**.
If you're using pandera to validate pandas objects, we highly recommend updating
your import:

```
# old import
import pandera as pa

# new import
import pandera.pandas as pa
```

If you're using pandera to validate objects from other compatible libraries
like pyspark or polars, see the supported libraries section of the documentation
for more information on how to import pandera:

https://pandera.readthedocs.io/en/stable/supported_libraries.html

To disable this warning, set the environment variable:

```
export DISABLE_PANDERA_IMPORT_WARNING=True
```

  warnings.warn(_future_warning, FutureWarning)
Validando dados...
✅ Dados válidos!

[ETAPA 3/4] Treinando modelo...
Dados de treino: 4000 registros
Dados de teste: 1000 registros
Treinando modelo...
✅ Modelo treinado!
Modelo salvo em: models/modelo_campanha.pkl

[ETAPA 4/4] Avaliando modelo...

==================================================
RESULTADOS DA AVALIAÇÃO
==================================================

📊 MÉTRICAS:
   Accuracy:  0.5550 (55.50%)
   Precision: 0.4951
   Recall:    0.3416
   F1-Score:  0.4043

📋 MATRIZ DE CONFUSÃO:
   Verdadeiros Negativos (TN): 404
   Falsos Positivos (FP):      154
   Falsos Negativos (FN):      291
   Verdadeiros Positivos (TP): 151

==================================================
🎯 F1-SCORE FINAL: 0.4043
==================================================

✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅
PIPELINE CONCLUÍDO COM SUCESSO!
✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅

📝 Anote o F1-Score no arquivo RESPOSTAS.md: 0.4043

```
---

## Parte 2: Interpretação dos Resultados

### 2.1 O modelo é bom ou ruim? Por quê?

O modelo não é bom, pois teve um F1 menor de 0.5, ou seja, não é confiável para tomadas de decisões.

### 2.2 O dataset é balanceado ou desbalanceado? Como você descobriu?

O dataset é um pouco desbalanceado, pois existe uma proporção ligeiramente maior de casos não "respodeu_campanha" (0). Isso pode induzir o modelo a fazer essa previsão, favorecendo a classe 0.
Esse desbalanceamento, ainda que moderado, foi percebido no Recall baixo (0.3416), com muitos falsos negativos, e no F1.

### 2.3 Por que usamos F1-Score e não apenas Accuracy neste caso?

Porque o F1-Score, que é a média harmônica entre Precisão e recall, mede o equilíbrio entre identificar corretamente a classe positiva e evitar erros de classificação. Neste caso, ele é mais adequadro que a Accuracy porque o dataset é desbalanceado e o objetivo principal é identificar clientes que responderiam à campanha. O F1-Score evita interpretações enganosas e mostra que o modelo ainda apresenta desempenho insuficiente para o objetivo desejado.

## Parte 3: Validação de Dados

### 3.1 Liste as validações Pandera que você implementou:

Foram utilizadas 8 validações, aqui divididas em 2 grupos:

Grupo 1 - estava pronta no código como exemplo
1. tempo_conta_meses (já veio pronta no código): Column(int, check.in_range(1, 240)) --- Garantir tempo de conta plausível, nos limites do intervalo
2. num_produtos (já veio pronta no código): Column(int, check.in_range(1,5)) --- Garantir quantidade de produtos no intervalo esperado
3. tem_cartao_credito (já veio pronta no código): Column(int, check.isin([0, 1])) --- Garantir valor binário (sim/não)

Grupo 2 - implementadas pela equipe de desenvolvimento:
1. cliente_id: Column(int, nullable=False, unique=True) --- Garantir id obrigatório e único para evitar duplicatas
2. idade: Column(int, check.in_range(18,80)) --- Restringir idade ao intervalo 18-80
3. renda_mensal: Column(float, check.in_range(1000, 50000)) --- Restringir renda ao intervalo definido
4. score_credito (já veio pronta no código): Column(float, check.in_range(300, 850)) --- Restringir o score de credito ao intervalo indicado
5. respondeu_campanha (target): Column(int, check.isin([0, 1])) --- Garantir target binário 0 ou 1, o que é essencial para o classificador


### 3.2 Por que validar dados ANTES de treinar o modelo?

De forma suscinta, para garantir que a matéria-prima utilizada no aprendizado seja de alta qualidade e confiável, permitindo a construção de um modelo que contribua com uma tomada de decisão mais assertiva.

Aprofundando a importância desta etapa no pipeline, a validação e limpeza dos dados antes do treinamento são essenciais pelos seguintes motivos:
1. Compreender o conjunto de dados, apoiando a identificação de padrões, distribuições e possíveis inconsistências (em conjunto com a etapa de exploração).
2. Assegurar a integridade estatística, evitando que valores inválidos distorçam o aprendizado do modelo.
3. Eliminar ou impedir a entrada de erros, como valores nulos, duplicados, fora de faixa, categorias inválidas ou tipos de dados errado.
4. Prevenir divergências significativas entre dados de treinamento e dados de produção, garantindo consistência ao longo do ciclo de vida do modelo.
5. Reduzir o risco de previsões incorretas ou enviesadas, causadas por dados inconsistentes.
6. Definir explicitamente o contrato de dados esperado pelo modelo, deixando claras as estruturas, tipos e valores permitidos.
7. Detectar anomalias de forma proativa, interrompendo o pipeline imediatamente quando dados inválidos são identificados (princípio de fail fast).
8. Economizar custos computacionais e operacionais, evitando treinar modelos com dados inadequados.
9. Mitigar degradação silenciosa do modelo, especialmente em ambientes produtivos.


## Parte 4: Versionamento

### 4.1 Liste os commits que vocês fizeram (copie do git log):

![print do git log](image.png)

commit ae8c1dfa1d787a907c609cd05f98e3aa07bfd88e (HEAD -> main, origin/main, origin/HEAD)
Author: Simsgod <simsgod@gmail.com>
Date:   Tue Dec 16 18:34:09 2025 -0300

    Atualização com dados do git log

commit b6773800612c188845d7649d1ecb84370b2fc8ba
Author: Simsgod <simsgod@gmail.com>
Date:   Mon Dec 15 23:30:20 2025 -0300

    Atualiza respostas e ignora artefatos de modelo treinado

commit d38e994d4bc2bfdbbdefe1a0d1409f8526cf7f62
Author: Simsgod <simsgod@gmail.com>
Date:   Mon Dec 15 12:35:56 2025 -0300

    resposta_1

commit 70e70372ab95358ee098b6daec2d9556b9dc3792
Merge: 511a24d c533a40
Author: Anna Lara <annafisica@gmail.com>
Date:   Mon Dec 15 11:09:45 2025 -0300

Merge pull request #1 from vitor-zago/main

    Etapas 3 e 4 concluídas

commit c533a4072cdcfbe22e5735ac4dab720d09b36527
Author: VITOR-ZAGO <zago.vitor@gmail.com>
Date:   Mon Dec 15 10:38:30 2025 -0300

    Inclusão da pasta Modelos/arquivo treinar.py/ arquivo validar.py/ modificação do arquivo carregar.py

commit 511a24dc64b175bf41ccb79d2b674e839e50387a
Author: Anna Elisa de Lara <annafisica@gmail.com>
Date:   Wed Dec 10 22:58:54 2025 -0300

    Atualização do arquivo "RESPOSTAS.md"
    com informações relacionadas às etapas 1 e 2 após sua conclusão.

commit a788ae3f7b13a1a12c8cd4ff0247317401fc871a
Author: Anna Elisa de Lara <annafisica@gmail.com>
Date:   Wed Dec 10 22:36:05 2025 -0300

    Etapas 1 e 2 concluídas.

commit 9462cd3858eb04141b18d9824f58af063521a45f
Author: Anna Elisa de Lara <annafisica@gmail.com>
Date:   Wed Dec 10 21:36:44 2025 -0300

    Commit Inicial - Criação do Repositório com
    arquivos iniciais disponibilizados pelo professor.
(END)

### 4.2 Por que mensagens de commit descritivas são importantes?

Mensagens de commit descritivas são essenciais para manter um histórico claro do projeto, permitindo entender o que foi alterado, quando, por quem e qual o impacto da alteração. Elas facilitam manutenção, rollback, trabalho em equipe e rastreabilidade das mudanças ao longo do tempo.


## Parte 5: Reflexão (Opcional)

### 5.1 Qual foi a maior dificuldade do grupo?

### 5.2 O que vocês fariam diferente se fossem refazer?

O pipeline funciona, mas não foi otimizado. Caso fôssemos refazê-lo, poderíamos explorar outros modelos e hiperparâmetros, tratar o desbalanceamento da base, aprimorar a validação e avaliação dos dados e estruturá-lo de forma mais próxima de um ambiente produtivo, com melhor monitoramento e reprodutibilidade.

Como o objetivo do negócio é identificar os clientes que respondem à campanha, o erro mais custoso é o falso negativo. Dessa forma, a estratégia de priorizar o Recall em vez de apenas a accuracy, discutida durante a aula, poderia ser aplicada no pipeline por meio do tratamento do desbalanceamento da base, atribuindo maior peso à classe positiva e avaliando o impacto direto no recall.

Essa estratégia poderia ser implementada no pipeline por meio de modelos mais robustos, como o Random Forest, por exemplo, avaliando seu desempenho principalmente por Recall e F1-Store.

Além disso, o pipeline poderia ser aprimorado com melhor separação entre EDA, validação e transformações em etapas independentes,inclusão de testes automatizados e monitoramento de data drift e model drift, aproximando-o de um cenário real de produção.



**Data de entrega:** **16/12/2025**/**\_\_**
