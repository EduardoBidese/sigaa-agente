# sigaa-agente

Use o **SIGAA** com a ajuda de um agente de IA (Claude ou Codex/ChatGPT). O agente abre as telas, lê as turmas,
preenche a planilha de frequência e os formulários no **seu** Firefox, com o **seu** login. Você confere e
autoriza cada gravação.

Desenvolvido por **Eduardo Bidese Puhl** (IFC).

## Como começar

1. Abra um agente que rode **no seu computador**: [Claude Code](https://claude.com/claude-code),
   [Claude Desktop](https://claude.ai/download) ou [Codex](https://openai.com/codex).
2. Cole este link na conversa e peça: *"Configure este projeto para mim"*:

   ```
   https://github.com/EduardoBidese/sigaa-agente
   ```

3. O agente vai guiar a instalação, um passo de cada vez. O passo a passo completo também está em
   [INSTALACAO.md](INSTALACAO.md), se você preferir fazer sozinho.

> **ChatGPT ou Claude pelo site/celular não funcionam.** Eles não têm acesso ao seu computador, então não
> conseguem controlar o Firefox. Quem usa ChatGPT pode usar o **Codex**, que vem com a mesma assinatura.

## O que é instalado (tudo gratuito)

| Programa | Para quê |
|---|---|
| [Firefox](https://www.mozilla.org/pt-BR/firefox/new/) | O navegador onde você entra no SIGAA |
| [Ui.Vision](https://addons.mozilla.org/pt-BR/firefox/addon/rpa/) | Extensão do Firefox que deixa o agente clicar e ler a página |
| [Node.js](https://nodejs.org/pt) | Roda a ponte entre o agente e a extensão |
| [uivision-mcp-bridge](https://ui.vision/mcp) | A ponte (MCP), oficial do Ui.Vision |

## O que ele faz

- Lê turmas, alunos, frequências, notas e declarações.
- Preenche a planilha de frequência a partir de quem você disser que veio.
- Ajuda a preencher formulários longos (projetos, editais, relatórios), inclusive com envio de PDF.

## Segurança

- **Você faz o login.** O agente nunca pede nem digita CPF ou senha.
- **Nada é gravado sem você mandar.** O agente preenche e para; botões como *Gravar*, *Enviar* ou *Excluir* só são
  clicados quando você autoriza aquela ação (por exemplo, "pode gravar").
- Tudo roda no seu computador: a ponte só aceita conexões locais (`127.0.0.1`).
- Os dados das telas que o agente lê vão para o serviço de IA que você usa (Anthropic ou OpenAI), como em qualquer
  conversa com ele. Siga as regras da sua instituição sobre dados de alunos.

## Para agentes de IA

Se você é um agente e recebeu este link, leia [AGENTS.md](AGENTS.md)
(`https://raw.githubusercontent.com/EduardoBidese/sigaa-agente/main/AGENTS.md`) e siga as instruções.

## Licença

[MIT](LICENSE). O SIGAA é um sistema da UFRN usado por várias instituições; este projeto não tem vínculo com a UFRN,
com o Ui.Vision nem com as empresas dos agentes.
