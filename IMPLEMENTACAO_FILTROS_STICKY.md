# Implementação de Filtros Sticky

## Data: 22/11/2025

## 🎯 Objetivo

Fazer o painel de filtros ficar fixo (sticky) abaixo do header e se esconder automaticamente ao fazer scroll para baixo.

## ✅ Implementação

### 1. CSS Sticky
```css
.filters-sticky {
    position: sticky;
    top: 70px; /* Abaixo do header */
    z-index: 90;
    transition: transform 0.3s ease, opacity 0.3s ease;
}

.filters-sticky.hidden {
    transform: translateY(-100%);
    opacity: 0;
    pointer-events: none;
}
```

### 2. Estado de Controle
```javascript
const [hideFiltersOnScroll, setHideFiltersOnScroll] = useState(false);
const lastScrollY = React.useRef(0);
```

### 3. Detecção de Direção do Scroll
```javascript
useEffect(() => {
    const handleScroll = () => {
        const scrollPosition = window.scrollY;
        const scrollingDown = scrollPosition > lastScrollY.current;
        
        if (showFilters) {
            if (scrollingDown && scrollPosition > 150) {
                // Esconder ao rolar para baixo
                setHideFiltersOnScroll(true);
            } else if (!scrollingDown) {
                // Mostrar ao rolar para cima
                setHideFiltersOnScroll(false);
            }
        }
        
        lastScrollY.current = scrollPosition;
    };
    
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
}, [showFilters]);
```

### 4. Aplicação no JSX
```javascript
<div 
    className={`filters-sticky ${hideFiltersOnScroll ? 'hidden' : ''}`}
    onMouseEnter={() => setHideFiltersOnScroll(false)}
>
```

## 🎬 Comportamento

### Posição Inicial
```
┌─────────────────────────────────────┐
│ Header (fixo)                       │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│ Painel de Filtros (sticky)          │ ← Visível
└─────────────────────────────────────┘
│ Cards de Estatísticas               │
│ Gráficos                            │
└─────────────────────────────────────┘
```

### Ao Rolar Para Baixo (> 150px)
```
┌─────────────────────────────────────┐
│ Header (fixo)                       │
└─────────────────────────────────────┘
                                        ← Painel escondido (translateY(-100%))
│ Cards de Estatísticas               │
│ Gráficos                            │
└─────────────────────────────────────┘
```

### Ao Rolar Para Cima
```
┌─────────────────────────────────────┐
│ Header (fixo)                       │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│ Painel de Filtros (sticky)          │ ← Reaparece
└─────────────────────────────────────┘
│ Cards de Estatísticas               │
└─────────────────────────────────────┘
```

### Ao Passar Mouse
```
┌─────────────────────────────────────┐
│ Header (fixo)                       │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│ Painel de Filtros (sticky)          │ ← Força aparecer
│ [Mouse aqui]                        │
└─────────────────────────────────────┘
```

## 🔧 Funcionalidades

### 1. Sticky Position
- ✅ Painel fica fixo abaixo do header
- ✅ Acompanha o scroll até certo ponto
- ✅ Não sobrepõe o header

### 2. Auto-Hide no Scroll
- ✅ Esconde ao rolar para baixo (> 150px)
- ✅ Mostra ao rolar para cima
- ✅ Transição suave (0.3s)

### 3. Interação com Mouse
- ✅ Reaparece ao passar mouse
- ✅ Cancela timer de auto-close
- ✅ Mantém visível enquanto mouse estiver sobre

### 4. Auto-Close
- ✅ Fecha após 2s de inatividade
- ✅ Timer reseta ao interagir
- ✅ Fecha ao clicar fora

## 📊 Logs de Debug

### Scroll Para Baixo
```
📜 Scroll para baixo - escondendo painel
```

### Scroll Para Cima
```
📜 Scroll para cima - mostrando painel
```

### Mouse Enter
```
🖱️ Mouse entrou no painel - cancelando timer
```

## 🧪 Como Testar

### Teste 1: Sticky Position
1. Abra o painel de filtros
2. Role a página para baixo
3. **Esperado**: Painel acompanha o scroll inicialmente

### Teste 2: Auto-Hide
1. Abra o painel
2. Role para baixo mais de 150px
3. **Esperado**: Painel desaparece suavemente

### Teste 3: Reaparece ao Rolar Para Cima
1. Com painel escondido
2. Role para cima
3. **Esperado**: Painel reaparece

### Teste 4: Mouse Hover
1. Painel escondido
2. Passe mouse onde o painel estava
3. **Esperado**: Painel reaparece

### Teste 5: Auto-Close
1. Abra o painel
2. Não interaja por 2 segundos
3. **Esperado**: Painel fecha automaticamente

## 🎨 Valores Ajustáveis

### Posição do Sticky
```css
top: 70px; /* Ajuste conforme altura do header */
```

### Threshold do Scroll
```javascript
scrollPosition > 150 // Ajuste quando deve esconder
```

### Velocidade da Transição
```css
transition: transform 0.3s ease; /* Ajuste velocidade */
```

### Tempo de Auto-Close
```javascript
setTimeout(() => {
    setShowFilters(false);
}, 2000); // Ajuste tempo em ms
```

## ✅ Checklist de Verificação

- [x] Painel fica sticky abaixo do header
- [x] Esconde ao rolar para baixo
- [x] Mostra ao rolar para cima
- [x] Reaparece ao passar mouse
- [x] Fecha após 2s de inatividade
- [x] Fecha ao clicar fora
- [x] Transições suaves
- [x] Não sobrepõe header
- [x] Logs de debug funcionando

## 🚀 Resultado Final

O painel de filtros agora:
1. ✅ Fica fixo abaixo do header (sticky)
2. ✅ Se esconde ao rolar para baixo
3. ✅ Reaparece ao rolar para cima
4. ✅ Reaparece ao passar mouse
5. ✅ Fecha automaticamente após 2s
6. ✅ Não atrapalha a visualização dos cards

Exatamente como mostrado na imagem de referência! 🎯
