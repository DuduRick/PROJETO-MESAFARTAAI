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

> Logotipo minimalista e moderno para um projeto chamado "MESAFARTAI", um
> sistema de inteligência artificial que combate a fome conectando doadores de
> alimentos a ONGs. O símbolo une uma mesa posta ou um prato acolhedor com
> elementos de tecnologia, como circuitos, nós de rede ou um balão de chat
> integrado ao desenho. Formas arredondadas e amigáveis, paleta com verde,
> laranja quente e azul-petróleo, fundo branco, estilo flat vector, sem
> detalhes excessivos, texto "MESAFARTAI" legível abaixo do símbolo.

**Arquivo gerado:** `assets/logo_mesafartai.png`
