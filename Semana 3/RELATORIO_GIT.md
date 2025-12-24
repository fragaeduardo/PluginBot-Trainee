# 🎓 Git completo
Este é um relatório que resume os ensinamentos do curso "Usando Git Direito: O Guia Definitivo" do Fábio Akita.
- **Nome:** Eduardo Fraga Pereira
- **Data:** 20/12/2025



---
## 🚫 NÃO escrever mensagens de commit ruins
Evitar mensagens como `fix`, `wip`, `arrumando`.
Se errou a mensagem do último commit, conserte:
```bash
git commit --amend -m "Mensagem correta e descritiva"
```



---
## 🛠️ Consertando antes de enviar para o servidor
### 1. "Commits" errados ou incompletos
Para commits locais ruins (`fix`, `fix 2`, `agora vai`) que precisam ser unidos antes do envio para o `master`:

**Opção A: Reset Soft**

Volta os commits para o estado de *staged*, mantendo as alterações
```bash
#Desfaz os últimos 3 commits, mas mantém os arquivos modificados
git reset --soft HEAD~3
#Faça um commit único e decente
git commit -m "Implementa funcionalidade X completa"
```

**Opção B: Rebase Interativo**

Permite reescrever a história, juntar (squash), editar ou remover commits.
```bash
git rebase -i HEAD~3
```
*No editor, trocar `pick` por `squash` (ou `s`) nos commits a serem fundidos.*



### 2. "Commits" lixo que precisam ser apagados
Para reverter o código exatamente ao estado anterior:
> **Obs:** CONFERIR COM CUIDADO ANTES DE RODAR ISSO
```bash
git reset --hard HEAD~1
```



### 3. Desfazendo o `reset --hard`
O Git raramente apaga dados imediatamente. Utilizar `reflog` para localizar commits perdidos.
```bash
git reflog
#Ache o hash do commit perdido (ex: a1b2c3d)
git reset --hard a1b2c3d
```



---
## 📦 Staging area
Não executar `git add .` cegamente. Caso haja alterações em arquivos de tarefas diferentes, separar os commits.

### `git add -p` (Patch)
O Git questionará trecho por trecho o que deve ser adicionado.

```bash
git add -p
```
- `y`: Sim, adiciona este pedaço.
- `n`: Não, pula este pedaço.
- `s`: Split (divide o pedaço em pedaços menores)



---
## 🐘 Arquivos gigantes (binários)
O Git não lida bem com binários (PSD, MP4, ZIP), salvando o arquivo inteiro a cada mudança e inflando o repositório.

**Solução: Git LFS (Large File Storage)**
Armazena apenas um ponteiro no Git, e o arquivo real vai para um servidor separado.
```bash
git lfs install #1. Instala o LFS
git lfs track "*.psd" #2. Quais arquivos rastrear
git add .gitattributes #3. Comite o arquivo .gitattributes gerado
```



---
## 🧹 Limpando a casa (BFG Repo-Cleaner)
Caso senhas ou arquivos gigantes tenham sido comitados, eles permanecem no histórico mesmo após exclusão

Para reescrever a história e limpar a sujeira (muito mais rápido que `git filter-branch`):
1.  Baixe o **BFG Repo-Cleaner** (requer Java).
2.  Faça um clone *mirror* do repositório:
    ```bash
    git clone --mirror url-do-seu-repo.git
    ```
3.  Rode o BFG para apagar arquivos grandes ou senhas:
    ```bash
    #Apaga os arquivos maiores que 100MB
    java -jar bfg.jar --strip-blobs-bigger-than 100M repo.git
    ```
4.  Limpe o lixo e force o push:
    ```bash
    cd repo.git
    git reflog expire --expire=now --all && git gc --prune=now --aggressive
    git push --force
    ```



---
> **Dicas:** **NAO** adotar modismos. **NAO** utilizar Monorepo apenas por popularidade. Utilizar a ferramenta adequada para a escala do problema.
