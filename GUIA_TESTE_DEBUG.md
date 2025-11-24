# Guia de Teste e Debug - Dashboard Modern

## Data: 22/11/2025

## 🎯 Objetivo

Testar e identificar problemas no dashboard-modern.html usando logs de debug.

## 📋 Preparação

### 1. Abrir o Dashboard
```powershell
# No PowerShell (Windows)
Start-Process dashboard-modern.html
```

Ou simplesmente clique duas vezes no arquivo `dashboard-modern.html`

### 2. Abrir DevTools
- Pressione `F12` ou
- Clique com botão direito → "Inspecionar" ou
- Menu → Mais ferramentas → Ferramentas do desenvolvedor

### 3. Ir para a aba Console
- Clique na aba "Console"
- Limpe o console (ícone 🚫 ou Ctrl+L)

## 🧪 Testes a Realizar

### Teste 1: Verificar se o Dashboard Carrega
**Esperado**: Ver mensagem no console
```
🔍 showFilters mudou para: false
```

**Se não aparecer**:
- ❌ React não está carregando
- ❌ Babel não está transpilando
- ❌ Erro de sintaxe no código

### Teste 2: Clicar no Botão de Filtros
**Ação**: Clique no botão "Filtros" no canto superior direito

**Esperado no console**:
```
🔘 Botão de filtros clicado! Estado atual: false
🔍 showFilters mudou para: true
⏱️ Auto-hide: Iniciando timer de 2 segundos...
👆 Click-outside: Adicionando listener...
👆 Click-outside: Listener adicionado após delay
```

**Se não aparecer**:
- ❌ Botão não está visível
- ❌ onClick não está funcionando
- ❌ Estado não está atualizando

### Teste 3: Aguardar 2 Segundos (Sem Interagir)
**Ação**: Após abrir o painel, não faça nada por 2 segundos

**Esperado no console**:
```
⏰ Auto-hide: Timer expirou! Fechando painel...
🔍 showFilters mudou para: false
🧹 Auto-hide: Cleanup - removendo timer
👆 Click-outside: Cleanup - removendo listener
```

**Esperado visualmente**:
- ✅ Painel fecha automaticamente

**Se não fechar**:
- ❌ setTimeout não está funcionando
- ❌ setShowFilters não está atualizando

### Teste 4: Passar Mouse sobre o Painel
**Ação**: 
1. Abra o painel
2. Passe o mouse sobre ele

**Esperado no console**:
```
🖱️ Mouse entrou no painel - cancelando timer
```

**Ação**: Saia do painel com o mouse

**Esperado no console**:
```
🖱️ Mouse saiu do painel - reiniciando timer (2s)
```

**Aguarde 2 segundos**:
```
⏰ Timer após mouse leave expirou!
🔍 showFilters mudou para: false
```

### Teste 5: Clicar no Painel
**Ação**:
1. Abra o painel
2. Clique em qualquer lugar dentro dele

**Esperado no console**:
```
🖱️ Painel clicado - resetando timer (2s)
👆 Click-outside: Click detectado [elemento]
👆 Click-outside: Click dentro do painel, ignorar
```

### Teste 6: Clicar Fora do Painel
**Ação**:
1. Abra o painel
2. Clique em qualquer lugar FORA dele (nos cards, por exemplo)

**Esperado no console**:
```
👆 Click-outside: Click detectado [elemento]
👆 Click-outside: Click fora do painel! Fechando...
🔍 showFilters mudou para: false
```

**Esperado visualmente**:
- ✅ Painel fecha imediatamente

## 📊 Interpretando os Resultados

### ✅ Tudo Funcionando
Se todos os logs aparecerem conforme esperado:
- Dashboard está funcionando corretamente
- Todas as funcionalidades implementadas

### ❌ Problemas Comuns

#### Problema 1: Nenhum Log Aparece
**Causa**: React/Babel não está carregando
**Solução**:
1. Verificar conexão com internet
2. Verificar aba Network para ver se scripts carregaram
3. Tentar em navegador diferente

#### Problema 2: Botão Não Aparece
**Causa**: CSS ou layout
**Solução**:
1. Inspecionar elemento (F12 → Elements)
2. Procurar pelo botão no HTML
3. Verificar estilos aplicados

#### Problema 3: Timer Não Funciona
**Causa**: setTimeout não executando
**Solução**:
1. Verificar se logs de timer aparecem
2. Verificar se cleanup está sendo chamado
3. Testar com tempo maior (5000ms)

#### Problema 4: Click Outside Não Funciona
**Causa**: Event listener não adicionado
**Solução**:
1. Verificar se log "Listener adicionado" aparece
2. Verificar se ref está correto
3. Testar com delay maior (500ms)

## 🔧 Comandos Úteis no Console

### Verificar se React está carregado:
```javascript
console.log('React:', typeof React);
console.log('ReactDOM:', typeof ReactDOM);
```

### Verificar estado atual:
```javascript
// Não funciona diretamente, mas pode ver nos React DevTools
```

### Forçar fechamento do painel:
```javascript
// Clicar no botão novamente
```

## 📝 Relatório de Bugs

Se encontrar problemas, anote:

1. **O que você fez**: (ex: "Cliquei no botão de filtros")
2. **O que esperava**: (ex: "Painel deveria abrir")
3. **O que aconteceu**: (ex: "Nada aconteceu")
4. **Logs no console**: (copie e cole)
5. **Navegador**: (Chrome, Firefox, Edge, etc.)
6. **Screenshots**: (se possível)

## 🎬 Próximos Passos

Após os testes:

1. Se tudo funcionar: ✅ Remover logs de debug
2. Se algo não funcionar: 🔧 Usar logs para identificar problema
3. Compartilhar resultados para análise

## 📞 Suporte

Precisa de ajuda? Compartilhe:
- Screenshots do console
- Descrição do problema
- Navegador usado
- Logs completos
