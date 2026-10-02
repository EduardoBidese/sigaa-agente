# Instalação

Leva uns 15 minutos. Tudo é gratuito, exceto a assinatura do agente de IA (que você provavelmente já tem).
Se um agente estiver guiando você, ele faz um passo por vez e pula o que já estiver instalado.

## 1. Escolha o agente

O agente precisa rodar **no seu computador**, porque é ele que conversa com o Firefox.

| Agente | Assinatura | Download |
|---|---|---|
| Claude Desktop | Claude Pro ou superior | https://claude.ai/download |
| Claude Code | Claude Pro ou superior | https://claude.com/claude-code |
| Codex | ChatGPT Plus ou superior | https://openai.com/codex |

**Não funcionam:** ChatGPT e claude.ai pelo navegador ou pelo celular.

## 2. Firefox

Baixe em https://www.mozilla.org/pt-BR/firefox/new/ (pule se já tiver).

## 3. Node.js

Baixe a versão **LTS** em https://nodejs.org/pt e instale com as opções padrão (precisa ser a 18 ou mais nova).
Para conferir, abra um terminal (no Windows: tecla Windows, digite `cmd`, Enter) e rode:

```
node --version
```

Deve aparecer algo como `v22.x.x`. Se acabou de instalar e o comando não for encontrado, feche e abra o terminal.

## 4. Extensão Ui.Vision no Firefox

1. Abra https://addons.mozilla.org/pt-BR/firefox/addon/rpa/ **no Firefox**.
2. Clique em **Adicionar ao Firefox** e aceite as permissões.
3. Fixe o ícone na barra: clique na peça de quebra-cabeça (Extensões) no canto direito, depois na engrenagem ao lado
   de Ui.Vision > **Fixar na barra de ferramentas**.

Precisa ser a versão 10.0.21 ou mais nova (a da loja já é).

## 5. Ponte MCP (liga o agente à extensão)

Rode no terminal:

```
npx uivision-mcp-bridge@latest --setup
```

Ele registra a ponte sozinho nos agentes instalados. Se perguntar algo, aceite. Depois **feche e abra o agente de
novo** (no Claude Desktop, feche pela bandeja do sistema, não só a janela).

Se o agente continuar sem as ferramentas `uivision`, registre na mão:

**Claude Desktop:** menu Configurações > Desenvolvedor > Editar configuração, e coloque no `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "uivision": { "command": "npx", "args": ["-y", "uivision-mcp-bridge"] }
  }
}
```

No Windows, se não funcionar, troque a linha por
`"uivision": { "command": "cmd", "args": ["/c", "npx", "-y", "uivision-mcp-bridge"] }`.

**Claude Code:** no terminal,

```
claude mcp add --scope user uivision -- npx -y uivision-mcp-bridge
```

No Windows: `claude mcp add --scope user uivision -- cmd /c npx -y uivision-mcp-bridge`.

**Codex:** acrescente no arquivo `~/.codex/config.toml` (no Windows, `C:\Users\SEU_USUARIO\.codex\config.toml`):

```toml
[mcp_servers.uivision]
command = "npx"
args = ["-y", "uivision-mcp-bridge"]
startup_timeout_sec = 120
tool_timeout_sec = 900
```

Mais detalhes na página oficial: https://ui.vision/mcp

## 6. Ligar a ponte no Firefox

1. Clique no ícone do Ui.Vision. Abre uma janela (o "painel").
2. No painel, clique em **Settings** (engrenagem) > aba **AI**.
3. Ligue **MCP bridge** (porta `50888`, a padrão) e clique em **Test**.
4. **Deixe o painel aberto** (pode minimizar). Se fechar, o agente perde a conexão.

## 7. Teste

Volte ao agente e peça: *"Confira a conexão com o Ui.Vision"*. Ele deve responder que está conectado ao Firefox.

Pronto. Abra o SIGAA da sua instituição no Firefox, **faça o login você mesmo** e diga ao agente o que quer fazer.

## Problemas comuns

| Sintoma | O que fazer |
|---|---|
| O agente não tem ferramentas `uivision` | Reinicie o agente. Confira o `node --version`. No Windows, use a variante com `cmd /c` do passo 5. |
| "Extensão não conectada" | O painel do Ui.Vision está fechado. Abra pelo ícone, Settings > AI > Test. |
| Funcionava e parou | Só uma sessão de agente por vez usa a porta 50888. Feche a outra conversa/janela de agente. |
| Nada acontece na janela anônima | Em `about:addons` > Ui.Vision, permita **Executar em janelas privativas**, ou use uma janela normal. |
| O SIGAA voltou para a tela de login | A sessão expirou. Entre de novo e peça para o agente continuar. |
