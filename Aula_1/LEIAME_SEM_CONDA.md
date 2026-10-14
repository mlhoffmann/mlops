# Aula 1 - MLOps Stack Para Otimização de Hiperparâmetros com MLflow e Optuna (Sem Conda)

Este guia é para quem não tem Conda instalado. Você só precisa ter Python e pip instalados.

## Requisitos

- Python 3.12 ou superior
- pip (geralmente já vem com Python)
- VSCode com as seguintes extensões instaladas:
  - **Python** (extensão oficial da Microsoft)
  - **Jupyter** (extensão oficial da Microsoft)

## Passo 1: Criar o ambiente virtual

Abra o **CMD** (Prompt de Comando) - **não use PowerShell** nos notebooks da Dell pois ele não tem permissão para rodar scripts.

Navegue até a pasta `Aula_1` e execute:

```cmd
python -m venv mlopsp1
```

## Passo 2: Ativar o ambiente virtual

No CMD, execute:

```cmd
mlopsp1\Scripts\activate
```

Você verá `(mlopsp1)` aparecer no início da linha de comando, indicando que o ambiente está ativo.

## Passo 3: Instalar as dependências

Com o ambiente virtual ativado, execute:

```cmd
pip install -r requirements.txt
pip install watermark
pip install ipykernel
```

## Passo 4: Configurar o VSCode

1. **Reinicie o VSCode** após criar o ambiente virtual
2. Abra o arquivo `Aula_1.ipynb`
3. No canto superior direito do arquivo, clique onde aparece "Select Kernel"
4. Selecione o Python interpreter: `Aula_1\mlopsp1\Scripts\python.exe`. Se não aparecer, clique em "Enter interpreter path..." e insira esse path.

**Nota:** Recomendo usar a extensão Jupyter do VSCode em vez de executar `jupyter notebook` diretamente.

## Passo 5: Executar o MLflow Server

Para rodar o servidor MLflow, abra um **novo terminal CMD** com o ambiente virtual ativado e execute:

```cmd
mlflow server --host 127.0.0.1 --port 8282
```

## Passo 6: Desativar o ambiente virtual (opcional)

Quando terminar, você pode desativar o ambiente:

```cmd
deactivate
```

## Remover o ambiente virtual (opcional)

Se quiser remover o ambiente virtual completamente:

```cmd
rmdir /s /q mlopsp1
```

## Solução de Problemas

- **Se o kernel não aparecer:** Certifique-se de reiniciar o VSCode após criar o ambiente virtual
- **Se tiver problemas de permissão:** Use CMD em vez de PowerShell
- **Se o mlflow não for encontrado:** Verifique se o ambiente virtual está ativado antes de rodar o comando
