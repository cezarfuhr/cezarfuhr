# Instruções para Atualização Manual das Estatísticas

Este documento descreve os passos para coletar e atualizar as estatísticas dos projetos open-source agregados no `README.md` do perfil.

### Pré-requisitos

- É necessário ter a ferramenta `cloc` instalada. (ex: `sudo apt-get install cloc`)

### Passos

1.  **Navegue até a raiz do monorepo**.

2.  **Execute os seguintes comandos no seu terminal** para coletar os dados brutos. 

    **Total de Commits (some os resultados):**
    ```bash
    (cd projects/conductor && git rev-list --all --count)
    (cd projects/conductor-gateway && git rev-list --all --count)
    (cd projects/conductor-web && git rev-list --all --count)
    ```

    **Análise de Linguagens (some os valores de `code` para cada linguagem):**
    ```bash
    (cd projects/conductor && cloc . --json --exclude-dir=node_modules,dist)
    (cd projects/conductor-gateway && cloc . --json --exclude-dir=node_modules,dist)
    (cd projects/conductor-web && cloc . --json --exclude-dir=node_modules,dist)
    ```

    **Contribuidores Únicos (conte as linhas únicas):**
    ```bash
    ( (cd projects/conductor && git log --all --format='%aN') && (cd projects/conductor-gateway && git log --all --format='%aN') && (cd projects/conductor-web && git log --all --format='%aN') ) | sort -u | wc -l
    ```

    **Data Mais Recente (pegue a maior data):**
    ```bash
    (cd projects/conductor && git log -1 --format=%cd --date=short)
    (cd projects/conductor-gateway && git log -1 --format=%cd --date=short)
    (cd projects/conductor-web && git log -1 --format=%cd --date=short)
    ```

3.  **Processe os dados** conforme os cálculos (soma, valores mais altos, etc.).

4.  **Atualize a tabela** na seção `📊 Estatísticas Agregadas (Local)` do arquivo `README.md` com os novos valores.
