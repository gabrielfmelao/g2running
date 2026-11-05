# Leads do site G2 → Google Sheets

Os cadastros do site (nome, e-mail, celular, cor escolhida) caem numa planilha do Google Sheets, sem servidor.

## Passo a passo (5 minutos)

1. Abra a planilha: https://docs.google.com/spreadsheets/d/1cU5fnMqfv2JiF8Fiir4r1bTh-OjaD6-FJHsceUDCZT0/edit
2. Na primeira linha, escreva os cabeçalhos: `Data`, `Nome`, `E-mail`, `Celular`, `Cor`, `Origem`.
3. Menu **Extensões > Apps Script**. Apague o que estiver lá e cole o código abaixo.
4. Clique em **Implantar > Nova implantação**. Tipo: **App da Web**. Executar como: **Eu**. Quem pode acessar: **Qualquer pessoa**. Clique em Implantar e autorize.
5. Copie a URL gerada (termina em `/exec`) e cole dentro das aspas de `LEAD_ENDPOINT` em `site/index.html`.
6. Faça um cadastro de teste no site e confira a linha na planilha.

Para baixar em Excel: **Arquivo > Fazer download > Microsoft Excel (.xlsx)**.

## Código do Apps Script

```javascript
function doPost(e) {
  var d = JSON.parse(e.postData.contents || '{}');
  var sh = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
  sh.appendRow([
    new Date(),
    d.nome || '',
    d.email || '',
    d.celular || '',
    d.cor || '',
    d.origem || ''
  ]);
  return ContentService.createTextOutput('ok');
}
```

## Se mudar o código depois

Toda alteração no Apps Script exige **Implantar > Gerenciar implantações > editar > Nova versão**. Só salvar não atualiza a URL.
