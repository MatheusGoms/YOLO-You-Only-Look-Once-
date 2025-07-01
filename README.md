Passos para Rotular a Base de Dados e Treinar com a Rede YOLO
Preparação da Base de Dados:

Organizar as imagens.
Rotular os objetos nas imagens.
Ferramentas de Rotulagem:

Utilizar ferramentas como LabelImg ou Roboflow para criar os arquivos de anotação.
Configuração do YOLO:

Baixar os arquivos YOLO e configurar o ambiente.
Preparar os arquivos de configuração (classes, estrutura da rede, etc.).
Treinamento:

Dividir os dados em treino e validação.
Executar o treinamento com o YOLO.
Avaliação do Modelo:

Testar o modelo treinado com novos dados.
Passo 1: Preparação da Base de Dados
Organizar as imagens:
Certifique-se de que as imagens estão em um formato suportado (ex.: .jpg, .png).
Organize as imagens em pastas, como train/ e val/ para treino e validação.
Passo 2: Rotulagem da Base de Dados
Ferramentas de Rotulagem:
LabelImg (https://github.com/tzutalin/labelImg):
Ferramenta gratuita e fácil de usar.
Permite rotular objetos em imagens e salvar os rótulos no formato YOLO.
Roboflow (https://roboflow.com/):
Plataforma online que ajuda na rotulagem e exportação dos dados no formato YOLO.
Formato de Anotação YOLO:
Cada imagem terá um arquivo .txt com os seguintes dados:

<Class_ID> <x_center> <y_center> <width> <height>

Onde:

Class_ID é o índice da classe (ex.: "0" para "gato", "1" para "cachorro").
x_center, y_center são as coordenadas do centro do objeto (normalizadas entre 0 e 1).
width, height são a largura e altura do objeto (também normalizadas).
Passo 3: Configuração do YOLO
Baixe os arquivos do YOLO, como o modelo pré-treinado (ex.: YOLOv5).

Instale o YOLO no ambiente:

git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt

repare os arquivos:

Crie o arquivo data.yaml para definir as classes e os caminhos dos dados:

train: ./path/to/train/images
val: ./path/to/val/images
nc: 2  # Número de classes
names: ['gato', 'cachorro']  # Nomes das classes

Passo 4: Treinamento
Execute o treinamento com YOLOv5:

python train.py --img 640 --batch 16 --epochs 50 --data data.yaml --weights yolov5s.pt

Parâmetros:

--img: Tamanho das imagens (ex.: 640x640).
--batch: Tamanho do lote.
--epochs: Número de épocas.
--data: Caminho para o arquivo data.yaml.
--weights: Pesos pré-treinados para inicialização (ex.: yolov5s.pt).
Passo 5: Avaliação do Modelo
Após o treinamento, você pode avaliar o modelo com novos dados:

python detect.py --source ./path/to/test/images --weights runs/train/exp/weights/best.pt --conf 0.5

Parâmetros:

--source: Caminho para as imagens de teste.
--weights: Pesos do modelo treinado.
--conf: Nível de confiança para a detecção.
Resumo
Rotule as imagens usando ferramentas como LabelImg ou Roboflow.
Configure o arquivo data.yaml com os caminhos da base de dados e classes.
Treine a rede YOLO com o script train.py.
Avalie o modelo com o script detect.py.
