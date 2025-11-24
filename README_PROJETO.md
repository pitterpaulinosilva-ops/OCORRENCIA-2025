# 📊 Dashboard de Ocorrências - SESI/SENAI Alagoas

## 🎯 Sobre o Projeto

Dashboard moderno e responsivo para gerenciamento e visualização de ocorrências do SESI/SENAI Alagoas, desenvolvido com React, Recharts e Tailwind CSS.

## ✨ Funcionalidades

### 📈 Visualizações
- **Cards de Estatísticas**: Total, Concluídas, Em Andamento, Taxa de Conclusão
- **5 Gráficos Interativos**:
  - Ocorrências por Severidade (Barras)
  - Top 5 Unidades (Pizza)
  - Tipos de Ocorrência (Barras Horizontais)
  - Evolução Temporal (Linha)
  - Processos Mais Afetados (Barras)

### 🔍 Filtros Avançados
- **4 Filtros Disponíveis**:
  - Status (Todos, Concluído, Em Andamento)
  - Unidade (5 unidades)
  - Severidade (7 níveis)
  - Período (Mês/Ano - 13 períodos)

### 🎨 Interface Moderna
- ✅ Design responsivo (Mobile, Tablet, Desktop)
- ✅ Painel de filtros sticky com auto-hide
- ✅ Animações suaves
- ✅ Cores institucionais SESI/SENAI
- ✅ Tema shadcn/ui

### 🚀 Funcionalidades Especiais
- **Auto-Hide**: Painel de filtros fecha após 2s de inatividade
- **Sticky Header**: Header fixo ao fazer scroll
- **Click Outside**: Fecha painel ao clicar fora
- **Logs de Debug**: Console detalhado para troubleshooting

## 📁 Estrutura do Projeto

```
OCORRENCIA-2025/
├── dashboard-modern.html          # Dashboard principal (React + Recharts)
├── index.html                     # Dashboard original (Chart.js)
├── test-select.html              # Teste isolado de selects
├── test-dashboard.html           # Teste de funcionalidades
├── assets/
│   └── icons/svg/                # Ícones SVG
├── docs/                         # Documentação (*.md)
│   ├── FILTRO_PERIODO_IMPLEMENTADO.md
│   ├── IMPLEMENTACAO_FILTROS_STICKY.md
│   ├── OTIMIZACAO_LAYOUT_FILTROS.md
│   └── ...
└── README.md
```

## 🚀 Como Usar

### Opção 1: Abrir Diretamente
```bash
# Abrir no navegador padrão
start dashboard-modern.html
```

### Opção 2: Servidor Local
```bash
# Python
python -m http.server 8000

# Node.js
npx http-server

# Acesse: http://localhost:8000/dashboard-modern.html
```

### Opção 3: Deploy (Vercel)
```bash
# Instalar Vercel CLI
npm i -g vercel

# Deploy
vercel
```

## 📊 Dados

### Estrutura dos Dados
```javascript
{
    codigo: "233",
    data: "13/06/2024",
    mes_ano: "2024-06",
    status: "Concluído",
    notificada: "Unidade Sesi Cambona",
    severidade: "Evento com Nenhum Dano (Saúde)",
    tipo_incidente_oms: "Não Classificado",
    origem: "Notificação Clínicas Sesi",
    processo: "SP10.2.1.Gerenciar Serviços...",
    responsavel: "carolina.albuquerque",
    ocorrencia: "Identificação Errada do Paciente",
    acao_imediata: "Não",
    notificadora: "Segurança e Saúde...",
    fase: "Concluída"
}
```

### Total de Dados
- **60 ocorrências** (Jun/2024 a Nov/2025)
- **5 unidades** diferentes
- **7 níveis** de severidade
- **13 períodos** (meses)

## 🎨 Tecnologias

### Frontend
- **React 18** - Biblioteca UI
- **Recharts 2.10** - Gráficos interativos
- **Tailwind CSS** - Estilização
- **Babel Standalone** - Transpilação JSX

### Bibliotecas
- **XLSX** - Exportação Excel
- **Lucide Icons** - Ícones

### Design System
- **shadcn/ui** - Componentes base
- **Cores Institucionais** - SESI/SENAI

## 📱 Responsividade

