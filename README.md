# Desafio_tecnico_Infinity_Vision
Sistema de reconhecimento visual de produtos para autoatendimento em supermercados, com zonas de confiança e revisão humana

## Reconhecimento Visual de Produtos para Autoatendimento em Supermercados
## Visão Geral

Este projeto implementa um sistema de reconhecimento visual de produtos voltado para caixas de autoatendimento em supermercados.
O objetivo é identificar se imagens de produtos correspondem ao mesmo item físico, mesmo diante de variações como rotação, enquadramento ou iluminação.

A solução utiliza embeddings visuais extraídos por redes neurais convolucionais (CNN) e métricas de distância, adotando uma estratégia conservadora, com zonas explícitas de confiança e incerteza.

## Problema Endereçado

Em cenários de autoatendimento, erros de reconhecimento podem gerar:

cobrança incorreta de produtos,

necessidade excessiva de intervenção humana,

impacto negativo na experiência do cliente.

Por isso, o sistema prioriza:

alta confiabilidade nos agrupamentos automáticos,

redução de falsos positivos,

revisão humana para casos ambíguos.

## Abordagem Técnica
## Pré-processamento das Imagens

Conversão das imagens para tons de cinza, conforme exigido no exercício.

Redimensionamento para tamanho fixo.

Normalização dos valores de pixel.

Replicação do canal grayscale para três canais, garantindo compatibilidade com CNNs pré-treinadas em RGB.

## Concatenação das Imagens Transformadas

Conforme solicitado no enunciado, o programa salva uma única imagem contendo a concatenação das versões transformadas das imagens de entrada.

Essa imagem permite:

validar visualmente o efeito do pré-processamento aplicado,

garantir rastreabilidade e transparência do pipeline.

O arquivo concatenado é salvo no diretório de saída definido em configuração.

## Extração de Embeddings

Uso de uma CNN pré-treinada (ex.: ResNet50 / MobileNet).

Não há etapa de treinamento, reduzindo custo computacional e dependência de dados rotulados.

Cada imagem é representada por um vetor numérico (embedding).

## Cálculo de Similaridade

Cálculo da distância entre embeddings para medir similaridade visual entre produtos.

Embeddings são normalizados para tornar a métrica mais estável e interpretável.

## Zonas de Decisão

Os pares de imagens são classificados em três zonas:

MESMO PRODUTO (alta confiança)
Agrupamento automático seguro.

INCERTO (revisão humana)
Casos ambíguos que não devem ser decididos automaticamente.

DIFERENTE
Produtos visualmente distintos.

Essa separação é intencional e reflete limitações naturais do espaço de embeddings.

## Como Utilizar

Coloque as imagens dos produtos no diretório configurado em images_dir.

Execute o notebook de cima para baixo, sem pular células.

O sistema irá:

aplicar o pré-processamento,

gerar e salvar a imagem concatenada das versões transformadas,

extrair embeddings visuais,

calcular distâncias entre os produtos,

classificar os pares por zona de decisão,

exibir visualizações dos resultados.

## Considerações Importantes

O sistema é conservador por design, priorizando evitar falsos positivos.

Nem todos os produtos iguais serão automaticamente agrupados.

A presença de uma zona de incerteza é uma decisão consciente de engenharia.

## Possíveis Extensões

Integração com API (FastAPI) para uso em produção.

Indexação vetorial para grandes volumes de produtos.

Ajuste automático de thresholds com dados reais de operação.

## Tecnologias Utilizadas

Python

OpenCV

TensorFlow / Keras

Scikit-learn

NumPy

Matplotlib
