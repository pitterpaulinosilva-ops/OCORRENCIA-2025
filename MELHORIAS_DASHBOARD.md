# Melhorias para o Dashboard de Ocorrências

## Análise Atual

O dashboard está usando Chart.js com HTML/CSS/JavaScript puro. Após a remoção de 4 gráficos (Timeline Mensal, Unidades Notificadoras, Origem da Notificação, Status das Ocorrências), alguns gráficos podem estar aparecendo em branco.

## Problemas Identificados

1. **Gráficos removidos mas código de inicialização pode estar incompleto**
2. **Falta de tratamento de erros na inicialização dos gráficos**
3. **Possível problema com o carregamento assíncrono**

## Soluções Propostas

### 1. Adicionar Verificação de Elementos Canvas

Antes de criar cada gráfico, verificar se o elemento canvas existe:

```javascript
const canvas = document.getElementById('chartId');
if (canvas && canvas.getContext) {
    charts.chartId = new Chart(canvas, {
        // configuração
    });
} else {
    console.error('Canvas não encontrado: chartId');
}
```

### 2. Adicionar Try-Catch na Inicialização

```javascript
try {
    charts.chartId = new Chart(document.getElementById('chartId'), {
        // configuração
    });
} catch (error) {
    console.error('Erro ao criar gráfico:', error);
}
```

### 3. Verificar Dados Antes de Atualizar

```javascript
function updateChart(chartId, labels, data) {
    if (charts[chartId] && labels && data && data.length > 0) {
        charts[chartId].data.labels = labels;
        charts[chartId].data.datasets[0].data = data;
        charts[chartId].update('active');
    }
}
```

## Migração para Shadcn/UI (Futuro)

Para uma versão futura com React/Next.js:

1. **Instalar dependências**:
```bash
npm install recharts lucide-react
npx shadcn-ui@latest init
npx shadcn-ui@latest add card chart
```

2. **Usar componentes Recharts** ao invés de Chart.js
3. **Aplicar design tokens do shadcn/ui**

## Correções Imediatas

Vou aplicar as seguintes correções no arquivo atual:

1. ✅ Adicionar verificações de segurança na inicialização
2. ✅ Adicionar try-catch para capturar erros
3. ✅ Melhorar logs de debug
4. ✅ Garantir que dados existem antes de renderizar
