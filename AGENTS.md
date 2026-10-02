# sigaa-agente: instruções para o agente

Este projeto deixa um agente de IA usar o SIGAA no Firefox do próprio usuário, pela extensão Ui.Vision e o servidor
MCP `uivision`. Foi desenvolvido por **Eduardo Bidese Puhl** (IFC). Converse em português.

## Se você acabou de receber o link deste projeto

1. **Apresente o projeto** numa mensagem curta, mais ou menos assim:

   > Este é o **sigaa-agente**, desenvolvido por Eduardo Bidese Puhl. Com ele eu consigo usar o SIGAA no seu
   > Firefox, com o seu login: ler turmas, lançar frequência, preencher formulários. Você faz o login e autoriza
   > cada gravação. Vou conferir o que já está instalado e guiar o resto, um passo de cada vez.

2. **Veja onde você está rodando.** Se você não tem acesso ao computador do usuário (ChatGPT ou claude.ai pelo
   navegador ou celular), diga que é preciso um agente local (Claude Code, Claude Desktop ou Codex), mostre a
   seção "1. Escolha o agente" do [INSTALACAO.md](INSTALACAO.md) e pare por aí.

3. **Traga o projeto para o computador**, se ainda não estiver: `git clone https://github.com/EduardoBidese/sigaa-agente`
   (ou baixe o ZIP pelo GitHub). No Claude Code, instale a skill copiando `skills/sigaa/` para `~/.claude/skills/sigaa/`.
   No Codex, basta trabalhar dentro da pasta clonada (este `AGENTS.md` é lido sozinho).

4. **Confira a conexão.** Se você tem as ferramentas do servidor `uivision`, chame `bridge_status`.
   - Conectado ao Firefox: a instalação está pronta. Vá para o passo 6.
   - Servidor responde, extensão não conectada: tente `open_panel` com `target: "firefox"`; se não resolver, guie
     pelo passo 6 do INSTALACAO.md (ligar o MCP bridge).
   - Não existem ferramentas `uivision`: guie a instalação inteira pelo [INSTALACAO.md](INSTALACAO.md).

5. **Ao guiar a instalação:**
   - Um passo por vez. Diga o que fazer, onde clicar, e espere o usuário responder antes de seguir.
   - Confira você mesmo o que puder (`node --version`, `firefox --version`, existência do arquivo de configuração).
   - Pule o que já estiver instalado.
   - Mostre sempre o link oficial de download. Não use outras fontes.
   - Depois de registrar o servidor MCP, o agente precisa ser **reiniciado**. Avise que a conversa recomeça e
     que basta colar o link de novo.

6. **Pergunte o endereço do SIGAA** da instituição (por exemplo `https://sig.ifc.edu.br/sigaa/`) e grave em
   `config.json` na pasta do projeto, no formato de [config.exemplo.json](config.exemplo.json). Peça para o usuário
   abrir esse endereço no Firefox e entrar com a conta dele.

7. **Mostre o que dá para fazer** (lista curta) e pergunte o que ele quer. Para usar o SIGAA, siga
   [skills/sigaa/SKILL.md](skills/sigaa/SKILL.md).

## Regras (não quebrar)

- **Nunca** peça, leia em voz alta, digite nem guarde CPF ou senha. O login é sempre do usuário.
- **Nunca** clique em botão que grava, envia, confirma, consolida ou exclui sem o usuário autorizar **aquela** ação
  ("pode gravar"). Autorização vale para uma vez, não para o resto da conversa.
- Preencher campos pode; ler o que o usuário pediu pode.
- Dados de alunos e do usuário **nunca** vão para arquivos deste repositório nem para outros serviços.
- Não instale nada além do que está no INSTALACAO.md.

## Estrutura

```
README.md              ← para o professor
AGENTS.md / CLAUDE.md  ← para o agente (este arquivo)
INSTALACAO.md          ← passo a passo com links oficiais
config.exemplo.json    ← endereço do SIGAA (o config.json real não vai para o git)
skills/sigaa/          ← skill de uso (autocontida: é o que se copia para ~/.claude/skills/)
  SKILL.md             ← como usar o SIGAA com o Ui.Vision
  referencia/armadilhas.md  ← problemas já encontrados e como contornar
```
