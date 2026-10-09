# MESAFARTAI – Escopo do Projeto

## 1. Problema de negócio

Toneladas de alimentos próprios para consumo são descartadas todos os dias por
feirantes, supermercados, restaurantes e produtores, por proximidade da data de
validade, pequenos defeitos estéticos ou excesso de estoque. Ao mesmo tempo,
ONGs, abrigos e cozinhas comunitárias enfrentam escassez de suprimentos para
alimentar famílias em situação de vulnerabilidade.

O gargalo não é a falta de comida, mas a falta de logística ágil e de
comunicação eficiente. Um comerciante não tem tempo de preencher formulários
extensos para doar 30 kg de alimento que vencem em 24 horas.

**Solução:** um chatbot em Python que entende mensagens informais do doador,
extrai os dados da doação e encaminha o alimento para a ONG mais próxima,
alinhado à **ODS 2 da ONU (Fome Zero e Agricultura Sustentável)**.

## 2. Público-alvo

| Perfil | Quem é | O que precisa |
|--------|--------|---------------|
| **Doador** | Supermercados, restaurantes, feirantes e produtores | Doar excedentes rapidamente, sem burocracia, por conversa |
| **ONG** | ONGs, abrigos e cozinhas comunitárias | Receber alimentos próximos, a tempo de serem consumidos |

## 3. Escopo das intenções tratadas

| Intenção | Descrição | Exemplo |
|----------|-----------|---------|
| `cadastrar_doacao` | Doador registra um alimento disponível | "Tenho 30 kg de tomate que vencem amanhã" |
| `solicitar_alimentos` | ONG pede alimentos disponíveis | "Preciso de arroz e feijão para hoje" |
| `consultar_status` | Consulta de andamento de uma doação ou coleta | "Minha doação já foi coletada?" |
| `fora_de_escopo` | Qualquer assunto não tratado pelo sistema | "Qual a previsão do tempo?" |

Frases com confiança abaixo do limiar (ex.: 0,60) recebem uma resposta de
fallback amigável pedindo para o usuário reformular a mensagem.

## 4. Dados coletados no chat

- **Alimento:** tipo/descrição do produto (ex.: tomate, arroz, pão)
- **Quantidade:** em kg, caixas ou unidades
- **Validade:** prazo informado (ex.: hoje, amanhã, 18h)
- **Identificação do usuário:** nome, perfil (Doador ou ONG), CEP, localização
  (latitude/longitude) e telefone
- **Resultado do match:** ONG escolhida, distância em km e data do match

## 5. Identidade visual

**Requisito do logotipo:** unir os conceitos de alimento/acolhimento e
tecnologia/IA assistiva.

**Prompt utilizado no gerador de imagem por IA:**

Crie uma logo conceitual, extremamente minimalista e tecnologicamente sofisticada para uma iniciativa que conecta alimentação, acolhimento humano e inteligência artificial assistiva.

**Conceito visual:** um símbolo geométrico original que integre três ideias em uma única forma: um recipiente alimentar abstrato, um gesto sutil de proteção e uma conexão inteligente. Utilize um arco ou contorno semicircular para sugerir um recipiente ou prato, combinado a um ponto central e uma linha contínua cuidadosamente posicionada, representando a IA como uma tecnologia que reconhece necessidades, oferece suporte e aproxima pessoas do alimento.

O símbolo deve transmitir a ideia de que a tecnologia não substitui o cuidado humano: ela o torna mais acessível, inteligente e inclusivo. A referência à alimentação deve ser indireta e sofisticada, sem desenhos literais de comida. O acolhimento deve estar presente na estrutura protetora e nas curvas da composição, enquanto a inteligência artificial aparece por meio de precisão geométrica, conexões discretas e organização visual.

**Estética:** minimalismo tecnológico, design vetorial, geometria precisa, formas sólidas, espaços negativos intencionais e proporções equilibradas. Utilize azul elétrico ou azul profundo combinado com ciano, preferencialmente em cores sólidas sobre fundo branco. O símbolo deve funcionar perfeitamente em uma única cor.

**Restrições essenciais:** não utilizar folhas, plantas, natureza, cérebros, robôs, rostos, mãos literais, talheres, garfos, colheres, circuitos complexos, redes de pontos, globos terrestres ou ícones prontos. Não combinar vários símbolos independentes. Não usar gradientes, sombras, efeitos 3D ou detalhes decorativos.

O resultado deve ser uma marca única, inteligente e memorável, com aparência de identidade visual criada por um estúdio especializado em tecnologia e inovação social. Poucos elementos, máxima intenção conceitual e reconhecimento imediato mesmo em tamanho reduzido. Apresentar somente o símbolo centralizado em fundo branco, sem mockups, sem textos e sem elementos adicionais.


> Logotipo minimalista e moderno para um projeto chamado "MESAFARTAI", um
> sistema de inteligência artificial que combate a fome conectando doadores de
> alimentos a ONGs. O símbolo une uma mesa posta ou um prato acolhedor com
> elementos de tecnologia, como circuitos, nós de rede ou um balão de chat
> integrado ao desenho. Formas arredondadas e amigáveis, paleta com verde,
> laranja quente e azul-petróleo, fundo branco, estilo flat vector, sem
> detalhes excessivos, texto "MESAFARTAI" legível abaixo do símbolo.

**Arquivo gerado:** `assets/logo_mesafartai.png`
