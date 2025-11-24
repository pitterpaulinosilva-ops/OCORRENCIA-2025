# Atualização da Importação/Exportação Excel

## Data: 22/11/2025

### Objetivo
Ajustar a funcionalidade de importação para aceitar planilhas Excel com as colunas no formato especificado.

---

## Formato da Planilha Excel

### Colunas Obrigatórias (em ordem)

| # | Nome da Coluna | Descrição | Exemplo |
|---|----------------|-----------|---------|
| 1 | **Código** | Código único da ocorrência | 233, 252, 257 |
| 2 | **Data** | Data da ocorrência | 13/06/2024 |
| 3 | **Tipo de Ocorrência** | Descrição do tipo | Identificação Errada do Paciente |
| 4 | **Notificada** | Unidade onde ocorreu | Unidade Sesi Cambona |
| 5 | **Severidade/Gravidade** | Nível de severidade | Evento com Nenhum Dano (Saúde) |
| 6 | **Tipo de Incidente - OMS por Mês** | Classificação OMS | Não Classificado |
| 7 | **Status** | Status atual | Concluído / Em Andamento |
| 8 | **Responsável** | Responsável pela ocorrência | carolina.albuquerque |
| 9 | **Fase** | Fase atual do processo | Concluída |
| 10 | **Processo** | Processo relacionado | Administrar Consultas/Exames |

---

## Mapeamento de Colunas

### Importação (Excel → Sistema)

```javascript
{
    'Código' → codigo
    'Data' → data, mes_ano
    'Tipo de Ocorrência' → ocorrencia
    'Notificada' → notificada, notificadora (padrão)
    'Severidade/Gravidade' → severidade
    'Tipo de Incidente - OMS por Mês' → tipo_incidente_oms
    'Status' → status
    'Responsável' → responsavel
    'Fase' → fase
    'Processo' → processo
}
```

### Exportação (Sistema → Excel)

As mesmas colunas são exportadas no mesmo formato, garantindo compatibilidade bidirecional.

---

## Alterações Implementadas

### 1. ✅ Função `validateAndProcessImportedData()`

**Antes:**
```javascript
ocorrencia: String(row['Ocorrência'] || '').trim()
tipo_incidente_oms: String(row['Tipo de Incidente - OMS'] || '').trim()
fase: String(row['Fase da Ocorrência'] || '').trim()
```

**Depois:**
```javascript
ocorrencia: String(row['Tipo de Ocorrência'] || '').trim()
tipo_incidente_oms: String(row['Tipo de Incidente - OMS por Mês'] || '').trim()
fase: String(row['Fase'] || '').trim()
```

### 2. ✅ Função `exportToExcel()`

**Mapeamento atualizado:**
```javascript
const columnMapping = {
    codigo: 'Código',
    data: 'Data',
    ocorrencia: 'Tipo de Ocorrência',
    notificada: 'Notificada',
    severidade: 'Severidade/Gravidade',
    tipo_incidente_oms: 'Tipo de Incidente - OMS por Mês',
    status: 'Status',
    responsavel: 'Responsável',
    fase: 'Fase',
    processo: 'Processo'
}
```

### 3. ✅ Campos Derivados Automáticos

Quando não presentes na planilha, são preenchidos automaticamente:

- **notificadora**: Usa o mesmo valor de "Notificada"
- **origem**: "Notificação Clínicas Sesi" (padrão)
- **acao_imediata**: "Sim" (padrão)

---

## Como Usar

### Importar Dados

1. **Prepare sua planilha Excel** com as 10 colunas obrigatórias
2. **Clique em "📤 Importar Excel"** no dashboard
3. **Selecione o arquivo** (.xlsx ou .xls)
4. **Aguarde a confirmação** de importação

**Comportamento:**
- ✅ Novas ocorrências são **adicionadas**
- ✅ Ocorrências existentes (mesmo código) são **atualizadas**
- ✅ Dados inválidos são **ignorados** com aviso no console

### Exportar Dados

1. **Clique em "📥 Exportar Excel"**
2. **Selecione as colunas** desejadas
3. **Clique em "Exportar"**
4. **Arquivo será baixado** automaticamente

**Formato do arquivo:**
- Nome: `ocorrencias_sesi_senai_YYYY-MM-DD.xlsx`
- Colunas: Conforme selecionadas
- Formato: Compatível com importação

---

## Validações

### Durante a Importação

✅ **Formato de arquivo**: Apenas .xlsx e .xls
✅ **Campo obrigatório**: Código (único campo realmente obrigatório)
✅ **Tipo de dados**: Conversão automática para string
✅ **Data**: Formatação automática para DD/MM/YYYY
✅ **Mês/Ano**: Extração automática da data (YYYY-MM)

