# Relatório de Execução – Fase 1, Etapa 2

Motor NLU com TF-IDF, Random Forest e trava de segurança por threshold.

## 1. Número de árvores utilizadas no motor NLU

Foram utilizadas **80 árvores** (`n_estimators=80`) no `RandomForestClassifier`, com `random_state=42` para garantir resultados reproduzíveis.

## 2. Valor do threshold no limiar de confiança

O limiar de confiança utilizado foi de **0.60 (60%)**. Quando a maior probabilidade retornada pelo modelo é menor que 0.60, ou quando a intenção prevista é `fora_de_escopo`, o motor devolve a intenção `fallback` e pede que o usuário reformule a mensagem.

## 3. Resultado da primeira execução

Saída do módulo ao executar a bateria de testes:

| Entrada | Intenção retornada | Confiança |
|---|---|---|
| Tenho 30 kg de banana para doar | cadastrar_doacao | 0.93 |
| Nossa instituição precisa de mantimentos | fallback | 0.41 |
| Qual é a receita de bolo de cenoura? | fallback | 0.49 |
| coisa comida doar la | fallback | 0.42 |

Saída bruta do terminal:

```
 [NLU] Modelo Random Forest e Vetorizador TF-IDF treinados com sucesso!

--- BATERIA DE TESTES DE ESTRESSE NLU ---

Entrada: 'Tenho 30 kg de banana para doar'
Intenção: cadastrar_doacao | Confiança: 0.93
Retorno: Intenção 'cadastrar_doacao' identificada com 92.5% de confiança.

Entrada: 'Nossa instituição precisa de mantimentos'
Intenção: fallback | Confiança: 0.41
Retorno: Desculpe, não consegui entender com clareza o seu pedido.
Você pode refazer a mensagem informando se deseja **doar alimentos** ou **solicitar doações para uma ONG**?

Entrada: 'Qual é a receita de bolo de cenoura?'
Intenção: fallback | Confiança: 0.49
Retorno: Desculpe, não consegui entender com clareza o seu pedido.
Você pode refazer a mensagem informando se deseja **doar alimentos** ou **solicitar doações para uma ONG**?

Entrada: 'coisa comida doar la'
Intenção: fallback | Confiança: 0.42
Retorno: Desculpe, não consegui entender com clareza o seu pedido.
Você pode refazer a mensagem informando se deseja **doar alimentos** ou **solicitar doações para uma ONG**?
```

**Análise:** a frase clara de doação foi classificada corretamente, com alta confiança. A frase fora de escopo e a frase confusa foram corretamente barradas pela trava de segurança. Já a frase "Nossa instituição precisa de mantimentos" é uma solicitação legítima de alimentos, mas ficou com 0.41 e caiu no fallback. Isso mostra que o modelo ainda não generaliza bem para vocabulário que não aparece no treino ("instituição", "mantimentos").

## 4. Como melhorar os resultados e aumentar o grau de confiança

O dataset atual tem apenas 21 frases (8 de `cadastrar_doacao`, 5 de `solicitar_alimentos`, 4 de `consultar_status` e 4 de `fora_de_escopo`). Com tão pouco dado, as árvores têm pouca base para votar com segurança, o que mantém a confiança baixa. As principais melhorias são:

- **Ampliar a base de treino:** incluir dezenas de frases por intenção, com sinônimos e formas diferentes de dizer a mesma coisa (por exemplo "mantimentos", "instituição", "entidade", "suprimentos", "cesta básica"). É o ganho mais direto para a frase que caiu no fallback.
- **Balancear as classes:** deixar todas as intenções com quantidade parecida de exemplos, ou usar `class_weight="balanced"`, para o modelo não favorecer `cadastrar_doacao`.
- **Enriquecer o `fora_de_escopo`:** adicionar muitos exemplos variados (receitas, esportes, clima, finanças, conversa casual) para o modelo reconhecer melhor o que está fora do domínio.
- **Pré-processar o texto:** normalizar para minúsculas, remover acentos e pontuação e tratar stopwords e variações como "doar", "doação" e "doando" (stemming ou lematização para o português).
- **Avaliar com dados separados:** dividir em treino e teste e usar validação cruzada, em vez de medir apenas com quatro frases manuais. Assim dá para medir acurácia, precisão e recall por intenção.
- **Ajustar hiperparâmetros:** testar outros valores de `n_estimators`, `max_depth`, `min_samples_leaf` e do `ngram_range` do TF-IDF, escolhendo pela validação cruzada.
- **Calibrar as probabilidades:** usar `CalibratedClassifierCV` para que a confiança reflita melhor a chance real de acerto.
- **Revisar o threshold com dados:** com um conjunto de validação, escolher o limiar que equilibra melhor entre barrar frases ruins e aceitar frases corretas, em vez de fixar 0.60 de forma arbitrária.
- **Aprender com o uso real:** registrar as mensagens que caíram no fallback, rotulá-las e incorporá-las ao treino.

## 5. Por que o Random Forest foi o melhor método de Machine Learning para esta fase

- **Funciona bem com poucos dados:** como o dataset inicial é pequeno, o Random Forest se comporta melhor que modelos que exigem grandes volumes de dados, como redes neurais.
- **Reduz o overfitting:** ele combina 80 árvores treinadas em amostras diferentes e faz a decisão por votação. Isso torna o resultado mais estável do que o de uma única árvore de decisão, que tende a decorar o treino.
- **Lida bem com dados esparsos e de alta dimensão:** a matriz do TF-IDF com bigramas tem muitas colunas, a maioria zerada, e o Random Forest trabalha bem nesse cenário.
- **Entrega probabilidades de forma nativa:** o `predict_proba` fornece a confiança de cada intenção, que é exatamente o que a trava de segurança por threshold precisa para decidir entre responder e acionar o fallback.
- **Treino rápido e leve:** não exige GPU nem escalonamento dos dados, o que combina com um chatbot que precisa responder em tempo real.
- **Interpretável:** é possível consultar a importância de cada termo (`feature_importances_`) para entender por que o modelo tomou uma decisão.
- **Reprodutível:** com `random_state=42`, os resultados são os mesmos a cada execução, o que facilita testes e a documentação.
