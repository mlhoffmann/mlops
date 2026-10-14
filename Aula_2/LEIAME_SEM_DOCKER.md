# Aula 2 - MLOps da Concepção ao Deploy - Sistema de LLM/RAG (Sem Docker)

Este guia é para quem não tem Docker Desktop instalado (como nas máquinas Dell) e precisa usar Podman como alternativa.

## Requisitos

- **Python 3.12** (versão específica necessária devido às dependências no requirements.txt)
- pip (geralmente já vem com Python)
- **WSL2 ou Hyper-V** (Podman requer um provedor de virtualização no Windows)
- **Podman** (instalado via Company Portal)
- VSCode com as seguintes extensões instaladas:
  - **Python** (extensão oficial da Microsoft)
  - **Jupyter** (extensão oficial da Microsoft)

## Passo 1: Verificar e instalar WSL2 ou Hyper-V

Abra o **CMD** (Prompt de Comando) - **não use PowerShell** nos notebooks da Dell pois ele não tem permissão para rodar scripts.

O Podman no Windows requer um provedor de virtualização. Você pode usar **WSL 2** (recomendado) ou **Hyper-V**.

### Opção A: Usar WSL 2 (recomendado)

Verifique se o WSL já está instalado:

```cmd
wsl --version
```

Se o WSL não estiver instalado, siga os passos do onboarding da empresa para instalar o WSL2.

### Opção B: Usar Hyper-V

Se o WSL não estiver disponível, você pode usar Hyper-V. Verifique se o Hyper-V está habilitado:

```cmd
dism /online /get-featureinfo /featurename:Microsoft-Hyper-V-All
```

Se não estiver habilitado, você precisará habilitá-lo (pode requerer reinicialização).

## Passo 2: Instalar o Podman

Acesse o **Company Portal** e instale o Podman.

## Passo 3: Criar a máquina Podman

Após instalar o Podman, abra o CMD e execute:

```cmd
podman machine init
```

## Passo 4: Iniciar a máquina Podman

Execute o comando para iniciar a máquina Podman:

```cmd
podman machine start
```

Verifique se a máquina está rodando:

```cmd
podman machine list
```

## Passo 5: Verificar a versão do Python

Verifique se você tem Python 3.12 instalado:

```cmd
python --version
```

Se a versão não for 3.12, tente:

```cmd
python3.12 --version
```

## Passo 7: Criar o ambiente virtual

Navegue até a pasta `Aula_2` e execute (use o comando que funcionou no passo anterior):

```cmd
python -m venv mlopsp2
```

ou

```cmd
python3.12 -m venv mlopsp2
```

## Passo 8: Ativar o ambiente virtual

No CMD, execute:

```cmd
mlopsp2\Scripts\activate
```

Você verá `(mlopsp2)` aparecer no início da linha de comando, indicando que o ambiente está ativo.

## Passo 9: Instalar as dependências

Com o ambiente virtual ativado, execute:

```cmd
pip install -r requirements.txt
```

## Passo 10: Executar o pipeline

O Podman geralmente cria um alias automático para o comando `docker`, então você pode tentar executar diretamente:

```cmd
python Aula2-05-Executa-Pipeline.py
```

**Se o comando `docker` não for reconhecido**, você precisará modificar o arquivo `Aula2-05-Executa-Pipeline.py` substituindo `docker` por `podman` nas linhas 29, 36 e 54:

- Linha 29: `podman run --name mlh-aula2 -p 5222:5432 -e POSTGRES_USER=mlh -e POSTGRES_PASSWORD=mlh1010 -e POSTGRES_DB=mlhdb -d postgres:16.1`
- Linha 36: `podman rm -f mlh-aula2`
- Linha 54: `podman rm -f mlh-aula2`

## Passo 11: Desativar o ambiente virtual (opcional)

Quando terminar, você pode desativar o ambiente:

```cmd
deactivate
```

## Passo 12: Parar a máquina Podman (opcional)

Quando não estiver mais usando o Podman, pode parar a máquina:

```cmd
podman machine stop
```

## Remover o ambiente virtual (opcional)

Se quiser remover o ambiente virtual completamente:

```cmd
rmdir /s /q mlopsp2
```

## Solução de Problemas

- **Se o Podman não iniciar:** Verifique se o WSL2 ou Hyper-V está instalado e funcionando corretamente
- **Se tiver problemas de permissão:** Use CMD em vez de PowerShell
- **Se o container não iniciar:** Verifique se a máquina Podman está rodando com `podman machine list`
- **Se tiver erros de dependência:** Certifique-se de estar usando Python 3.12 exatamente
- **Se o comando `docker` não for reconhecido:** O Podman geralmente cria um alias automático, mas se não funcionar, modifique o script `Aula2-05-Executa-Pipeline.py` substituindo `docker` por `podman` nas linhas 29, 36 e 54
