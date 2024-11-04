{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "gpuType": "T4",
      "authorship_tag": "ABX9TyN8oxvu6ZYeZzeW81eP75vS",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    },
    "accelerator": "GPU"
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/leandrolaune/CRUD-tabela-de-produtos-Python-SQL/blob/master/Classifica%C3%A7%C3%A3o_de_folhas_de_milho_com_CNN.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Instalando deeplake"
      ],
      "metadata": {
        "id": "gCIvf4VXe0Ld"
      }
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "A5YHxlGh-K6g",
        "outputId": "02a13408-a763-45c7-f9da-a90904b34a98"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Collecting deeplake<4\n",
            "  Downloading deeplake-3.9.27.tar.gz (618 kB)\n",
            "\u001b[?25l     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m0.0/618.7 kB\u001b[0m \u001b[31m?\u001b[0m eta \u001b[36m-:--:--\u001b[0m\r\u001b[2K     \u001b[91m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[91m╸\u001b[0m \u001b[32m614.4/618.7 kB\u001b[0m \u001b[31m32.0 MB/s\u001b[0m eta \u001b[36m0:00:01\u001b[0m\r\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m618.7/618.7 kB\u001b[0m \u001b[31m16.4 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25h  Installing build dependencies ... \u001b[?25l\u001b[?25hdone\n",
            "  Getting requirements to build wheel ... \u001b[?25l\u001b[?25hdone\n",
            "  Preparing metadata (pyproject.toml) ... \u001b[?25l\u001b[?25hdone\n",
            "Requirement already satisfied: numpy<2.0 in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (1.26.4)\n",
            "Requirement already satisfied: pillow~=10.4.0 in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (10.4.0)\n",
            "Collecting boto3 (from deeplake<4)\n",
            "  Downloading boto3-1.35.51-py3-none-any.whl.metadata (6.7 kB)\n",
            "Requirement already satisfied: click in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (8.1.7)\n",
            "Collecting pathos (from deeplake<4)\n",
            "  Downloading pathos-0.3.3-py3-none-any.whl.metadata (11 kB)\n",
            "Collecting humbug>=0.3.1 (from deeplake<4)\n",
            "  Downloading humbug-0.3.2-py3-none-any.whl.metadata (6.8 kB)\n",
            "Requirement already satisfied: tqdm in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (4.66.5)\n",
            "Collecting lz4 (from deeplake<4)\n",
            "  Downloading lz4-4.3.3-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.7 kB)\n",
            "Requirement already satisfied: pyjwt in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (2.9.0)\n",
            "Requirement already satisfied: pydantic in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (2.9.2)\n",
            "Collecting libdeeplake==0.0.147 (from deeplake<4)\n",
            "  Downloading libdeeplake-0.0.147-cp310-cp310-manylinux2014_x86_64.whl.metadata (352 bytes)\n",
            "Collecting aioboto3>=10.4.0 (from deeplake<4)\n",
            "  Downloading aioboto3-13.2.0-py3-none-any.whl.metadata (8.8 kB)\n",
            "Requirement already satisfied: nest-asyncio in /usr/local/lib/python3.10/dist-packages (from deeplake<4) (1.6.0)\n",
            "Collecting dill (from libdeeplake==0.0.147->deeplake<4)\n",
            "  Downloading dill-0.3.9-py3-none-any.whl.metadata (10 kB)\n",
            "Collecting aiobotocore==2.15.2 (from aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4)\n",
            "  Downloading aiobotocore-2.15.2-py3-none-any.whl.metadata (23 kB)\n",
            "Collecting aiofiles>=23.2.1 (from aioboto3>=10.4.0->deeplake<4)\n",
            "  Downloading aiofiles-24.1.0-py3-none-any.whl.metadata (10 kB)\n",
            "Collecting botocore<1.35.37,>=1.35.16 (from aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4)\n",
            "  Downloading botocore-1.35.36-py3-none-any.whl.metadata (5.7 kB)\n",
            "Requirement already satisfied: aiohttp<4.0.0,>=3.9.2 in /usr/local/lib/python3.10/dist-packages (from aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (3.10.10)\n",
            "Requirement already satisfied: wrapt<2.0.0,>=1.10.10 in /usr/local/lib/python3.10/dist-packages (from aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (1.16.0)\n",
            "Collecting aioitertools<1.0.0,>=0.5.1 (from aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4)\n",
            "  Downloading aioitertools-0.12.0-py3-none-any.whl.metadata (3.8 kB)\n",
            "Collecting boto3 (from deeplake<4)\n",
            "  Downloading boto3-1.35.36-py3-none-any.whl.metadata (6.7 kB)\n",
            "Collecting jmespath<2.0.0,>=0.7.1 (from boto3->deeplake<4)\n",
            "  Downloading jmespath-1.0.1-py3-none-any.whl.metadata (7.6 kB)\n",
            "Collecting s3transfer<0.11.0,>=0.10.0 (from boto3->deeplake<4)\n",
            "  Downloading s3transfer-0.10.3-py3-none-any.whl.metadata (1.7 kB)\n",
            "Requirement already satisfied: requests in /usr/local/lib/python3.10/dist-packages (from humbug>=0.3.1->deeplake<4) (2.32.3)\n",
            "Collecting ppft>=1.7.6.9 (from pathos->deeplake<4)\n",
            "  Downloading ppft-1.7.6.9-py3-none-any.whl.metadata (12 kB)\n",
            "Collecting pox>=0.3.5 (from pathos->deeplake<4)\n",
            "  Downloading pox-0.3.5-py3-none-any.whl.metadata (8.0 kB)\n",
            "Collecting multiprocess>=0.70.17 (from pathos->deeplake<4)\n",
            "  Downloading multiprocess-0.70.17-py310-none-any.whl.metadata (7.2 kB)\n",
            "Requirement already satisfied: annotated-types>=0.6.0 in /usr/local/lib/python3.10/dist-packages (from pydantic->deeplake<4) (0.7.0)\n",
            "Requirement already satisfied: pydantic-core==2.23.4 in /usr/local/lib/python3.10/dist-packages (from pydantic->deeplake<4) (2.23.4)\n",
            "Requirement already satisfied: typing-extensions>=4.6.1 in /usr/local/lib/python3.10/dist-packages (from pydantic->deeplake<4) (4.12.2)\n",
            "Requirement already satisfied: python-dateutil<3.0.0,>=2.1 in /usr/local/lib/python3.10/dist-packages (from botocore<1.35.37,>=1.35.16->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (2.8.2)\n",
            "Requirement already satisfied: urllib3!=2.2.0,<3,>=1.25.4 in /usr/local/lib/python3.10/dist-packages (from botocore<1.35.37,>=1.35.16->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (2.2.3)\n",
            "Requirement already satisfied: charset-normalizer<4,>=2 in /usr/local/lib/python3.10/dist-packages (from requests->humbug>=0.3.1->deeplake<4) (3.4.0)\n",
            "Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests->humbug>=0.3.1->deeplake<4) (3.10)\n",
            "Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.10/dist-packages (from requests->humbug>=0.3.1->deeplake<4) (2024.8.30)\n",
            "Requirement already satisfied: aiohappyeyeballs>=2.3.0 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (2.4.3)\n",
            "Requirement already satisfied: aiosignal>=1.1.2 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (1.3.1)\n",
            "Requirement already satisfied: attrs>=17.3.0 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (24.2.0)\n",
            "Requirement already satisfied: frozenlist>=1.1.1 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (1.5.0)\n",
            "Requirement already satisfied: multidict<7.0,>=4.5 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (6.1.0)\n",
            "Requirement already satisfied: yarl<2.0,>=1.12.0 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (1.16.0)\n",
            "Requirement already satisfied: async-timeout<5.0,>=4.0 in /usr/local/lib/python3.10/dist-packages (from aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (4.0.3)\n",
            "Requirement already satisfied: six>=1.5 in /usr/local/lib/python3.10/dist-packages (from python-dateutil<3.0.0,>=2.1->botocore<1.35.37,>=1.35.16->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (1.16.0)\n",
            "Requirement already satisfied: propcache>=0.2.0 in /usr/local/lib/python3.10/dist-packages (from yarl<2.0,>=1.12.0->aiohttp<4.0.0,>=3.9.2->aiobotocore==2.15.2->aiobotocore[boto3]==2.15.2->aioboto3>=10.4.0->deeplake<4) (0.2.0)\n",
            "Downloading libdeeplake-0.0.147-cp310-cp310-manylinux2014_x86_64.whl (17.7 MB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m17.7/17.7 MB\u001b[0m \u001b[31m84.7 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading aioboto3-13.2.0-py3-none-any.whl (34 kB)\n",
            "Downloading aiobotocore-2.15.2-py3-none-any.whl (77 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m77.4/77.4 kB\u001b[0m \u001b[31m5.2 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading boto3-1.35.36-py3-none-any.whl (139 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m139.1/139.1 kB\u001b[0m \u001b[31m10.8 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading humbug-0.3.2-py3-none-any.whl (15 kB)\n",
            "Downloading lz4-4.3.3-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.3 MB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m1.3/1.3 MB\u001b[0m \u001b[31m48.6 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading pathos-0.3.3-py3-none-any.whl (82 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m82.1/82.1 kB\u001b[0m \u001b[31m5.5 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading aiofiles-24.1.0-py3-none-any.whl (15 kB)\n",
            "Downloading botocore-1.35.36-py3-none-any.whl (12.6 MB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m12.6/12.6 MB\u001b[0m \u001b[31m101.6 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading dill-0.3.9-py3-none-any.whl (119 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m119.4/119.4 kB\u001b[0m \u001b[31m8.6 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading jmespath-1.0.1-py3-none-any.whl (20 kB)\n",
            "Downloading multiprocess-0.70.17-py310-none-any.whl (134 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m134.8/134.8 kB\u001b[0m \u001b[31m10.9 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading pox-0.3.5-py3-none-any.whl (29 kB)\n",
            "Downloading ppft-1.7.6.9-py3-none-any.whl (56 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m56.8/56.8 kB\u001b[0m \u001b[31m4.0 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading s3transfer-0.10.3-py3-none-any.whl (82 kB)\n",
            "\u001b[2K   \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m82.6/82.6 kB\u001b[0m \u001b[31m6.2 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
            "\u001b[?25hDownloading aioitertools-0.12.0-py3-none-any.whl (24 kB)\n",
            "Building wheels for collected packages: deeplake\n",
            "  Building wheel for deeplake (pyproject.toml) ... \u001b[?25l\u001b[?25hdone\n",
            "  Created wheel for deeplake: filename=deeplake-3.9.27-py3-none-any.whl size=740515 sha256=c8731067322d78d5df99ac1ef25286cf7d310a9d47b640798b225d5530e8f66a\n",
            "  Stored in directory: /root/.cache/pip/wheels/71/e6/93/ec5cbe3896a600183b67ca09014e694dacc494c344727cfdfe\n",
            "Successfully built deeplake\n",
            "Installing collected packages: ppft, pox, lz4, jmespath, dill, aioitertools, aiofiles, multiprocess, libdeeplake, humbug, botocore, s3transfer, pathos, boto3, aiobotocore, aioboto3, deeplake\n",
            "Successfully installed aioboto3-13.2.0 aiobotocore-2.15.2 aiofiles-24.1.0 aioitertools-0.12.0 boto3-1.35.36 botocore-1.35.36 deeplake-3.9.27 dill-0.3.9 humbug-0.3.2 jmespath-1.0.1 libdeeplake-0.0.147 lz4-4.3.3 multiprocess-0.70.17 pathos-0.3.3 pox-0.3.5 ppft-1.7.6.9 s3transfer-0.10.3\n"
          ]
        }
      ],
      "source": [
        "pip install \"deeplake<4\""
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Importando bibliotecas, carregando dataset e preparando dados"
      ],
      "metadata": {
        "id": "_fI-S1i9fAlq"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Importar bibliotecas necessárias\n",
        "import tensorflow as tf\n",
        "from tensorflow.keras import datasets, layers, models\n",
        "import deeplake\n",
        "import numpy as np\n",
        "import matplotlib.pyplot as plt\n",
        "from sklearn.model_selection import train_test_split\n",
        "\n",
        "# Carregar o dataset do Deep Lake\n",
        "ds = deeplake.load('hub://activeloop/plantvillage-without-augmentation')\n",
        "\n",
        "# Nomear as classes\n",
        "class_names = ['Apple___Apple_scab', 'Apple___Black_rot', 'Apple___Cedar_apple_rust', 'Apple___healthy',\n",
        "               'Blueberry___healthy', 'Cherry___Powdery_mildew', 'Cherry___healthy', 'Corn___Cercospora_leaf_spot Gray_leaf_spot',\n",
        "               'Corn___Common_rust', 'Corn___Northern_Leaf_Blight', 'Corn___healthy', 'Grape___Black_rot',\n",
        "               'Grape___Esca_(Black_Measles)', 'Grape___Leaf_blight_(Isariopsis_Leaf_Spot)', 'Grape___healthy',\n",
        "               'Orange___Haunglongbing_(Citrus_greening)', 'Peach___Bacterial_spot', 'Peach___healthy',\n",
        "               'Pepper,_bell___Bacterial_spot', 'Pepper,_bell___healthy', 'Potato___Early_blight', 'Potato___Late_blight',\n",
        "               'Potato___healthy', 'Raspberry___healthy', 'Soybean___healthy', 'Squash___Powdery_mildew',\n",
        "               'Strawberry___Leaf_scorch', 'Strawberry___healthy', 'Tomato___Bacterial_spot', 'Tomato___Early_blight',\n",
        "               'Tomato___Late_blight', 'Tomato___Leaf_Mold', 'Tomato___Septoria_leaf_spot', 'Tomato___Spider_mites Two-spotted_spider_mite',\n",
        "               'Tomato___Target_Spot', 'Tomato___Tomato_Yellow_Leaf_Curl_Virus', 'Tomato___Tomato_mosaic_virus', 'Tomato___healthy']\n",
        "\n",
        "# Definir as classes de interesse\n",
        "selected_classes = ['Corn___healthy', 'Corn___Cercospora_leaf_spot Gray_leaf_spot',\n",
        "                    'Corn___Northern_Leaf_Blight', 'Corn___Common_rust']\n",
        "selected_indices = [class_names.index(cls) for cls in selected_classes]\n",
        "\n",
        "# Filtrar as imagens e os rótulos das classes selecionadas\n",
        "filtered_images = []\n",
        "filtered_labels = []\n",
        "\n",
        "# Contar o número de imagens por classe\n",
        "class_counts = {cls: 0 for cls in selected_indices}\n",
        "\n",
        "for i in range(len(ds['images'])):\n",
        "    label = ds['labels'][i].numpy()[0]\n",
        "    if label in selected_indices and class_counts[label] < 500:  # Ajuste o número conforme necessário\n",
        "        filtered_images.append(ds['images'][i].numpy())\n",
        "        filtered_labels.append(selected_indices.index(label))\n",
        "        class_counts[label] += 1\n",
        "\n",
        "# Converter para arrays do NumPy\n",
        "filtered_images = np.array(filtered_images)\n",
        "filtered_labels = np.array(filtered_labels)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "7gllvJqf-WUv",
        "outputId": "20a932c1-8708-4e47-8fc9-edb399c4e01b"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "/usr/local/lib/python3.10/dist-packages/deeplake/util/check_latest_version.py:32: UserWarning: A newer version of deeplake (4.0.0) is available. It's recommended that you update to the latest version using `pip install -U deeplake`.\n",
            "  warnings.warn(\n"
          ]
        },
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Opening dataset in read-only mode as you don't have write permissions.\n"
          ]
        },
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "|"
          ]
        },
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "This dataset can be visualized in Jupyter Notebook by ds.visualize() or at https://app.activeloop.ai/activeloop/plantvillage-without-augmentation\n",
            "\n"
          ]
        },
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "\\"
          ]
        },
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "hub://activeloop/plantvillage-without-augmentation loaded successfully.\n",
            "\n"
          ]
        },
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "\r \r\r\r/usr/local/lib/python3.10/dist-packages/deeplake/core/tensor.py:719: UserWarning: Indexing by integer in a for loop, like `for i in range(len(ds)): ... ds.tensor[i]` can be quite slow. Use `for i, sample in enumerate(ds)` instead.\n",
            "  warnings.warn(\n"
          ]
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "##  Divisão dos dados em treino, validação e teste"
      ],
      "metadata": {
        "id": "_WLa-spofMoN"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "import numpy as np\n",
        "from sklearn.model_selection import StratifiedShuffleSplit\n",
        "\n",
        "# Supondo que filtered_images e filtered_labels já tenham sido definidos anteriormente\n",
        "# Função para garantir que todas as classes estão presentes nos conjuntos\n",
        "def split_data(images, labels, train_size, val_size, test_size):\n",
        "    strat_split = StratifiedShuffleSplit(n_splits=1, test_size=test_size, random_state=42)\n",
        "\n",
        "    # Divisão inicial: treino e teste\n",
        "    for train_idx, test_idx in strat_split.split(images, labels):\n",
        "        train_images, test_images = images[train_idx], images[test_idx]\n",
        "        train_labels, test_labels = labels[train_idx], labels[test_idx]\n",
        "\n",
        "    # Divisão do treino em treino e validação\n",
        "    strat_split_train_val = StratifiedShuffleSplit(n_splits=1, test_size=val_size/(1-test_size), random_state=42)\n",
        "    for train_idx, val_idx in strat_split_train_val.split(train_images, train_labels):\n",
        "        final_train_images, val_images = train_images[train_idx], train_images[val_idx]\n",
        "        final_train_labels, val_labels = train_labels[train_idx], train_labels[val_idx]\n",
        "\n",
        "    return final_train_images, val_images, test_images, final_train_labels, val_labels, test_labels\n",
        "\n",
        "# Dividir os dados em 80% treino e 20% teste e garantir representação das classes\n",
        "train_images, val_images, test_images, train_labels, val_labels, test_labels = split_data(\n",
        "    filtered_images, filtered_labels, train_size=0.8, val_size=0.2, test_size=0.2)\n",
        "\n",
        "# Verificar a quantidade de amostras por classe para garantir a representação correta\n",
        "unique_train_labels, train_counts = np.unique(train_labels, return_counts=True)\n",
        "unique_val_labels, val_counts = np.unique(val_labels, return_counts=True)\n",
        "unique_test_labels, test_counts = np.unique(test_labels, return_counts=True)\n",
        "\n",
        "print('Amostras por classe no treino:', dict(zip(unique_train_labels, train_counts)))\n",
        "print('Amostras por classe na validação:', dict(zip(unique_val_labels, val_counts)))\n",
        "print('Amostras por classe no teste:', dict(zip(unique_test_labels, test_counts)))"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "B7S4-FOQ_12J",
        "outputId": "2ff93359-29e8-42a1-cf66-17eeb72689b1"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Amostras por classe no treino: {0: 300, 1: 267, 2: 300, 3: 300}\n",
            "Amostras por classe na validação: {0: 100, 1: 89, 2: 100, 3: 100}\n",
            "Amostras por classe no teste: {0: 100, 1: 90, 2: 100, 3: 100}\n"
          ]
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Definindo a arquitetura da CNN e compilando o modelo"
      ],
      "metadata": {
        "id": "aaywvTz6ln8u"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Definir a arquitetura da CNN\n",
        "model = models.Sequential([\n",
        "    layers.Conv2D(32, (3, 3), activation='relu', input_shape=(256, 256, 3)),  # Ajuste o tamanho da imagem conforme necessário\n",
        "    layers.MaxPooling2D((2, 2)),\n",
        "    layers.Conv2D(64, (3, 3), activation='relu'),\n",
        "    layers.MaxPooling2D((2, 2)),\n",
        "    layers.Conv2D(128, (3, 3), activation='relu'),\n",
        "    layers.MaxPooling2D((2, 2)),\n",
        "    layers.Flatten(),\n",
        "    layers.Dense(128, activation='relu'),\n",
        "    layers.Dense(4, activation='softmax')  # 4 classes no total\n",
        "])\n",
        "\n",
        "# Compilar o modelo\n",
        "model.compile(optimizer='adam',\n",
        "              loss='sparse_categorical_crossentropy',\n",
        "              metrics=['accuracy'])\n",
        "\n",
        "model.summary()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 472
        },
        "id": "5o72XbkXBjTK",
        "outputId": "9fee0997-13e3-4b48-d28d-bbf9f4cec0e7"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "/usr/local/lib/python3.10/dist-packages/keras/src/layers/convolutional/base_conv.py:107: UserWarning: Do not pass an `input_shape`/`input_dim` argument to a layer. When using Sequential models, prefer using an `Input(shape)` object as the first layer in the model instead.\n",
            "  super().__init__(activity_regularizer=activity_regularizer, **kwargs)\n"
          ]
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "\u001b[1mModel: \"sequential\"\u001b[0m\n"
            ],
            "text/html": [
              "<pre style=\"white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace\"><span style=\"font-weight: bold\">Model: \"sequential\"</span>\n",
              "</pre>\n"
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓\n",
              "┃\u001b[1m \u001b[0m\u001b[1mLayer (type)                        \u001b[0m\u001b[1m \u001b[0m┃\u001b[1m \u001b[0m\u001b[1mOutput Shape               \u001b[0m\u001b[1m \u001b[0m┃\u001b[1m \u001b[0m\u001b[1m        Param #\u001b[0m\u001b[1m \u001b[0m┃\n",
              "┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩\n",
              "│ conv2d (\u001b[38;5;33mConv2D\u001b[0m)                      │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m254\u001b[0m, \u001b[38;5;34m254\u001b[0m, \u001b[38;5;34m32\u001b[0m)        │             \u001b[38;5;34m896\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ max_pooling2d (\u001b[38;5;33mMaxPooling2D\u001b[0m)         │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m127\u001b[0m, \u001b[38;5;34m127\u001b[0m, \u001b[38;5;34m32\u001b[0m)        │               \u001b[38;5;34m0\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ conv2d_1 (\u001b[38;5;33mConv2D\u001b[0m)                    │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m125\u001b[0m, \u001b[38;5;34m125\u001b[0m, \u001b[38;5;34m64\u001b[0m)        │          \u001b[38;5;34m18,496\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ max_pooling2d_1 (\u001b[38;5;33mMaxPooling2D\u001b[0m)       │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m62\u001b[0m, \u001b[38;5;34m62\u001b[0m, \u001b[38;5;34m64\u001b[0m)          │               \u001b[38;5;34m0\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ conv2d_2 (\u001b[38;5;33mConv2D\u001b[0m)                    │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m60\u001b[0m, \u001b[38;5;34m60\u001b[0m, \u001b[38;5;34m128\u001b[0m)         │          \u001b[38;5;34m73,856\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ max_pooling2d_2 (\u001b[38;5;33mMaxPooling2D\u001b[0m)       │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m30\u001b[0m, \u001b[38;5;34m30\u001b[0m, \u001b[38;5;34m128\u001b[0m)         │               \u001b[38;5;34m0\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ flatten (\u001b[38;5;33mFlatten\u001b[0m)                    │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m115200\u001b[0m)              │               \u001b[38;5;34m0\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ dense (\u001b[38;5;33mDense\u001b[0m)                        │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m128\u001b[0m)                 │      \u001b[38;5;34m14,745,728\u001b[0m │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ dense_1 (\u001b[38;5;33mDense\u001b[0m)                      │ (\u001b[38;5;45mNone\u001b[0m, \u001b[38;5;34m4\u001b[0m)                   │             \u001b[38;5;34m516\u001b[0m │\n",
              "└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘\n"
            ],
            "text/html": [
              "<pre style=\"white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace\">┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┓\n",
              "┃<span style=\"font-weight: bold\"> Layer (type)                         </span>┃<span style=\"font-weight: bold\"> Output Shape                </span>┃<span style=\"font-weight: bold\">         Param # </span>┃\n",
              "┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━┩\n",
              "│ conv2d (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">Conv2D</span>)                      │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">254</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">254</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">32</span>)        │             <span style=\"color: #00af00; text-decoration-color: #00af00\">896</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ max_pooling2d (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">MaxPooling2D</span>)         │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">127</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">127</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">32</span>)        │               <span style=\"color: #00af00; text-decoration-color: #00af00\">0</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ conv2d_1 (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">Conv2D</span>)                    │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">125</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">125</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">64</span>)        │          <span style=\"color: #00af00; text-decoration-color: #00af00\">18,496</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ max_pooling2d_1 (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">MaxPooling2D</span>)       │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">62</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">62</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">64</span>)          │               <span style=\"color: #00af00; text-decoration-color: #00af00\">0</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ conv2d_2 (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">Conv2D</span>)                    │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">60</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">60</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">128</span>)         │          <span style=\"color: #00af00; text-decoration-color: #00af00\">73,856</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ max_pooling2d_2 (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">MaxPooling2D</span>)       │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">30</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">30</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">128</span>)         │               <span style=\"color: #00af00; text-decoration-color: #00af00\">0</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ flatten (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">Flatten</span>)                    │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">115200</span>)              │               <span style=\"color: #00af00; text-decoration-color: #00af00\">0</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ dense (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">Dense</span>)                        │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">128</span>)                 │      <span style=\"color: #00af00; text-decoration-color: #00af00\">14,745,728</span> │\n",
              "├──────────────────────────────────────┼─────────────────────────────┼─────────────────┤\n",
              "│ dense_1 (<span style=\"color: #0087ff; text-decoration-color: #0087ff\">Dense</span>)                      │ (<span style=\"color: #00d7ff; text-decoration-color: #00d7ff\">None</span>, <span style=\"color: #00af00; text-decoration-color: #00af00\">4</span>)                   │             <span style=\"color: #00af00; text-decoration-color: #00af00\">516</span> │\n",
              "└──────────────────────────────────────┴─────────────────────────────┴─────────────────┘\n",
              "</pre>\n"
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "\u001b[1m Total params: \u001b[0m\u001b[38;5;34m14,839,492\u001b[0m (56.61 MB)\n"
            ],
            "text/html": [
              "<pre style=\"white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace\"><span style=\"font-weight: bold\"> Total params: </span><span style=\"color: #00af00; text-decoration-color: #00af00\">14,839,492</span> (56.61 MB)\n",
              "</pre>\n"
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "\u001b[1m Trainable params: \u001b[0m\u001b[38;5;34m14,839,492\u001b[0m (56.61 MB)\n"
            ],
            "text/html": [
              "<pre style=\"white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace\"><span style=\"font-weight: bold\"> Trainable params: </span><span style=\"color: #00af00; text-decoration-color: #00af00\">14,839,492</span> (56.61 MB)\n",
              "</pre>\n"
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "\u001b[1m Non-trainable params: \u001b[0m\u001b[38;5;34m0\u001b[0m (0.00 B)\n"
            ],
            "text/html": [
              "<pre style=\"white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace\"><span style=\"font-weight: bold\"> Non-trainable params: </span><span style=\"color: #00af00; text-decoration-color: #00af00\">0</span> (0.00 B)\n",
              "</pre>\n"
            ]
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Treinando a CNN com callbacks"
      ],
      "metadata": {
        "id": "G3lXsSpqmLPz"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "from tensorflow.keras.callbacks import ModelCheckpoint\n",
        "\n",
        "# Callback para salvar o melhor modelo durante o treinamento\n",
        "checkpoint = ModelCheckpoint('best_model.keras', monitor='val_accuracy', save_best_only=True)\n",
        "\n",
        "# Treinamento por 20 épocas completas\n",
        "history = model.fit(train_images, train_labels,\n",
        "                    epochs=20,  # Treinar por 20 épocas\n",
        "                    validation_data=(val_images, val_labels),\n",
        "                    callbacks=[checkpoint])\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "v0Jjlqw9Bn8v",
        "outputId": "fcd02b7a-e612-40ff-d665-f06167d4525f"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Epoch 1/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m27s\u001b[0m 476ms/step - accuracy: 0.5089 - loss: 312.7827 - val_accuracy: 0.9512 - val_loss: 0.1695\n",
            "Epoch 2/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m4s\u001b[0m 108ms/step - accuracy: 0.9655 - loss: 0.1100 - val_accuracy: 0.9666 - val_loss: 0.0796\n",
            "Epoch 3/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m4s\u001b[0m 90ms/step - accuracy: 0.9874 - loss: 0.0349 - val_accuracy: 0.9769 - val_loss: 0.0569\n",
            "Epoch 4/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m5s\u001b[0m 92ms/step - accuracy: 0.9962 - loss: 0.0212 - val_accuracy: 0.9871 - val_loss: 0.0735\n",
            "Epoch 5/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m5s\u001b[0m 90ms/step - accuracy: 0.9959 - loss: 0.0109 - val_accuracy: 0.9923 - val_loss: 0.0298\n",
            "Epoch 6/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m4s\u001b[0m 63ms/step - accuracy: 0.9962 - loss: 0.0139 - val_accuracy: 0.9794 - val_loss: 0.0608\n",
            "Epoch 7/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 58ms/step - accuracy: 0.9920 - loss: 0.0212 - val_accuracy: 0.9383 - val_loss: 0.2112\n",
            "Epoch 8/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 59ms/step - accuracy: 0.9844 - loss: 0.0579 - val_accuracy: 0.9769 - val_loss: 0.0642\n",
            "Epoch 9/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 60ms/step - accuracy: 0.9899 - loss: 0.0396 - val_accuracy: 0.9820 - val_loss: 0.0587\n",
            "Epoch 10/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 58ms/step - accuracy: 0.9837 - loss: 0.0404 - val_accuracy: 0.9589 - val_loss: 0.2378\n",
            "Epoch 11/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m3s\u001b[0m 58ms/step - accuracy: 0.9984 - loss: 0.0042 - val_accuracy: 0.9897 - val_loss: 0.0338\n",
            "Epoch 12/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m3s\u001b[0m 62ms/step - accuracy: 1.0000 - loss: 0.0019 - val_accuracy: 0.9846 - val_loss: 0.0582\n",
            "Epoch 13/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m4s\u001b[0m 99ms/step - accuracy: 1.0000 - loss: 5.9068e-04 - val_accuracy: 0.9949 - val_loss: 0.0167\n",
            "Epoch 14/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m4s\u001b[0m 59ms/step - accuracy: 0.9990 - loss: 0.0033 - val_accuracy: 0.9794 - val_loss: 0.0848\n",
            "Epoch 15/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 58ms/step - accuracy: 0.9850 - loss: 0.0492 - val_accuracy: 0.8972 - val_loss: 0.5402\n",
            "Epoch 16/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 58ms/step - accuracy: 0.9223 - loss: 0.2820 - val_accuracy: 0.9614 - val_loss: 0.1866\n",
            "Epoch 17/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 58ms/step - accuracy: 0.9571 - loss: 0.1800 - val_accuracy: 0.9383 - val_loss: 0.2853\n",
            "Epoch 18/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 61ms/step - accuracy: 0.9446 - loss: 0.2289 - val_accuracy: 0.9717 - val_loss: 0.3718\n",
            "Epoch 19/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 59ms/step - accuracy: 0.9839 - loss: 0.0529 - val_accuracy: 0.9794 - val_loss: 0.1022\n",
            "Epoch 20/20\n",
            "\u001b[1m37/37\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m2s\u001b[0m 58ms/step - accuracy: 0.9937 - loss: 0.0199 - val_accuracy: 0.9846 - val_loss: 0.1006\n"
          ]
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Avaliando no conjunto de teste e gerando matriz confusão"
      ],
      "metadata": {
        "id": "zgKtw2pSmUtv"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay\n",
        "import matplotlib.pyplot as plt\n",
        "import numpy as np\n",
        "\n",
        "# Fazer previsões no conjunto de teste\n",
        "y_pred = model.predict(test_images)\n",
        "y_pred_classes = np.argmax(y_pred, axis=1)\n",
        "\n",
        "# Gerar a matriz de confusão\n",
        "conf_matrix = confusion_matrix(test_labels, y_pred_classes)\n",
        "\n",
        "# Nomes das classes traduzidos\n",
        "translated_class_names = ['Milho saudável', 'Mancha foliar de Cercospora (mancha cinzenta da folha)',\n",
        "                          'Murcha da folha do norte', 'Ferrugem comum']\n",
        "\n",
        "# Verificar as classes presentes no conjunto de teste\n",
        "unique_test_labels = np.unique(test_labels)\n",
        "print(f'Classes presentes no conjunto de teste: {unique_test_labels}')\n",
        "\n",
        "# Criar a máscara para destacar apenas a diagonal\n",
        "mask = np.zeros_like(conf_matrix)\n",
        "np.fill_diagonal(mask, 1)\n",
        "\n",
        "# Configurar a exibição da matriz de confusão\n",
        "fig, ax = plt.subplots(figsize=(8, 8))\n",
        "disp = ConfusionMatrixDisplay(confusion_matrix=conf_matrix,\n",
        "                              display_labels=[translated_class_names[i] for i in unique_test_labels])\n",
        "\n",
        "# Plotar a matriz de confusão sem colorir\n",
        "disp.plot(cmap=plt.cm.Blues, ax=ax, values_format='.0f')\n",
        "\n",
        "# Rotacionar os labels do eixo x para 45 graus\n",
        "plt.xticks(rotation=45)\n",
        "\n",
        "# Aplicar a máscara para esconder os valores fora da diagonal\n",
        "for i in range(conf_matrix.shape[0]):\n",
        "    for j in range(conf_matrix.shape[1]):\n",
        "        if i != j:\n",
        "            ax.text(j, i, \"\", va='center', ha='center')\n",
        "\n",
        "plt.show()\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 951
        },
        "id": "aYePy8pYSTx-",
        "outputId": "0d202a65-33d4-4349-993b-e9d50807f84b"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "\u001b[1m13/13\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m1s\u001b[0m 93ms/step\n",
            "Classes presentes no conjunto de teste: [0 1 2 3]\n"
          ]
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 800x800 with 2 Axes>"
            ],
            "image/png": "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p8GDByt9+vTy8vJSpUqVdPTo0USNweGVBsHBwVq0aJHu3LljXhcZGamFCxcqc+bMDowscf35558qVqyYcuTIoTRp0jzVPgICAmyuUnic6OjoZ3p8Qg0YMEANGzZUiRIl9P333+uPP/7QxIkTtXfvXs2fP/+p92vv55FY7t69+9SP/frrr+Xv768yZcokYkQvlpQpU8rPz8/RYTidP//8U2XLllWWLFkUFBTk0FhatmypadOmOTSG59nd6Hvac+iMyr+cy7zOZDKp3Mu5tGPfCQdGhmeVzM2kZG4mRd69Z7E+8u49vZI3g7Kk9Ve6lD5av/eM+b7w23e168hFlciV3t7hIglwfLsW3u/ngPFvM0R7LUrg9IRr166pTJkycnd31/fff68DBw5o4sSJSpEihXmbcePGadq0afr444+1bds2+fj4qEqVKoqMjEy0l8rhSYOiRYsqODhYy5YtM69btmyZMmfOrCJFilhs+8MPP6hs2bIKDAxUUFCQatSooT///NN8//2S6GXLlum1116Tt7e3ChUqpC1bLLN1YWFhKl++vLy9vZUiRQpVqVJF165dM98fGxurPn36KGXKlEqXLp2GDh1q8fhJkyapQIEC8vHxUXBwsDp27KiIiIjHPseQkBAtXbpU8+bNs6ieOH36tGrXri1fX1/5+/urQYMGunjx4mP383A5sK2vx+LFi1WuXDl5eno+9gze0aNH9eqrr8rT01N58+bVTz/99Mg2Z86cUYMGDRQYGKiUKVOqdu3aOnny5GPj3b59u0aPHq2JEydq/PjxKl26tEJCQvT6669r6dKlatGihXnbb7/9VkWLFpWnp6eyZcumYcOG6d69f/9wMgxDM2fOVK1ateTj46NRo0ZJklauXKkSJUrI09NTqVKlUt26dc2PuXbtmpo3b64UKVLI29tbb7zxhkXW7dSpU6pZs6ZSpEghHx8f5cuXT999950kaf369TIMQ6tXr1bBggXl6empV155RX/88YfFc1y6dKny5csnDw8PhYSEaOLEiRb3h4SEaMSIEWrevLn8/f3Vrl07SVLfvn2VM2dOeXt7K1u2bBo0aNB/JkIWLVqkmjVrWqy7/5kYPXq00qZNq8DAQA0fPlz37t1T7969lTJlSmXKlElz5861eNx/jX//7Pj8+fMVEhKigIAANWrUSDdv/lsuFxsbq3Hjxumll16Sh4eHMmfObH5f7jt+/Phjj8UrV66ocePGypgxo7y9vVWgQAF9+eWXT3wNpCcfvw+XyIeEhGj06NFq3bq1/Pz8lDlzZs2aNcvieVr7gX6/oic2NlZjxoxR1qxZ5eXlpUKFCunrr782P/7+52Tt2rUqXry4vL29Vbp0aR0+fFiSFBoaqmHDhmnv3r2P7DuhP0ck247ThH62DMPQrl27NHz4cBmGYf55t2/fPlWoUEFeXl4KCgpSu3bt/jO+xPjZWbNmTe3cudPiZxn+deV6hGJiYpU6pWVyLHVKf126Eu6gqJAYIu5Ea/vB8+rd8GWlS+kjk8lQg/K5VCJXOqVN4aO0KbwlSZev37Z43KXrt5Xmn/vg3Di+XQvvN2wxduxYBQcHa+7cuXr55ZeVNWtWVa5cWdmzZ5cUX2UwZcoUDRw4ULVr11bBggU1b948nTt3LlGnmTs8aSBJrVu3tvhS89lnn6lVq1aPbHfr1i316NFDO3fu1Nq1a2UymVS3bt1H5r8OGDBAvXr10p49e5QzZ041btzY/AV0z549qlixovLmzastW7bo119/Vc2aNRUTE2N+/Oeffy4fHx9t27ZN48aN0/Dhwy3+ODeZTJo2bZr279+vzz//XL/88ov69Onz2Oe3Y8cOVa1aVQ0aNND58+c1depUxcbGqnbt2rp69ao2bNign376ScePH1fDhg1tft1sfT369eunbt266eDBg6pSpcoj+4mNjVW9evWUPHlybdu2TR9//LH69u1rsU10dLSqVKkiPz8/bdq0SWFhYfL19VXVqlUfe/Z8wYIF8vX1VceOHa3ef79qYtOmTWrevLm6deumAwcO6JNPPlFoaOgjX0CHDh2qunXrat++fWrdurVWr16tunXrqlq1atq9e7fWrl2rl19+2bx9y5YttXPnTq1YsUJbtmxRXFycqlWrZv4C1alTJ0VFRWnjxo3at2+fxo4dK19fX4sxe/furYkTJ2rHjh1KnTq1atasaX78rl271KBBAzVq1Ej79u3T0KFDNWjQoEemkEyYMEGFChXS7t27NWjQIEmSn5+fQkNDdeDAAU2dOlWzZ8/W5MmTrb5O9/36668qXrz4I+t/+eUXnTt3Ths3btSkSZM0ZMgQ1ahRQylSpNC2bdvUoUMHtW/fXn/99Zf5MbaM/+eff+qbb77RqlWrtGrVKm3YsEEffPCB+f7+/fvrgw8+0KBBg3TgwAEtXLhQadOmtdjHk47FyMhIFStWTKtXr9Yff/yhdu3a6e2339b27dsf+xrYcvw+bOLEiSpevLh2796tjh076t133zV/qe/Vq5fOnz9vXiZMmCBvb2/z6zxmzBjNmzdPH3/8sfbv36/33ntPzZo104YNGx55nhMnTtTOnTuVLFkytW7dWpLUsGFD9ezZU/ny5TOPcf8YT+jPEVuOUynhn63z588rX7586tmzp86fP69evXrp1q1bqlKlilKkSKEdO3boq6++0s8//6zOnTs/dj9S4vzszJw5s9KmTatNmzZZHSMqKkrh4eEWC/CiaD95jQzD0MHQNrq4tJPa1SikpZuOKDYuztGhAcALxzAcs0h65G+ZqKgoqzGuWLFCxYsX11tvvaU0adKoSJEimj17tvn+EydO6MKFC6pUqZJ5XUBAgEqWLPnIifNn8VxcPaFZs2bq37+/Tp06JSn+TOKiRYu0fv16i+3q169vcfuzzz5T6tSpdeDAAeXPn9+8vlevXqpevbokadiwYcqXL5+OHTum3Llza9y4cSpevLhmzJhh3j5fvnwW+y1YsKB53niOHDk0ffp0rV27Vq+//rokPXImc+TIkerQoYPFPh+UOnVqeXh4yMvLS+nSpZMk/fTTT9q3b59OnDih4OBgSdK8efOUL18+7dixQyVKlPjP183W16N79+6qV6/eY/fz888/69ChQ/rxxx+VIUMGSdLo0aP1xhtvmLdZvHixYmNj9emnn5qvLzp37lwFBgZq/fr1VpvzHT16VNmyZZO7u/sTn8ewYcPUr18/c+VBtmzZNGLECPXp08di/n6TJk0skkmNGjVSo0aNNGzYMPO6QoUKmcdesWKFwsLCVLp0aUnxSYzg4GB98803euutt3T69GnVr19fBQoUMI/7sCFDhpjf988//1yZMmXS8uXL1aBBA02aNEkVK1Y0JwJy5sypAwcOaPz48Ra9OCpUqKCePXta7HfgwIHm/4eEhKhXr15atGjRY780Xr9+XTdu3DC/Pw9KmTKlpk2bJpPJpFy5cmncuHG6ffu23n//fUn/frn/9ddf1ahRI5vHj42NVWhoqLnc/+2339batWs1atQo3bx5U1OnTtX06dPN71v27NlVtmxZi9iedCxmzJhRvXr1Mm/bpUsX/fjjj1qyZIlF8udBthy/D6tWrZo5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tnjMxIkTzV9yO3bsqHfffVeHDx823+/n56fQ0FAdOHBAU6dO1ezZszV58uTHxhAREaEaNWoob9682rVrl4YOHapevXpZbBMbG6tMmTLpq6++0oEDBzR48GC9//77WrJkidV9BgcH6/z58/L399eUKVN0/vx5NWzYUGfPnlW1atVUokQJ7d27VzNnztScOXM0cuTIJ75OjnjOTxvr7du3NWHCBM2fP18bN27U6dOnLfY9depUTZw4URMmTNDvv/+uKlWqqFatWjp69KjFfvr166du3brp4MGDeu211zRlyhT5+/vr/PnzOn/+vHmfnTt31pYtW7Ro0SL9/vvveuutt1S1atVH9ndfVFTUI79oXcmV6xGKiYlV6pR+FutTp/TXpSuu9Vq4At5v15A2yF+SdPmKZUn6pSs3leaf+9IG+evyNcv7Y2JidS38tvnxcC4c364tODhYAQEB5mXMmDGP3bZTp06qXr26KlWqZLF+165dio6OtlifO3duZc6cWVu2JG61CpdcBFxIs2bN1L9/f506dUpSfKO/RYsWPfWZ3SZNmlgkHRo1aqRGjRpp2LBh5nWFChWyeEy1atXUsWNHSfFn2CdPnqx169YpV674TPvAgQPN24aEhKhXr15atGiR+vTpYzWGhQsXKjY2VnPmzJGnp6fy5cunv/76S++++655G3d3d4uYsmbNqi1btmjJkiVq0KDBI/t0c3NTunTpZBiGAgIClC5dOknSjBkzFBwcrOnTp8swDOXOnVvnzp1T3759NXjwYJlM1vOwjnjOTxtrdHS0Pv74Y2XPnl1S/Jf64cOHm++fMGGC+vbtq0aNGkmSxo4dq3Xr1mnKlCn66KOPzNt1797dojwuICBAhmGYX0tJOn36tObOnavTp08rQ4YMkqRevXrphx9+0Ny5czV69OhH4hszZozFewkAAPA0zM0J7TymJJ05c0b+/v8m/Dw8PKxuv2jRIv3222/asWPHI/dduHBByZMnf2QKbdq0aXXhwoVEi1kiaQC4lNSpU6t69eoKDQ1VXFycqlevrlSpUj31/ooXL25xe8+ePXrnnXee+JgH52Ld/xJ56dIl87rFixdr2rRp+vPPPxUREaF79+5Z/FB92MGDB1WwYEF5enqa15UqVeqR7T766CN99tlnOn36tO7cuaO7d++qcOHC//UUHxmrVKlSMh74DVOmTBlF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RET+pvDwcADrU08R+XdOnDjBRx99ZP143rx5HDp0CIPBwOTJk63bBw8ezPLly2nRogXdu3fn9OnTfP/998yfPz/e8oUJ7ezZs1SrVo0CBQqwaNEismXLBsDt27fJmjUrHTp04NmzZwQFBeHs7Ezjxo3ZtWsX7733Hps3byZNmjS6CU1gfn5+zJ8/H29vb5ydnRk4cCDVq1dn9erVAAwcOJBx48YxcuRIunTpQqpUqWxcsUjioZEGIiIif5Obm5sCA5H/p44dOxIcHAz8Oc983bp1TJkyhaNHjxIREWE99j//+Q9NmjRhyZIlDB8+nFKlSrFo0SKbBgZms5lChQqxc+dOrly5QosWLawjIbJmzcqLFy84ceIEBQsWxNnZGZPJRKZMmRg4cCChoaGkTZtWgUECiPtc9LfffmP16tWsWLGCgQMHkj9/fuzt7alZs6b1mOHDh9OuXTtCQ0OtK1+IyEsKDUREREQkwbRt25YRI0YAcPXqVQBWrFhBt27duHDhAgsWLODx48fW44cNG0a1atW4du1avMaBtggM4s5rN5vNjBo1ih07dtC9e3du3rwJvGxuWLhwYXbu3MmSJUvo168fmzdvpl69emTJkiXBa06Jfvjhh3i9Z27duoWdnR2fffYZoaGhtGrVinHjxvHtt9/y5MkTli9fDrycdrJz587XGlaKpHQKDUREREQkwXz22Wc4ODgwd+5cOnXqxPbt2wGYNGkSNWvW5LvvvmPJkiU8efLEes53333H4sWLbX4zZzAYMBgMhISEULp0afbs2UOFChXYtm0bLVu25NatWzg4ONCsWTPSpk2Lr68vGzZsICQkhJw5c9qs7pRk1qxZdO/enQ8//NC6LVeuXHh4ePDDDz/QunVrxo0bR+fOnQE4evQooaGhnD592nq8mh6KxKeeBiIiIiLyzsVtSAewatUqRowYQcGCBencuTOVKlUCwMvLi71799KnTx8aN25M+vTpreckhpu569evU7ZsWXr06IGvry+RkZEcP36cxo0bkzdvXpYtW0aWLFm4f/8+ERERpE6dGldXV5vWnFLMmDEDb29vli1bRv369a3b7927R+XKlTlx4gQjRoygX79+ADx//pyGDRuSPn16ayglIq/TSAMREREReafiBgY//fQTd+7coX79+owYMYI//viDqVOnsmPHDgDmzp1LhQoV6N27Nzt3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FoB58+YxcOBAGjVqhJ+fH9mzZ+fOnTuEhYVRokQJjEYjMTEx2Nsnvhmrt27dYsSIERw4cIC6devSv39/4OW0Clv0XBARSakS308IEREREfmfLBaLNTCYP38+f/zxB4cOHeLLL7+0HuPp6QnAwIEDMRqNdO7cmUKFCpElSxbgZeiQGAMDgGzZsjFgwABGjBjBhg0biIyMZNiwYQoMREQSWOL8KSEiIiIifynuKgkDBw5kwoQJlC5dml9++YWHDx9StmxZSpYsCbwMDoxGI+3atSNv3rwUKlTIep3ENCXhTWKDg379+rF3717u3btH5syZbV2WiEiKoukJIiIiIklI3OH5hw4dYurUqXTo0IFy5cqxfPlyRo8eTdGiRenWrRvFixe3nrdx40aqV6+eJJ/Uh4eHA382cxQRkYSTuONlEREREQEgODgYwHrTv3z5cjp37szp06cpXLgwAI0bN8bX15fjx48zefJkjh49aj3/yy+/TDSrJPxTbm5uCgxERGxEoYGIiIhIInf48GHmzZtHdHQ0sYNEDQYDqVOn5tSpU5w6dcp6bPPmzfH19eX3339nyJAhnD9/Pt61kuJIAxERsR2FBiIiIiKJXObMmTl16hSbN2+29jJo1KgRgwcPplixYgwbNoy9e/daj2/WrBmdO3fG1dWV9957z1Zli4hIMqCeBiIiIiKJWGzTw2HDhnHw4EGmT59Ozpw5rfvXrVvHDz/8gMFgYPDgwZQrV+61a7y6NKOIiMjfpZ8eIiIiIolY7MiCcuXKER4ezvbt2+P1Jahduzbe3t4AjBgxgp07d752DQUGIiLyb+kniIiIiEgSUL16dcqWLYuPjw/79u2Lt6927dp069aN8PBw1qxZY6MKRUQkOdL0BBEREZFELu70gvr16/Prr7+yaNEiypYtS+rUqa3H7dmzh3LlymlkgYiIvDUKDURERESSgNjgwGw207RpU3bv3k337t35+uuv+eCDD954rIiIyP+XQgMRERGRJGjkyJHs27ePkydP4u3tTalSpahUqZKtyxIRkWRGoYGIiIhIIvBXowNiV0+IZTKZsLOzA+D69evs2rWLFStWUKRIERo1asTHH3+cYDWLiEjyp9BARERExMbiBganTp0CwNHRkQIFCry2H14PEp4/f469vT0ODg4JWLWIiKQECg1EREREbChuADB48GBCQ0MJDw+n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efP+0fstUKAAV65cYcmSJVy8eJHJkye/saljqlSpaNu2LceOHWPXrl10796dJk2akC1bNgCGDRvGqFGjmDx5MufOnePEiRPMnTuXCRMm/KN6REQSM4UGIiIiIilc6tSp+eWXX8idOzcNGjTg/fffp3379rx48cI68qB37960bt2atm3bUq5cOVxcXKhfv/5/ve60adNo1KgRXbp0oXDhwnTs2JGnT58C4O7uzrBhw/D398fNzQ1vb28AAgICGDRoEKNGjeL999+nZs2arF+/nrx58wIv+wysXLmS0NBQihYtyvTp0xk5cuQ/er9ff/01Pj4+eHt7U6xYMfbu3cugQYNeOy5//vw0aNCAr776iurVq/Pxxx/HW1KxQ4cOzJ49m7lz5/LRRx9RqVIl5s2bZ61VRCQ5MFj+qnuNiIiIiIiIiKRoGmkgIiIiIiIiIm+k0EBERERERERE3kihgYiIiIiIiIi8kUIDEREREREREXkjhQYiIiIiIiIi8kYKDURERERERETkjRQaiIiIiIiIiMgbKTQQERERERERkTdSaCAiIiIiIiIib6TQQERERERERETeSKGBiIiIiIiIiLzR/wE41q6VOdxSCwAAAABJRU5ErkJggg==\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "Plotando o desempenho do treinamento"
      ],
      "metadata": {
        "id": "pLl4_yRomfZc"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Plotar o desempenho\n",
        "plt.plot(history.history['accuracy'], label='Acurácia no treinamento')\n",
        "plt.plot(history.history['val_accuracy'], label='Acurácia na validação')\n",
        "plt.xlabel('Épocas')\n",
        "plt.ylabel('Acurácia')\n",
        "plt.legend(loc='lower right')\n",
        "plt.show()"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 451
        },
        "id": "hz1ooKNxaJDj",
        "outputId": "4de086db-3f4d-4ae2-fa8f-f2530f84160c"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<Figure size 640x480 with 1 Axes>"
            ],
            "image/png": "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QggryMrKYu3atcyfP5/jx48bbidOnMDPz8+QkNysWTNCQ0PzPE7lypWJjIw0PL548SIpKSmPPP+BAwfo2bMnHTp0oGzZsmRlZfH3338bXg8ICMDd3T3fc99v3759dOjQgZdffpmWLVtSr149Ll++XKB989OwYUNDbs3952rUqFGe+7i4uKDVah95bB8fH/z8/Lhy5Qr16tUzuumThYti3759jBo1igEDBtC0aVN8fX25evVqkY+n99hjj3H27NmH2lqvXj1DLs+j6Le7/+fj6emJn59foX/OpmD7f6aUQNIDJISwpt9++43Y2FjGjBnz0HDLwIEDWblyJRMmTGD27Nn06NGDunXrMmTIELKysti6dSvTpk0DoHv37ixevJj27duj1WqZNm3aQz0AuQkMDGT9+vXs3buXChUqMG/ePGJiYgyvu7m5MW3aNN566y1cXFzo2LEjd+7c4cyZM4wZM+ah4wUEBLB27Vq2b99O7dq1+frrr/n777+LFUgAvPnmmwwaNIiWLVsSHBzMr7/+yqZNmx6aVXW/WrVqsX37dsLCwqhYsWK+w1n//ve/ee211/Dy8qJnz56kp6fzzz//EBsby5QpU4rU5oCAADZt2kTfvn3RaDTMnDnTJD0w06ZNo127dkyaNImxY8dSpkwZzp49y44dO1i8eHGBjlGlShXc3d3Ztm0b1atXx83NDS8vL958801mz55N3bp1adGiBatXr+b48eNGw23mID1AFqYoiiEHyNvj0b8ohBDC1FauXElwcHCuX84DBw7kn3/+4eTJk3Tt2pWNGzfyyy+/0KJFC7p3787hw4cN286fPx9/f386d+7M888/z9SpUw0rdednxowZBAUF0atXL7p160aNGjUeKh44c+ZM3njjDWbNmkXDhg0ZPHhwnrkkL730Es888wyDBw8mKCiIe/fu8fLLLxfuh5KL/v3789lnn/HJJ5/QuHFjli9fzurVqw05UrkZN24cgYGBtG7dmsqVKz/Us3G/sWPH8t///pfVq1fTtGlTunTpwpo1a4oVuC1YsIDy5cvToUMH+vbtS0hICI899liRj6fXrFkz/vzzTy5cuEDnzp1p2bIls2bNMhpCfRQnJyc+//xzli9fjp+fH/369QPgtddeY8qUKbzxxhs0bdqUbdu28csvv5h3BhigUR4cwBUkJCTg5eVFfHw8np6eJj12UnoWTWarU2QLO2VVCGFb0tLSCA8Pp3bt2ri5uVm7OUKUCvl97grz/S09QBamrwHk6uRQqBkbQgghhDAdCYAs7P78H1kIVQghhLAOCYAsTGaACSGEENYnAZCFyQwwIYQQwvokALKwGJkBJoQQQlidBEAWZlgIVXqAhBBCCKuRAMjC9ENgkgMkhBBCWI8EQBYmOUBCCCGE9UkAZGGGWWASAAkhBADLly9n9+7d1m6GKGUkALIw/TIY5SUJWggh+Prrr1mxYgVt2rQp8D5Xr15Fo9Fw/Phx8zXMikaNGmW0NEjXrl2ZPHlyvvvUqlWLhQsXmrQdgwYNokaNGuzbt48XXnjBaMHakkDWYbCwGMkBEkLYkAMHDtCpUyd69uzJli1bLHruCxcuMG/ePHbs2EGZMmUKvJ+/vz+RkZFUqlTJjK2zHZs2bSrQIrOmlJCQwNWrV/n666+ZPHky3t7eJllTzJZIAGRBiqIQJzlAQggbsnLlSl599VVWrlzJrVu3CrW4ZVFkZmYavszr16/PqVOnCn0MR0dHfH19Td00m1WhQgWLn9PT09Ow8G1J6/nRkyEwC0pKzyJTq649Kz1AQpRQigIZyda5FXJt66SkJDZs2MDEiRPp06cPa9aseWibX3/9lTZt2uDm5kalSpUYMGCA4TWNRsPmzZuNtvf29jYcRz9UtWHDBrp06YKbmxvffvst9+7dY+jQoVSrVg0PDw+aNm3KunXrjI6j0+mYN28e9erVw9XVlRo1avDBBx8YHVc/BKbVahkzZgy1a9fG3d2dwMBAPvvss3yvfffu3Wg0GkJDQ2ndujUeHh506NCBsLAwwzaXL1+mX79++Pj4ULZsWdq0acPOnTvzPOaFCxfQaDScP3/e6PlPP/2UunXrFrmtDw6B3b59m759++Lu7k7t2rX59ttvH9pnwYIFNG3alDJlyuDv78/LL79MUlKS0Tb79u2ja9eueHh4UL58eUJCQoiNjQVg27ZtdOrUCW9vbypWrMhTTz3F5cuXjfY/deoU3bt3x93dnYoVKzJ+/PiHzmHLpAfIgvT5P+7Ojri7yEKoQpRImSnwoXl7UfL0zi1wKfhQ0vfff0+DBg0IDAzkhRdeYPLkyUyfPt2wTuGWLVsYMGAA7777LmvXriUjI4OtW7cWullvv/028+fPp2XLlri5uZGWlkarVq2YNm0anp6ebNu2jREjRlC3bl3atm0LwPTp01mxYgWffvopnTp1IjIy8qHAQk+n01G9enU2btxIxYoV2b9/P+PHj6dq1aoMGjQo37a9++67zJ8/n8qVKzNhwgRefPFF9u3bB6gBYu/evfnggw9wdXVl7dq19O3bl7CwMGrUqPHQserXr0/r1q359ttvef/99w3Pf/vttzz//PPFbqveqFGjuHXrFrt27cLZ2ZnXXnuN27dvG23j4ODA559/Tu3atbly5Qovv/wyb731Fl988QUAx48fp0ePHrz44ot89tlnODk5sWvXLrRaLQDJyclMmTKFZs2akZSUxKxZsxgwYADHjx/HwcGB5ORkQkJCaN++PX///Te3b99m7NixTJo0KddA2iYp4iHx8fEKoMTHx5v0uMciYpWa035T2n+406THFUJYR2pqqnL27FklNTU158n0JEWZ7WmdW3pSodrfoUMHZeHChYqiKEpmZqZSqVIlZdeuXYbX27dvrwwbNizP/QHlp59+MnrOy8tLWb16taIoihIeHq4AhnPk56mnnlLeeOMNRVEUJSEhQXF1dVVWrFiR67b64x47dizP473yyivKwIED83x9165dCqDs3Jnz+3jLli0KYPx+PqBx48bKokWL8nz9008/VerWrWt4HBYWpgDKuXPnCtzWkSNHKv369TM87tKli/L6668bHe/w4cOG18+dO6cAyqeffprnOTZu3KhUrFjR8Hjo0KFKx44d89z+QXfu3FEA5dSpU4qiKMqXX36plC9fXklKyvk/t2XLFsXBwUGJiooq8HGLItfPXbbCfH9LD5AFxcoUeCFKPmcPtSfGWucuoLCwMA4fPsxPP/0EgJOTE4MHD2blypV07doVUHsJxo0bV+xmtW7d2uhxZmYms2bNYsOGDdy8eZOMDPV3o7u7OwDnzp0jPT2dHj16FPgcS5YsYdWqVURERJCamkpGRgYtWrR45H7NmjUz3K9atSqgDjHVqFGDpKQk5syZw5YtW4iMjCQrK4vU1FQiIiLyPN6QIUOYOnUqBw8epF27dnz77bc89thjNGjQoNhtBfVn4+TkRKtWrQzPNWjQAG9vb6Ptdu7cydy5czl//jwJCQlkZWWRlpZGSkoKHh4eHD9+nOeeey7P81y8eJFZs2Zx6NAh7t69i06nAyAiIoImTZpw7tw5mjdvbpS83rFjR3Q6HWFhYfj4+BToeqxJAiALkiKIQpQCGk2hhqGsZeXKlWRlZRklPSuKgqurK4sXL8bLy8sQkORFo9GgPJB3lJmZ+dB2D87wmjdvHt988w0bNmygWbNmlC1blsGDB5Oeng7wyPM+aP369UydOpX58+fTvn17ypUrx8cff8yhQ4ceue/9s6v0Q3/6L/upU6eyY8cOPvnkE+rVq4e7uzvPPvusIWDLja+vL927d+e7776jXbt2fPfdd0ycONEkbS2oq1ev8tRTTzFx4kQ++OADKlSowN69exkzZgwZGRl4eHg88mfct29fatasyYoVK/Dz80On09GkSZN8r93eSBK0BRmKIEoCtBDCirKysli7di3z58/n+PHjhtuJEyfw8/MzJCQ3a9aM0NDQPI9TuXJlIiMjDY8vXrxISkrKI89/4MABevbsSYcOHShbtixZWVlGM40CAgJwd3fP99z327dvHx06dODll1+mZcuW1KtX76GE3aLYt28fo0aNYsCAATRt2hRfX1+uXr36yP2GDRvGhg0bOHDgAFeuXGHIkCEma2uDBg3IysriyJEjhufCwsKIi4szPD5y5Ag6nY758+fTrl076tevz61bxr2S+b239+7dIywsjBkzZtCjRw8aNmxoSI7Wa9iwISdOnCA5Odno2hwcHAgMDCzw9ViTBEAWlKlVcHVykB4gIYRV/fbbb8TGxjJmzBiaNGlidBs4cCArV64EYPbs2axbt47Zs2dz7tw5Tp06xUcffWQ4Tvfu3Vm8eDHHjh3jn3/+YcKECQWqVxMYGMjWrVvZu3cvZ8+eZezYscTExBhed3NzY9q0abz11lusXbuWy5cvc/DgQUO7HhQQEMA///zD9u3buXDhAjNnzjTJ1O2AgAA2bdpkCA6ff/55Q+9Qfp555hkSExOZOHEi3bp1M+plK25bAwMD6dmzJy+99BKHDh3iyJEjjB071qhHp169emRmZrJo0SKuXLnC119/zbJly4yOM336dP7++29efvllTp48yfnz51m6dCl3796lfPnyVKxYkS+//JJLly7xxx9/MGXKFKP9hw0bhpubGyNHjuT06dPs2rWLV199leHDh9vF8BdIAGRRE7vWJew/vZj5VCNrN0UIUYqtXLmS4OBgvLy8Hnpt4MCB/PPPP5w8eZKuXbuyceNGfvnlF1q0aEH37t0NtWEA5s+fj7+/P507d+b5559n6tSp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\n"
          },
          "metadata": {}
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Avaliando a precisão no conjunto de validação"
      ],
      "metadata": {
        "id": "0mFLibUMmpuy"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Avaliar a precisão no conjunto de validação\n",
        "val_loss, val_acc = model.evaluate(val_images, val_labels, verbose=2)\n",
        "print(f'Acurácia no conjunto de validação: {val_acc * 100:.2f}%')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "0I-g2cCzaPUO",
        "outputId": "624daa37-bb47-4663-b6bc-e15243bf7221"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "13/13 - 0s - 25ms/step - accuracy: 0.9846 - loss: 0.1006\n",
            "Acurácia no conjunto de validação: 98.46%\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "from sklearn.metrics import classification_report\n",
        "\n",
        "# Fazer previsões no conjunto de teste\n",
        "y_pred = model.predict(test_images)\n",
        "y_pred_classes = np.argmax(y_pred, axis=1)\n",
        "\n",
        "# Gerar o relatório de classificação\n",
        "report = classification_report(test_labels, y_pred_classes, target_names=selected_classes)\n",
        "\n",
        "# Exibir o relatório\n",
        "print(\"Relatório de classificação por classe:\")\n",
        "print(report)\n"
      ],
      "metadata": {
        "id": "kISI88kLa1rc",
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "outputId": "0419baba-6b06-48cd-e72b-3b3fa67096d2"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "\u001b[1m13/13\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m0s\u001b[0m 16ms/step\n",
            "Relatório de classificação por classe:\n",
            "                                            precision    recall  f1-score   support\n",
            "\n",
            "                            Corn___healthy       0.99      0.98      0.98       100\n",
            "Corn___Cercospora_leaf_spot Gray_leaf_spot       0.99      1.00      0.99        90\n",
            "               Corn___Northern_Leaf_Blight       0.97      1.00      0.99       100\n",
            "                        Corn___Common_rust       1.00      0.97      0.98       100\n",
            "\n",
            "                                  accuracy                           0.99       390\n",
            "                                 macro avg       0.99      0.99      0.99       390\n",
            "                              weighted avg       0.99      0.99      0.99       390\n",
            "\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "import os\n",
        "import zipfile\n",
        "import shutil\n",
        "\n",
        "def save_images(images, labels, subset_name):\n",
        "    # Criar uma pasta para o subconjunto\n",
        "    base_path = f'/content/{subset_name}'\n",
        "    if os.path.exists(base_path):\n",
        "        shutil.rmtree(base_path)\n",
        "    os.makedirs(base_path, exist_ok=True)\n",
        "\n",
        "    # Criar pastas para cada classe dentro do subconjunto\n",
        "    for label in np.unique(labels):\n",
        "        class_path = os.path.join(base_path, translated_class_names[label])\n",
        "        os.makedirs(class_path, exist_ok=True)\n",
        "\n",
        "    # Salvar cada imagem na pasta da classe correspondente\n",
        "    for i, (image, label) in enumerate(zip(images, labels)):\n",
        "        class_path = os.path.join(base_path, translated_class_names[label])\n",
        "        file_path = os.path.join(class_path, f'{subset_name}_image_{i}.png')\n",
        "        plt.imsave(file_path, image.astype('uint8'))\n",
        "\n",
        "    # Compactar a pasta do subconjunto\n",
        "    zip_path = f'/content/{subset_name}.zip'\n",
        "    with zipfile.ZipFile(zip_path, 'w') as zipf:\n",
        "        for root, _, files in os.walk(base_path):\n",
        "            for file in files:\n",
        "                zipf.write(os.path.join(root, file),\n",
        "                           os.path.relpath(os.path.join(root, file), base_path))\n",
        "\n",
        "    # Remover a pasta temporária após a compactação\n",
        "    shutil.rmtree(base_path)\n",
        "    return zip_path\n",
        "\n",
        "# Salvar e compactar os conjuntos de treino, validação e teste\n",
        "train_zip = save_images(train_images, train_labels, 'train')\n",
        "val_zip = save_images(val_images, val_labels, 'val')\n",
        "test_zip = save_images(test_images, test_labels, 'test')\n",
        "\n",
        "# Fazer o download dos arquivos compactados\n",
        "from google.colab import files\n",
        "files.download(train_zip)\n",
        "files.download(val_zip)\n",
        "files.download(test_zip)\n",
        "\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 69
        },
        "id": "tH07aGBjZw4R",
        "outputId": "2fe85028-a7ad-4e15-d09c-453ca244f8cd"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.Javascript object>"
            ],
            "application/javascript": [
              "\n",
              "    async function download(id, filename, size) {\n",
              "      if (!google.colab.kernel.accessAllowed) {\n",
              "        return;\n",
              "      }\n",
              "      const div = document.createElement('div');\n",
              "      const label = document.createElement('label');\n",
              "      label.textContent = `Downloading \"${filename}\": `;\n",
              "      div.appendChild(label);\n",
              "      const progress = document.createElement('progress');\n",
              "      progress.max = size;\n",
              "      div.appendChild(progress);\n",
              "      document.body.appendChild(div);\n",
              "\n",
              "      const buffers = [];\n",
              "      let downloaded = 0;\n",
              "\n",
              "      const channel = await google.colab.kernel.comms.open(id);\n",
              "      // Send a message to notify the kernel that we're ready.\n",
              "      channel.send({})\n",
              "\n",
              "      for await (const message of channel.messages) {\n",
              "        // Send a message to notify the kernel that we're ready.\n",
              "        channel.send({})\n",
              "        if (message.buffers) {\n",
              "          for (const buffer of message.buffers) {\n",
              "            buffers.push(buffer);\n",
              "            downloaded += buffer.byteLength;\n",
              "            progress.value = downloaded;\n",
              "          }\n",
              "        }\n",
              "      }\n",
              "      const blob = new Blob(buffers, {type: 'application/binary'});\n",
              "      const a = document.createElement('a');\n",
              "      a.href = window.URL.createObjectURL(blob);\n",
              "      a.download = filename;\n",
              "      div.appendChild(a);\n",
              "      a.click();\n",
              "      div.remove();\n",
              "    }\n",
              "  "
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.Javascript object>"
            ],
            "application/javascript": [
              "download(\"download_611731d3-5a4e-436f-8e95-64a338efafc2\", \"train.zip\", 153566170)"
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.Javascript object>"
            ],
            "application/javascript": [
              "\n",
              "    async function download(id, filename, size) {\n",
              "      if (!google.colab.kernel.accessAllowed) {\n",
              "        return;\n",
              "      }\n",
              "      const div = document.createElement('div');\n",
              "      const label = document.createElement('label');\n",
              "      label.textContent = `Downloading \"${filename}\": `;\n",
              "      div.appendChild(label);\n",
              "      const progress = document.createElement('progress');\n",
              "      progress.max = size;\n",
              "      div.appendChild(progress);\n",
              "      document.body.appendChild(div);\n",
              "\n",
              "      const buffers = [];\n",
              "      let downloaded = 0;\n",
              "\n",
              "      const channel = await google.colab.kernel.comms.open(id);\n",
              "      // Send a message to notify the kernel that we're ready.\n",
              "      channel.send({})\n",
              "\n",
              "      for await (const message of channel.messages) {\n",
              "        // Send a message to notify the kernel that we're ready.\n",
              "        channel.send({})\n",
              "        if (message.buffers) {\n",
              "          for (const buffer of message.buffers) {\n",
              "            buffers.push(buffer);\n",
              "            downloaded += buffer.byteLength;\n",
              "            progress.value = downloaded;\n",
              "          }\n",
              "        }\n",
              "      }\n",
              "      const blob = new Blob(buffers, {type: 'application/binary'});\n",
              "      const a = document.createElement('a');\n",
              "      a.href = window.URL.createObjectURL(blob);\n",
              "      a.download = filename;\n",
              "      div.appendChild(a);\n",
              "      a.click();\n",
              "      div.remove();\n",
              "    }\n",
              "  "
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.Javascript object>"
            ],
            "application/javascript": [
              "download(\"download_bbc32a20-db11-41df-b166-6e15a04a820d\", \"val.zip\", 51242040)"
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.Javascript object>"
            ],
            "application/javascript": [
              "\n",
              "    async function download(id, filename, size) {\n",
              "      if (!google.colab.kernel.accessAllowed) {\n",
              "        return;\n",
              "      }\n",
              "      const div = document.createElement('div');\n",
              "      const label = document.createElement('label');\n",
              "      label.textContent = `Downloading \"${filename}\": `;\n",
              "      div.appendChild(label);\n",
              "      const progress = document.createElement('progress');\n",
              "      progress.max = size;\n",
              "      div.appendChild(progress);\n",
              "      document.body.appendChild(div);\n",
              "\n",
              "      const buffers = [];\n",
              "      let downloaded = 0;\n",
              "\n",
              "      const channel = await google.colab.kernel.comms.open(id);\n",
              "      // Send a message to notify the kernel that we're ready.\n",
              "      channel.send({})\n",
              "\n",
              "      for await (const message of channel.messages) {\n",
              "        // Send a message to notify the kernel that we're ready.\n",
              "        channel.send({})\n",
              "        if (message.buffers) {\n",
              "          for (const buffer of message.buffers) {\n",
              "            buffers.push(buffer);\n",
              "            downloaded += buffer.byteLength;\n",
              "            progress.value = downloaded;\n",
              "          }\n",
              "        }\n",
              "      }\n",
              "      const blob = new Blob(buffers, {type: 'application/binary'});\n",
              "      const a = document.createElement('a');\n",
              "      a.href = window.URL.createObjectURL(blob);\n",
              "      a.download = filename;\n",
              "      div.appendChild(a);\n",
              "      a.click();\n",
              "      div.remove();\n",
              "    }\n",
              "  "
            ]
          },
          "metadata": {}
        },
        {
          "output_type": "display_data",
          "data": {
            "text/plain": [
              "<IPython.core.display.Javascript object>"
            ],
            "application/javascript": [
              "download(\"download_93825755-e2da-400c-b483-79445f231bcf\", \"test.zip\", 51426298)"
            ]
          },
          "metadata": {}
        }
      ]
    }
  ]
}
