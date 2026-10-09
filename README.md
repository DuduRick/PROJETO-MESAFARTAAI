MESAFARTAI – Logística e Inteligência Assistiva no Combate à Fome


O MESAFARTAI é um chatbot em Python que conecta doadores de alimentos (supermercados, restaurantes, feirantes e produtores) a ONGs, abrigos e cozinhas comunitárias. O doador escreve em linguagem natural, como “tenho 30 kg de tomate que vence amanhã”, e o sistema classifica a intenção da mensagem (Scikit-Learn/Spacy), extrai produto, quantidade e validade com Regex e usa o algoritmo KNN para encaminhar a doação à ONG mais próxima. Os dados ficam em SQLite3 e a interação acontece por uma interface web em Streamlit.
O projeto está alinhado à ODS 2 da ONU (Fome Zero e Agricultura Sustentável), pois ataca o principal gargalo do combate à fome: não falta comida, falta logística ágil e comunicação eficiente. Ao direcionar alimentos próprios para consumo, que seriam descartados, a famílias em situação de vulnerabilidade, o sistema amplia o acesso à alimentação (meta 2.1) e reduz o desperdício.

Eduardo Henrique Faria da Silva - 160361
Kaio Henrique Paes de Barros - 157877
Andre de Oliveira Pinheiro - 146010
