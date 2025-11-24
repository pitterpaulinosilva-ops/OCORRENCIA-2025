# Dashboard de Ocorrências - SESI/SENAI Alagoas

## 📊 Descrição
Painel interativo para visualização e análise de ocorrências do SESI/SENAI Alagoas, desenvolvido com HTML, CSS e JavaScript puro. Inclui funcionalidades avançadas de importação/exportação Excel e análise de dados em tempo real.

## ✨ Funcionalidades
- 📊 Visualização de dados em gráficos interativos (Chart.js)
- 📱 Interface responsiva para desktop e mobile
- 📈 Análise de tendências e estatísticas em tempo real
- 📤 **Importação de dados Excel** (.xlsx/.xls) com validação
- 📥 **Exportação personalizada para Excel** com seleção de colunas
- 🔍 Sistema de filtros avançados por status, unidade, severidade e período
- 📋 Tabela de dados detalhados com paginação e busca
- 🎨 Design moderno com cores institucionais SESI/SENAI
- 🧪 Testes de integridade e performance integrados

## 🚀 Tecnologias Utilizadas
- **HTML5** - Estrutura da aplicação
- **CSS3** - Estilização e layout responsivo
- **JavaScript (ES6+)** - Lógica da aplicação e interatividade
- **Chart.js** - Biblioteca para gráficos (CDN)
- **SheetJS** - Manipulação de arquivos Excel (CDN)

## 📋 Pré-requisitos
- **Node.js** (versão 16 ou superior)
- **npm** - Gerenciador de pacotes

## 🛠️ Instalação

### 1. Clone o repositório
```bash
git clone https://github.com/pitterpaulinosilva-ops/DASHBOARD-OCORRENCIA.git
cd DASHBOARD-OCORRENCIA
```

### 2. Instalar dependências
```bash
npm install
```

## 🏃‍♂️ Como Executar

### Desenvolvimento Local
```bash
# Servidor com reload automático
npm run dev

# Servidor HTTP simples
npm start

# Servidor alternativo
npm run serve
```

### Preview de Produção
```bash
npm run preview
```

## 🌐 Deploy na Vercel

### Deploy Automático (Recomendado)
1. Faça push do código para GitHub
2. Conecte seu repositório na [Vercel](https://vercel.com)
3. A Vercel detectará automaticamente as configurações

### Deploy via CLI
```bash
# Instalar Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy para produção
vercel --prod
```

### Configurações de Deploy
O projeto inclui `vercel.json` com:
- Configuração para SPA (Single Page Application)
- Headers de segurança
- Redirecionamento de rotas

## 📁 Estrutura do Projeto
```
dashboard-ocorrencias-2025/
├── assets/             # Recursos estáticos
│   └── icons/          # Ícones do projeto
│       ├── png/        # Ícones em formato PNG
│       └── svg/        # Ícones em formato SVG
├── index.html          # Aplicação principal (SPA)
├── index.html.backup   # Backup da versão anterior
├── package.json        # Configurações e scripts
├── package-lock.json   # Lock de dependências
├── vercel.json         # Configurações de deploy Vercel
├── .gitignore          # Arquivos ignorados pelo Git
└── README.md           # Documentação
```

## 🔧 Scripts Disponíveis
```bash
npm start           # Servidor de desenvolvimento
npm run dev         # Desenvolvimento com live reload
npm run serve       # Servidor alternativo
npm run build       # Preparar para produção
npm run preview     # Preview da versão de produção
```

## 📊 Funcionalidades Excel
### Importação
- Suporte para arquivos .xlsx e .xls
- Validação automática de dados
- Verificação de integridade
- Atualização em tempo real do dashboard

### Exportação
- Seleção personalizada de colunas
- Barra de progresso
- Mensagens de status
- Formato Excel nativo

## 🧪 Testes Integrados
O sistema inclui testes automáticos para:
- Integridade de dados
- Performance das operações
- Compatibilidade com Excel
- Validação de formatos

## 🌍 URLs de Produção
- **Desenvolvimento**: `http://localhost:3000`
- **Produção**: `https://dashboard-ocorrencias-2025.vercel.app`

## 🔒 Segurança
- Headers de segurança configurados
- Validação de dados de entrada
- Proteção contra XSS
- Sanitização de uploads

## 📱 Compatibilidade
- ✅ Chrome 80+
- ✅ Firefox 75+
- ✅ Safari 13+
- ✅ Edge 80+
- ✅ Dispositivos móveis

## 🤝 Contribuição
1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença
Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 📞 Suporte
Para dúvidas ou problemas:
- 📧 Email: ti@sesisenal-al.org.br
- 🐛 Issues: [GitHub Issues](https://github.com/seu-usuario/dashboard-ocorrencias-2025/issues)

---
**Desenvolvido com ❤️ pela equipe SESI/SENAI Alagoas**