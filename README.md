# 🗺️ Extrator de Logradouros de Mapa PDF

Ferramenta para extrair nomes de logradouros (ruas, avenidas, praças, etc.) de mapas municipais em PDF e gerar um GeoPackage georreferenciado, combinando a extração direta do PDF com a malha viária do OpenStreetMap.

## ✨ O que faz

- Extrai texto de PDFs vetoriais (gerados por AutoCAD, QGIS, ArcGIS ou similares) com posição e orientação de cada rótulo.
- Filtra automaticamente os logradouros pelos prefixos comuns (RUA, AVENIDA, TRAVESSA, ALAMEDA, PRAÇA, etc.).
- Baixa a malha viária do município no OpenStreetMap.
- Faz **match exato** por nome normalizado e **match fuzzy** (similaridade ≥ 80%) para tolerar variações ortográficas.
- **Valida espacialmente** os matches fuzzy com modelo afim (RANSAC), classificando cada resultado por confiança.
- Gera um **GeoPackage com 4 camadas auditáveis** (exato, fuzzy aceito, rejeitados, ausentes do OSM).
- Exporta também um CSV consolidado e um relatório de cobertura.

## 🎯 Casos de uso

- Prefeituras que precisam digitalizar mapas de arruamento em CAD/PDF.
- Pesquisadores que estudam a evolução da malha urbana municipal.
- Planejamento urbano, cadastro imobiliário, mobilidade.
- Comparação entre mapas oficiais e o OpenStreetMap para identificar lacunas da base comunitária.

## 📋 Requisitos

- **Python 3.11 ou 3.12** (recomendado). Python 3.13 pode funcionar, mas algumas dependências geoespaciais podem não ter *wheels* prontas para Windows.
- **Conexão com internet** (para baixar a malha do OSM).
- **~500 MB de espaço em disco** para as dependências.

### Dependências principais

| Pacote | Papel |
|---|---|
| `pymupdf` | Extração de texto do PDF |
| `osmnx` | Download da malha viária do OSM |
| `geopandas`, `shapely` | Manipulação geoespacial |
| `scikit-learn` | Validação espacial (RANSAC) |
| `fastapi`, `uvicorn` | Servidor web local |
| `pyogrio`, `pyarrow` | Leitura e escrita de GeoPackage/Parquet |

## 🚀 Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/SEU_USUARIO/logradouros-app.git
cd logradouros-app