### Breakpoints
- **Mobile**: < 640px (1 coluna)
- **Tablet**: 640px - 1024px (2 colunas)
- **Desktop**: > 1024px (4 colunas)

### Otimizações Mobile
- Font size 16px (evita zoom iOS)
- Touch-friendly (44px mínimo)
- Scroll otimizado
- Layout adaptável

## 🧪 Testes

### Arquivos de Teste
1. **test-select.html** - Teste de selects
2. **test-dashboard.html** - Teste de funcionalidades
3. **test-charts.html** - Teste de gráficos

### Como Testar
```bash
# Abrir arquivo de teste
start test-select.html

# Verificar console (F12)
# Testar funcionalidades
# Verificar logs
```

## 📚 Documentação

### Principais Documentos
- `FILTRO_PERIODO_IMPLEMENTADO.md` - Filtro de período
- `IMPLEMENTACAO_FILTROS_STICKY.md` - Filtros sticky
- `OTIMIZACAO_LAYOUT_FILTROS.md` - Layout responsivo
- `CORRECAO_SELECT_PERIODO.md` - Correção de bugs
- `GUIA_TESTE_DEBUG.md` - Guia de testes

### Logs de Debug
```javascript
// Console mostra:
🔍 showFilters mudou para: true
⏱️ Auto-hide: Iniciando timer de 2 segundos...
📅 Período selecionado: 2025-01
🔍 Aplicando filtros...
✓ Filtro Período aplicado: 2025-01 - 3 resultados
📊 Total após filtros: 3 de 60
```

## 🎯 Funcionalidades Detalhadas

### 1. Painel de Filtros Sticky
- Fica fixo abaixo do header
- Esconde ao rolar para baixo
- Mostra ao rolar para cima
- Auto-hide após 2s

### 2. Filtros Inteligentes
- Combinação de múltiplos filtros
- Contador de filtros ativos
- Resumo dos filtros aplicados
- Botão limpar filtros

### 3. Gráficos Interativos
- Tooltips informativos
- Animações suaves
- Cores institucionais
- Responsivos

### 4. Cards de Estatísticas
- Atualização em tempo real
- Cores diferenciadas
- Ícones intuitivos
- Valores destacados

## 🔧 Configuração

### Cores Institucionais
```css
--sesi-blue: #003E7E;
--sesi-red: #E30613;
--senai-blue: #00579D;
--senai-orange: #FF6600;
```

### Breakpoints Tailwind
```javascript
sm: '640px',  // Tablet
md: '768px',  // Tablet grande
lg: '1024px', // Desktop
xl: '1280px'  // Desktop grande
```

## 📈 Melhorias Futuras

- [ ] Exportação de relatórios PDF
- [ ] Filtros salvos (localStorage)
- [ ] Modo escuro
- [ ] Gráficos adicionais
- [ ] Integração com API
- [ ] Autenticação de usuários
- [ ] Notificações em tempo real

## 🤝 Contribuindo

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'feat: Nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## 📝 Changelog

### v2.0.0 (22/11/2025)
- ✅ Dashboard moderno com React
- ✅ Filtros otimizados e responsivos
- ✅ Painel sticky com auto-hide
- ✅ Filtro de período funcional
- ✅ Layout responsivo completo
- ✅ Logs de debug
- ✅ Documentação completa

### v1.0.0 (Anterior)
- Dashboard original com Chart.js
- Filtros básicos
- 50 ocorrências

## 📄 Licença

Este projeto é propriedade do SESI/SENAI Alagoas.

## 👥 Autores

- **SESI/SENAI Alagoas** - Dados e requisitos
- **Desenvolvimento** - Dashboard e funcionalidades

## 🔗 Links

- **Repositório**: https://github.com/pitterpaulinosilva-ops/OCORRENCIA-2025
- **Demo**: [Em breve]
- **Documentação**: Ver pasta `/docs`

## 📞 Suporte

Para dúvidas ou problemas:
1. Verifique a documentação em `/docs`
2. Consulte os arquivos de teste
3. Abra uma issue no GitHub
4. Verifique os logs no console (F12)

---

**Desenvolvido com ❤️ para SESI/SENAI Alagoas**

**Última atualização**: 22/11/2025
