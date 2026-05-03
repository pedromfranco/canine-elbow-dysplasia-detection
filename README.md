# Canine Elbow Dysplasia Detection - Auto-Cropping Stage

Este projeto implementa a primeira fase de um sistema de diagnóstico de displasia do cotovelo canino, baseado na metodologia do estudo de **Hauback et al. (2025)**.

## Objetivo
Desenvolver uma ferramenta de **Auto-Cropping** utilizando a arquitetura **RetinaNet** para localizar e recortar automaticamente o côndilo umeral em radiografias digitais. Este processo garante que a fase de diagnóstico receba imagens padronizadas e focadas na área de interesse clínico.

## Tecnologias Utilizadas
- **Python 3.13.0**
- **PyTorch & Torchvision**
- **RetinaNet (ResNet50 FPN)**
- **Torchvision v2 Transforms**

## Metodologia
- **Detecção**: Localização da região epicondilar através de uma rede RetinaNet pré-treinada em ImageNet e ajustada para o conjunto de dados específico.
- **Expansão**: Aplicação de um fator de expansão de 5x sobre a bounding box detectada. Este multiplicador assegura a inclusão de toda a anatomia articular necessária ao diagnóstico, abrangendo a incisura troclear da ulna e a cabeça do rádio.
- **Padronização**: Redimensionamento dos recortes para 800x800 pixels. A aplicação de padding lateral ou vertical garante a preservação da proporção anatómica original, evitando distorções ósseas artificiais.

## Resultados Atuais
- Treino realizado em GPU (NVIDIA GTX 1650 Ti).
- Implementação de Checkpointing baseado em IoU (Intersection over Union) no conjunto de validação para garantir a seleção do modelo com melhor capacidade de generalização.
- Exportação automática de imagens processadas para a fase subsequente de classificação.

## Estrutura do Repositório
- **scripts/**: Contém o código de treino da RetinaNet e o script de processamento em massa (auto-cropping).
- **models/**: Local destinado ao armazenamento dos pesos do modelo (.pth).
- **README.md**: Documentação principal do projeto.
- **.gitignore**: Configuração para exclusão de conjuntos de dados pesados e ficheiros de ambiente local.

## Instalação e Requisitos
1. Instalação das dependências principais:
   ```bash
   pip install torch torchvision matplotlib pillow

2. Hardware: Recomenda-se o uso de uma GPU compatível com CUDA para a execução do ciclo de treino e inferência em massa.

## Referências
Hauback, et al. (2025). Deep learning can detect elbow disease in dogs screened for elbow dysplasia.