# Guia de Importação Excel - Troubleshooting

## Erro: "Erro ao processar arquivo Excel"

### Causas Comuns

1. **Formato de arquivo incorreto**
   - ❌ Arquivo .csv, .txt ou outro formato
   - ✅ Use apenas .xlsx ou .xls

2. **Cabeçalhos incorretos ou ausentes**
   - ❌ Primeira linha sem cabeçalhos
   - ❌ Nomes de colunas diferentes
   - ✅ Use exatamente os nomes especificados

3. **Dados vazios ou inválidos**
   - ❌ Planilha sem dados (apenas cabeçalhos)
   - ❌ Coluna "Código" vazia
   - ✅ Preencha pelo menos o código

4. **Formato de data inválido**
   - ❌ Texto não reconhecido como data
   - ✅ Use formato DD/MM/AAAA ou deixe o Excel formatar

---

## Melhorias Implementadas

### 1. ✅ Logs Detalhados no Console

Agora, quando houver erro, abra o Console do navegador (F12) e você verá:

```
Iniciando validação de X linhas
Processando linha 2: {dados...}
Erro ao processar linha 3: [detalhes do erro]
Validação concluída. Novos registros: X
```

### 2. ✅ Validação de Cabeçalhos

O sistema agora verifica se os cabeçalhos estão corretos e mostra:
- Cabeçalhos esperados
- Cabeçalhos encontrados
- Aviso se houver diferença

### 3. ✅ Tratamento de Erros Robusto

- Try-catch em cada linha processada
- Erros não param a importação completa
- Linhas com erro são ignoradas, outras são processadas

### 4. ✅ Proteção em Funções de Data

- `formatDate()` com try-catch
- `extractMonthYear()` com try-catch
- Valores padrão se houver erro

---

## Como Usar o Console para Debug

### Passo 1: Abrir Console
- **Chrome/Edge**: F12 ou Ctrl+Shift+J
- **Firefox**: F12 ou Ctrl+Shift+K
- **Safari**: Cmd+Option+C

### Passo 2: Tentar Importar
1. Clique em "Importar Excel"
2. Selecione o arquivo
3. Observe as mensagens no console

### Passo 3: Identificar o Problema

**Se ver:**
```
Cabeçalhos encontrados: Codigo, Data, Tipo...
Cabeçalhos esperados: Código, Data, Tipo de Ocorrência...
```
**Solução:** Corrija os nomes dos cabeçalhos (note o acento em "Código")

**Se ver:**
```
Erro ao processar linha 5: Cannot read property 'trim' of undefined
```
**Solução:** A linha 5 tem algum campo vazio ou inválido

**Se ver:**
```
Erro em formatDate: Invalid Date
```
**Solução:** O formato da data na planilha não é reconhecido

---

## Template de Planilha Correta

### Estrutura Exata

```
| Código | Data       | Tipo de Ocorrência | Notificada | Severidade/Gravidade | Tipo de Incidente - OMS por Mês | Status | Responsável | Fase | Processo |
|--------|------------|-------------------|------------|---------------------|--------------------------------|--------|-------------|------|----------|
```

### Exemplo de Linha Válida

```
| 426 | 15/11/2025 | Queda | Unidade Sesi Tabuleiro | Circunstância de Risco (Saúde) | Não Classificado | Em Andamento | fania.silva | Analisar Causa e Fazer Plano de Ação | Administrar Consultas/ Exames de Saúde |
```

---

## Checklist Antes de Importar

### ✅ Arquivo
- [ ] Formato .xlsx ou .xls
- [ ] Não está corrompido
- [ ] Abre normalmente no Excel

### ✅ Cabeçalhos (Linha 1)
- [ ] Código (com acento)
- [ ] Data
- [ ] Tipo de Ocorrência (não "Ocorrência")
- [ ] Notificada
- [ ] Severidade/Gravidade
- [ ] Tipo de Incidente - OMS por Mês (não "Tipo de Incidente - OMS")
- [ ] Status
- [ ] Responsável (com acento)
- [ ] Fase (não "Fase da Ocorrência")
- [ ] Processo

### ✅ Dados (Linha 2+)
- [ ] Pelo menos uma linha com dados
- [ ] Coluna "Código" preenchida em todas as linhas
- [ ] Datas em formato reconhecível (DD/MM/AAAA)
- [ ] Sem células mescladas
- [ ] Sem fórmulas complexas

---

## Solução Rápida: Exportar e Reimportar

### Método Mais Seguro

1. **Exporte os dados atuais**
   - Clique em "Exportar Excel"
   - Selecione todas as colunas
   - Baixe o arquivo

2. **Use como template**
   - Abra o arquivo exportado
   - Adicione/edite suas linhas
   - Mantenha os cabeçalhos exatos

3. **Importe de volta**
   - Clique em "Importar Excel"
   - Selecione o arquivo editado
   - Deve funcionar perfeitamente

---

## Mensagens de Erro e Soluções

### "Formato de arquivo inválido"
**Causa:** Arquivo não é .xlsx ou .xls
**Solução:** Salve como Excel 2007+ (.xlsx)

### "Arquivo Excel está vazio"
**Causa:** Planilha sem dados ou apenas cabeçalhos
**Solução:** Adicione pelo menos uma linha de dados

### "Nenhum dado válido encontrado"
**Causa:** Todas as linhas falharam na validação
**Solução:** 
1. Verifique se a coluna "Código" está preenchida
2. Verifique os cabeçalhos no console
3. Use o template exportado

### "Erro ao processar arquivo Excel"
**Causa:** Erro genérico durante processamento
**Solução:**
1. Abra o console (F12)
2. Veja os detalhes do erro
3. Corrija o problema específico
4. Tente novamente

---

## Suporte Adicional

### Informações Úteis para Debug

Ao reportar um problema, inclua:

1. **Mensagem de erro** (screenshot)
2. **Console do navegador** (F12 → Console tab)
3. **Primeira linha da planilha** (cabeçalhos)
4. **Exemplo de linha com dados**
5. **Versão do Excel** usada

### Teste Simples

Crie uma planilha com apenas:
```
Código | Data       | Tipo de Ocorrência | Notificada | Severidade/Gravidade | Tipo de Incidente - OMS por Mês | Status | Responsável | Fase | Processo
999    | 22/11/2025 | Teste             | Teste      | Não Informado        | Não Classificado                | Concluído | teste | Concluída | Teste
```

Se isso funcionar, o problema está nos seus dados.
Se não funcionar, o problema pode ser no navegador ou biblioteca.

---

## Status das Melhorias

✅ Logs detalhados no console
✅ Validação de cabeçalhos
✅ Try-catch em cada linha
✅ Proteção em funções de data
✅ Mensagens de erro mais claras
✅ Continuação mesmo com erros parciais