### Valores Padrão

Se um campo estiver vazio na planilha:

| Campo | Valor Padrão |
|-------|--------------|
| Data | Data atual |
| Severidade | "Não Informado" |
| Tipo OMS | "Não Classificado" |
| Status | "Em Andamento" |
| Fase | "Avaliar Ocorrência" |
| Origem | "Notificação Clínicas Sesi" |
| Ação Imediata | "Sim" |

---

## Exemplo de Planilha

### Estrutura Mínima

```
| Código | Data       | Tipo de Ocorrência | Notificada | Severidade/Gravidade | Tipo de Incidente - OMS por Mês | Status | Responsável | Fase | Processo |
|--------|------------|-------------------|------------|---------------------|--------------------------------|--------|-------------|------|----------|
| 426    | 15/11/2025 | Queda             | Sesi Tabuleiro | Circunstância de Risco | Não Classificado | Em Andamento | fania.silva | Analisar Causa | Administrar Consultas |
```

### Planilha Completa (Exemplo)

```excel
Código | Data       | Tipo de Ocorrência              | Notificada           | Severidade/Gravidade           | Tipo de Incidente - OMS por Mês | Status       | Responsável          | Fase                              | Processo
-------|------------|--------------------------------|---------------------|-------------------------------|--------------------------------|--------------|---------------------|----------------------------------|----------------------------------
233    | 13/06/2024 | Identificação Errada Paciente  | Unidade Sesi Cambona| Evento com Nenhum Dano (Saúde)| Não Classificado               | Concluído    | carolina.albuquerque| Concluída                        | SP10.2.1.Gerenciar Serviços
252    | 13/11/2024 | Queda                          | Unidade Sesi Tabuleiro| Evento com Dano Leve (Saúde)| Não Classificado               | Concluído    | fania.silva         | Concluída                        | Administrar Acesso Paciente
```

---

## Mensagens de Feedback

### Sucesso
- ✅ "X ocorrências importadas com sucesso!"
- ✅ "X ocorrências atualizadas com sucesso!"
- ✅ "Arquivo Excel exportado com sucesso!"

### Erro
- ❌ "Formato de arquivo inválido. Selecione um arquivo .xlsx ou .xls"
- ❌ "O arquivo Excel está vazio ou não contém dados válidos"
- ❌ "Nenhum dado válido foi encontrado no arquivo"
- ❌ "Erro ao processar arquivo Excel. Verifique o formato"

### Avisos (Console)
- ⚠️ "Linha X: Campo obrigatório 'Código' ausente"
- ⚠️ "Erro ao processar linha X: [detalhes]"
- ℹ️ "Linha X: Ocorrência Y atualizada"
- ℹ️ "Linha X: Nova ocorrência Y adicionada"

---

## Compatibilidade

### Formatos Suportados
✅ Excel 2007+ (.xlsx)
✅ Excel 97-2003 (.xls)

### Navegadores
✅ Chrome/Edge (Chromium)
✅ Firefox
✅ Safari
✅ Opera

### Bibliotecas Utilizadas
- **SheetJS (XLSX.js)**: v0.18.5
- Carregada via CDN: `https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js`

---

## Troubleshooting

### Problema: "Nenhum dado válido encontrado"
**Solução:**
1. Verifique se a primeira linha contém os cabeçalhos exatos
2. Certifique-se de que há pelo menos uma linha com dados
3. Verifique se a coluna "Código" está preenchida

### Problema: "Formato de arquivo inválido"
**Solução:**
1. Salve o arquivo como .xlsx (Excel 2007+)
2. Não use formatos como .csv ou .txt
3. Certifique-se de que o arquivo não está corrompido

### Problema: Dados não aparecem após importação
**Solução:**
1. Abra o Console do navegador (F12)
2. Verifique mensagens de erro ou avisos
3. Confirme que os códigos são únicos
4. Recarregue a página e tente novamente

---

## Próximas Melhorias Sugeridas

1. 🔄 Validação de formato de data mais robusta
2. 🔄 Preview dos dados antes de importar
3. 🔄 Opção de escolher qual planilha importar (se houver múltiplas)
4. 🔄 Importação incremental (adicionar sem duplicar)
5. 🔄 Template de planilha para download
6. 🔄 Validação de valores permitidos (dropdown)
7. 🔄 Histórico de importações

---

## Status

✅ **Implementação Concluída**
✅ **Mapeamento de Colunas Atualizado**
✅ **Compatibilidade Bidirecional (Import/Export)**
✅ **Validações Implementadas**
✅ **Sem Erros de Sintaxe**
