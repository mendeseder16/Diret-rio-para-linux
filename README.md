# Diret-rio-para-linux

# Exemplo de Script Bash

```bash
#!/bin/bash

# Define variáveis
USUARIOS=("usuario1" "usuario2" "usuario3")
GRUPOS=("grupo1" "grupo2")
DIRETORIOS=("/home/usuario1" "/home/usuario2" "/home/diretorios")
PERMISSOES=(750 750 755)  # Permissões para cada diretório, respectivamente

# Cria grupos
for GRUPO in "${GRUPOS[@]}"; do
    if ! getent group "$GRUPO" > /dev/null 2>&1; then
        groupadd "$GRUPO"
        echo "Grupo $GRUPO criado."
    else
        echo "Grupo $GRUPO já existe."
    fi
done

# Cria usuários e associa a grupos
for USUARIO in "${USUARIOS[@]}"; do
    if ! id "$USUARIO" > /dev/null 2>&1; then
        useradd -m -G "${GRUPOS[0]}" "$USUARIO"
        echo "$USUARIO criado e adicionado ao grupo ${GRUPOS[0]}."
    else
        echo "Usuário $USUARIO já existe."
    fi
done

# Cria diretórios e define permissões
for idx in "${!DIRETORIOS[@]}"; do
    DIR="${DIRETORIOS[$idx]}"
    PERMISSAO="${PERMISSOES[$idx]}"

    if [ ! -d "$DIR" ]; then
        mkdir -p "$DIR"
        chmod "$PERMISSAO" "$DIR"
        echo "Diretório $DIR criado com permissões $PERMISSAO."
    else
        echo "Diretório $DIR já existe."
    fi
done

echo "Infraestrutura criada com sucesso!"
```

# Como Utilizar o Script

1. Crie um arquivo de script:
   Salve o código acima em um arquivo com a extensão `.sh`, por exemplo, `setup_infra.sh`.

2. Dê permissão de execução:
   Execute o seguinte comando no terminal para dar permissão de execução ao script:
   ```bash
   chmod +x setup_infra.sh
   ```

3. Execute o script:
   Basta rodar o script como superusuário:
   ```bash
   sudo ./setup_infra.sh
   ```

# Upload para o GitHub

1. Crie um repositório no GitHub.
2. Clone o repositório: 
   ```bash
   git clone https://github.com/SEU_USUARIO/NOME_DO_REPOSITORIO.git
   ```
3. Coloque o script no repositório:
   Mova o arquivo `setup_infra.sh` para a pasta do repositório clonado.

4. Faça o commit e o push:
   ```bash
   git add setup_infra.sh
   git commit -m "Adicionando script de configuração de infraestrutura"
   git push origin main
   ```

# Conclusão

Com este script, você terá uma infraestrutura de usuários, grupos e diretórios configurada automaticamente em novas máquinas virtuais. Você pode modificar o script conforme necessário para atender a requisitos específicos.
