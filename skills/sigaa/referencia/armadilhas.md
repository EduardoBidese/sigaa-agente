# Armadilhas do SIGAA com o Ui.Vision (Firefox)

Problemas encontrados em uso real e o que funcionou. Confira os nomes exatos da API em `get_authoring_guide`.

## `uiv.evaluate` devolve texto, não objeto

Arrays e objetos voltam como string JSON, às vezes codificada duas vezes. Retorne sempre
`JSON.stringify(...)` e decodifique do seu lado (se depois do primeiro `JSON.parse` ainda for string, decodifique
de novo).

## Link de menu que não abre

Muitos links do SIGAA chamam `jsfcljs(form, params, '_blank')`, que faz um submit JSF e abre em outra aba. Se o
clique não fizer nada:

1. Leia o HTML do link (`onclick`) para ver o formulário e os parâmetros.
2. Dispare o mesmo submit na aba atual (sem o `'_blank'`) com `uiv.evaluate`.
3. Espere a página carregar antes do próximo passo.

## Upload de arquivo

`uiv.page.fill` em `<input type="file">` falha no Firefox. O que funciona:

1. No computador do usuário, ponha o arquivo em base64 num JSON na área de transferência. No Windows:

   ```powershell
   $b = [Convert]::ToBase64String([IO.File]::ReadAllBytes("C:\caminho\arquivo.pdf"))
   Set-Clipboard -Value (@{ nome = "arquivo.pdf"; tipo = "application/pdf"; b64 = $b } | ConvertTo-Json -Compress)
   ```

   No macOS, o equivalente com `base64` e `pbcopy`.
2. Leia a área de transferência com `uiv.getVar('!clipboard')`.
3. Dentro de `uiv.evaluate`, decodifique o base64, monte um `File`, coloque num `DataTransfer` e atribua
   `input.files = dt.files`. Dispare o evento `change` no input.
4. Confira na tela se o nome do arquivo apareceu.

## Textos longos

Digitar textos grandes campo a campo é lento e pode perder caracteres. Ponha o texto na área de transferência
(mesmo método acima, sem base64) e atribua o valor ao campo com `uiv.evaluate`, disparando `input` e `change`.

## Codificação

As páginas são windows-1252. Caracteres fora dela (emoji, "●", "→", aspas tipográficas raras) viram "?" ou somem.
Troque por equivalentes simples antes de preencher.

## Sessão expirada

O SIGAA derruba a sessão depois de um tempo parado e às vezes ao usar o botão Voltar do navegador. Se a página
mostrar a tela de login ou "sessão expirada", peça para o usuário entrar de novo e recomece pelo portal do docente.
Use os links do próprio SIGAA, não o Voltar do navegador.
