# Configuração do Template de TCC - CEFET(V) para Utilização Local no Windows com WSL.

## Template

Este é o [Template](https://github.com/lucasmsoares96/Template-Monografia-CEFET-MG) oficialmente disponibilizado pelo [CEFET-MG campus V (Divinópolis-MG)](https://www.eng-computacao.divinopolis.cefetmg.br/2019/03/19/tcc/). Clone o repositório conforme a documentação original.

```
git clone --recurse-submodules https://github.com/lucasmsoares96/Template-Monografia-CEFET-MG.git
```

## Pré-Requisitos

* Windows 10 ou superior
* [WSL instalado e configurado](https://learn.microsoft.com/pt-br/windows/wsl/install)
* VSCode com as extensões **LaTeX Workshop**, **Code Spell Checker**, **WSL** e **Remote-Explorer** instaladas
* Distribuição Linux (Preferência por derivadas do **Debian**) rodando no WSL

## Instalando o Latex no WSL

```bash
sudo apt update
sudo apt install texlive-full -y
sudo apt install latexmk 
```

Esse processo pode demorar, pois o pacote `texlive-full` é grande.

## Configurações

1. Abra o VSCode, vá até o explorador remoto e conecte-se a distribuição na qual fez a instalação do Latex.
2. Abra as configurações `settings.json`, cole as configurações abaixo e salve.
  ```json
  {
      // Code Spell Checker
      "cSpell.language": "pt, en",
      "cSpell.enabledFileTypes": {"tex": true, "md": true, "txt": true, "*": false},
      "cSpell.allowCompoundWords": true,
  
      // latex workshop
      "latex-workshop.latex.outDir": "out",
      "latex-workshop.view.pdf.viewer": "tab",
      "latex-workshop.view.pdf.ref.viewer": "tabOrBrowser",
      "latex-workshop.latex.autoBuild.run": "onSave",
      "latex-workshop.latex.recipes": [
          {
              "name": "latexmk (out)",
              "tools": ["latexmk-out"]
          }
      ],
      "latex-workshop.latex.tools": [
          {
              "name": "latexmk-out",
              "command": "latexmk",
              "args": [
                  "-pdf",
                  "-output-directory=out",
                  "%DOC%",
                  "-synctex=1",
                  "-interaction=nonstopmode",
                  "-file-line-error"
              ]
          }
      ]
  }
  ```
> 💡 Essa configuração compila o `.tex` automaticamente ao salvar e gera os PDFs na pasta `out`, além de permitir que o clique no PDF leve até a linha do código-fonte.

3. Navegue até a pasta do template da sua maquina local (dica: `/mnt/c/Users`) e encontre a pasta do template.

## Utilização

* Use o comando `Ctrl+Alt+B` para compilar manualmente (se necessário).
* O atalho `Ctrl+Alt+V` deve abrir o PDF compilado.
* Caso queira compilar manualmente, utilize o comando abaixo, disponibilizado pela documentação original.
```bash
latexmk -pdf -output-directory=out main.tex
```

### Dicas
* Certifique-se de estar com o VSCode aberto no WSL (ícone do WSL no canto inferior esquerdo).
* Todas as vezes que salvar o `.tex`, será recompilado automaticamente, por isso, deixe o terminal de saída ativo para ver se a recompilação terminou.
  * Caso queira alterar esta configuração, vá no `settings.json` e altere  `"latex-workshop.latex.autoBuild.run": "onSave"`.

