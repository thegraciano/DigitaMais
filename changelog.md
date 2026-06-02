# Changelog — DigitaMais

## v2.1.0 — 2025-06-02

### 🔒 Segurança
- Senhas e nome de usuário admin migrados de texto puro para hashes SHA-256 via Web Crypto API nativa (sem dependências externas)
- Comparação de credenciais agora é 100% assíncrona e baseada em hash — nenhuma credencial fica legível no código-fonte
- `saveCredentials` passa a armazenar `userHash` e `passHash`; o valor original nunca é retido em memória após o hash
- Removido comentário instrucional que indicava como extrair senhas via console do navegador
- Adicionada função `esc()` de sanitização HTML (escapa `& < > " '`) aplicada a todos os pontos onde dados do usuário entram no DOM
- Corrigido XSS em `renderAdminWords`: palavras adicionadas pelo admin eram inseridas via `innerHTML` sem escape — reescrito com `createElement` + `textContent`
- Corrigido XSS na lista de resultados: `r.word` e nome do aluno entravam em `innerHTML` — substituído por construção segura via DOM
- Corrigido XSS no painel de celebração (`celeb-stats`): template string com `innerHTML` substituída por `createElement`
- Corrigido XSS no relatório PDF: `r.studentName`, `item.word`, `bestItem.word` e `worstItem.word` agora passam por `esc()` antes de entrar no template HTML
- Nome do aluno sanitizado e limitado a 60 caracteres na entrada

### 🎵 Áudio
- Trilha sonora de fundo substituída: BPM elevado de 72 para 130, onda `sine` trocada por `square` (estilo arcade), melodia reescrita em escala maior com contratempo e baixo marcado
- Adicionado som de contagem regressiva: beep curto nos números 3-2-1 e acorde ascendente no "VAI!"
- Adicionada fanfarra de vitória ao finalizar atividade (8 notas em progressão ascendente)

### 🐛 Correções
- Corrigido bug crítico em `finishGame`: referência a `#error-alert` (inexistente) trocada para `#high-error-alert` — impedia a tela de conclusão de aparecer ao terminar uma atividade
- Corrigido perda de foco ao alternar teclado virtual durante jogo: botão "Teclado" agora chama `focusInput()` após toggle, eliminando a necessidade de clicar no texto para continuar digitando

### ⌨️ Teclado Virtual
- Adicionado indicador de Caps Lock: badge âmbar animado aparece acima do teclado quando Caps Lock está ativo; tecla Caps Lock no teclado virtual é destacada em laranja
- Detecção de Caps Lock via `getModifierState` + listener no evento `keydown`
- Modo misto: teclas Shift (⇧) destacadas em verde com tooltip "Shift + [letra]" sempre que a próxima letra exigida for maiúscula, ensinando visualmente o uso correto do Shift no ABNT2
- Letras maiúsculas acentuadas também acionam o highlight do Shift junto à sequência de tecla morta
