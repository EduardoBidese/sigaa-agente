---
name: sigaa
description: Usa o SIGAA (sistema acadêmico usado por institutos e universidades federais) no Firefox do próprio usuário pela extensão Ui.Vision e o servidor MCP uivision. Use quando o usuário pedir algo no SIGAA - ver turmas e alunos, lançar frequência, conferir notas, ler declarações, preencher projetos, editais e relatórios, enviar PDF. Login sempre manual; nada é gravado sem autorização.
---

# SIGAA pelo Firefox (Ui.Vision)

Projeto [sigaa-agente](https://github.com/EduardoBidese/sigaa-agente), de Eduardo Bidese Puhl.
Se o servidor `uivision` não estiver instalado, siga o `INSTALACAO.md` do projeto.

## Antes de começar

1. Chame `bridge_status`. Se a extensão não estiver conectada, tente `open_panel` com `target: "firefox"`.
   Se continuar, peça para o usuário abrir o painel do Ui.Vision no Firefox > Settings > AI > ligar
   **MCP bridge** (porta 50888) > **Test**, e deixar o painel aberto.
2. Se o servidor `uivision` nem subir (erro no começo da sessão), avise o usuário antes de tentar outro caminho.
   Não troque para outro navegador nem para Playwright: o SIGAA funciona melhor no Firefox com o Ui.Vision.
3. Na primeira vez da sessão, chame `get_authoring_guide` para conhecer a API de macros e de JavaScript
   (`uiv.*`). Não invente nomes de comando.
4. Endereço do SIGAA: `config.json` na pasta do projeto (formato em `config.exemplo.json`). Se não existir,
   pergunte ao usuário e grave.

## Regras

- **Login é do usuário.** Nunca peça, digite nem guarde CPF ou senha. Se cair na tela de login, peça para ele
  entrar e diga quando continuar.
- **Ler e preencher pode. Gravar, não.** Botões como *Gravar*, *Salvar*, *Enviar*, *Confirmar*, *Submeter*,
  *Consolidar*, *Finalizar* e *Excluir* só com autorização explícita do usuário para **aquela** ação
  ("pode gravar"). Depois de gravar, confira a mensagem "Operação realizada com sucesso!" e diga o resultado.
- Se o agente ou o ambiente bloquear o clique em um botão de gravar, não insista: o usuário clica e você preenche
  a próxima tela.
- Só faça o que o usuário pediu. Não navegue por outras áreas "para conferir".
- Não grave dados de alunos em arquivos do repositório.

## Navegação

- Comece pelo portal do docente (`portal_docente` do config) e siga os menus como uma pessoa faria.
- Para ler uma tela, prefira o texto da página (`get_page` / `browser_snapshot`) a capturas de tela.
- Os menus do SIGAA são JSF. Se um clique não funcionar, veja `referencia/armadilhas.md`.

## Frequência

Caminho: Portal do Docente > turma > **Alunos** > **Lançar Freq. em Planilha**.

1. Leia a planilha e mostre ao usuário as datas e o que já está lançado.
2. Pergunte quem veio (ou quem faltou) em cada data. Não suponha.
3. O valor de cada célula é o **número de faltas** do aluno naquela data: `0` = presente; falta inteira = número de
   aulas do dia (confira na tela, por exemplo `5`). Vazio = não lançado. Colunas marcadas como feriado não se lançam.
4. Preencha, mostre um resumo (data, presentes, faltosos) e **pare**. Só clique em **Gravar Frequências** quando o
   usuário disser "pode gravar".

## Formulários longos (projetos, editais, relatórios)

- Preencha uma tela por vez e mostre o que foi preenchido antes de avançar.
- Textos longos vão melhor pela área de transferência (veja armadilhas). Respeite o limite de caracteres de cada
  campo (muitos são de 8000) e use só caracteres que existem em windows-1252: nada de emoji, "●", "→".
- "Gravar e Avançar" também é gravar: precisa de autorização.

## Enviar arquivo (PDF)

Preencher `<input type="file">` direto não funciona no Firefox. Use o método da área de transferência descrito em
`referencia/armadilhas.md`.
