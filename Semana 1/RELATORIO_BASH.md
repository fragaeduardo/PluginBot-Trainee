# 🚀 Bash para iniciantes
Este é um relatório que resume os ensinamentos da playlist "Bash for Beginners" da Microsoft.
- **Nome:** Eduardo Fraga Pereira
- **Data:** 21/11/2025


---
## 🧭 Navegação e ajuda
* `help cd`: Ajuda rápida para comandos internos do Bash.
* `man ls`: O manual completo (**Man**ual). Use `/termo` para buscar e `q` para sair
* `pwd`: Mostra o caminho atual (**P**rint **W**orking **D**irectory).
* `ls`: Lista arquivos.
    * `ls -a`: Mostra ocultos.
    * `ls -l`: Mostra detalhes (permissões, tamanho).
* `cd (nome da pasta)`: Entra na pasta.
* `cd ..`: Volta uma pasta.
* `cd ~`: Vai para sua pasta Home.
* `cd -`: Volta para o último lugar onde você estava.
> **Dica:** Usar `pushd pasta` para entrar numa pasta salvando o local atual na memória, e `popd` para voltar magicamente.



---
## 📂 Manipulando arquivos (CRUD)
* **Criar**:
    * `mkdir pasta`: Cria diretório. (`mkdir -p a/b/c` cria a árvore toda).
    * `touch arquivo.txt`: Cria arquivo vazio ou atualiza horário.
* **Mover/Renomear**:
    * `mv arquivo.txt pasta/`: Move
    * `mv antigo.txt novo.txt`: Renomeia.
* **Copiar**:
    * `cp arquivo.txt copia.txt`: Copia arquivo.
    * `cp -r pasta copia_pasta`: Copia diretório recursivamente.
* **Apagar** (Cuidado!):
    * `rm arquivo.txt`: Apaga arquivo.
    * `rm -r pasta`: Apaga diretório e tudo dentro. Sem volta.



---
## 🔍 Encontrando arquivos
* `find . -name "*.txt"`: Busca arquivos `.txt` na pasta atual e subpastas.
* `which python`: Mostra onde está o executável do python.
* `grep "erro" log.txt`: Busca a palavra "erro" dentro do arquivo `log.txt`.



---
## 📜 Lendo arquivos no terminal
* `cat arquivo.txt`: Mostra tudo de uma vez.
* `head arquivo.txt`: Mostra as primeiras 10 linhas.
* `tail arquivo.txt`: Mostra as últimas 10 linhas.
    * `tail -f log.txt`: Fica assistindo o arquivo crescer (bom para ver logs em tempo real).
* `less arquivo.txt`: Abre para leitura navegável (usar setas, `q` para sair)



---
## 🔀 Redirecionamentos
### Redirecionadores (`>`, `>>`)
* `comando > arquivo.txt`: Salva a saída no arquivo (sobrescrevendo).
* `comando >> arquivo.txt`: Adiciona ao final do arquivo (append).
* `comando 2> erros.txt`: Salva apenas os erros gerados.
#### O pipe (`|`): Joga a saída de um comando como entrada do próximo.
```bash
#Lista todos os arquivos e busca por "config" no resultado
ls -la | grep "config"

#Le um arquivo gigante e permite navegar nele
cat log_gigante.txt | less
```



---
## 🔐 Permissões (`chmod`)
Cada permissão é um número

Permissões:
`r` (ler = 4), `w` (escrever = 2), `x` (executar = 1) ---> 7 = 4+2+1 = permissão total.
* `chmod +x script.sh`: Torna o arquivo executável.
* `chmod 777 arquivo`: Dá permissão total (Tomar cuidado com isso).
    * Primeiro `7` -> dono do arquivo
    * Segundo `7` -> grupo do arquivo
    * Terceiro `7` -> outros (qqr pessoa)
* `chown usuario:grupo arquivo`: Muda o dono do arquivo



---
## 🤖 Bash scripting: automatizações
Crie um arquivo com extensão `.sh` e comece com o **Shebang**: `#!/bin/bash`.

### Variáveis
```bash
nome="Fulano"
echo "Olá, $nome!"
```

### Condicionais (`if`)
```bash
if [ "$nome" == "Fulano" ]; then
    echo "Pessoa encontrada!"
else
    echo "Pessoa não encontrada!"
fi
```

### Loops
```bash
contador=1
while [ $contador -le 5 ]; do #O -le significa <=
    echo "Contando: $contador"
    ((contador++))
done
```
```bash
for arquivo in *.txt; do
    echo "Arquivo encontrado: $arquivo"
done
```

### Funções
```bash
minha_funcao() {
    local var_local="Variável local, invisível fora daqui"
    echo "Executando função..."
}

minha_funcao #Chama a função
```



---
> Scripts são arquivos de texto. Para rodar, use `./script.sh` (se tiver permissão `+x`) ou `bash script.sh`.
